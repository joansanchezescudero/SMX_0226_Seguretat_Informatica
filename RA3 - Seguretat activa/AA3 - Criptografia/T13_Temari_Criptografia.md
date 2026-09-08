# RA3 · AA3 — Criptografia

*Del Codi Cèsar a l'AES: com protegim la confidencialitat i la integritat.*

## 1. Introducció

La criptografia és la ciència que s'encarrega de protegir la confidencialitat i la integritat de les dades, i també de garantir la identitat a les comunicacions.

Durant segles s'ha utilitzat per protegir missatges: des del Codi Cèsar fins a la màquina Enigma alemanya de la Segona Guerra Mundial. La criptoanàlisi és la ciència que s'encarrega de trencar aquests codis i xifrats.

**Xifrat**: transformar un text pla en text xifrat mitjançant un algorisme i una clau. **Desxifrat**: el procés invers.

> 💡 No confondre xifrar amb codificar. Una codificació (com Base64) NO assegura la confidencialitat: només representa la informació amb un alfabet diferent. Qualsevol la pot decodificar.

Seguretat **incondicional** (segur amb poder computacional infinit, rar — ex: xifrat de Vernam) vs. seguretat **condicional** (la majoria dels sistemes actuals, com AES: segurs avui, potencialment trencables en el futur).

## 2. Criptografia de clau simètrica

La mateixa clau xifra i desxifra. Emissor i receptor l'han de conèixer i mantenir en secret.

Algorismes: **AES**, DES/3DES, IDEA, RC4, Blowfish. **AES-256** és l'estàndard recomanat des de 2001.

| | |
|---|---|
| **Avantatges** | Confidencialitat garantida; ràpid; text xifrat curt. |
| **Inconvenients** | Problema de l'intercanvi de claus; no garanteix integritat ni no-rebuig. |

## 3. Criptografia de clau pública

Parell de claus: **privada** i **pública**. Xifrar amb la pública del destinatari; només la seva privada ho desxifra. Resol el problema de l'intercanvi de claus.

Algorismes: RSA, DSA, ElGamal, corba el·líptica.

> 💡 Si es xifra amb la clau PRIVADA, només es desxifra amb la PÚBLICA: així es verifica que el missatge prové del propietari — la base de la **signatura digital**.

| | |
|---|---|
| **Avantatges** | Resol l'intercanvi de claus; permet signatura digital i autenticació. |
| **Inconvenients** | Més lent; claus i missatges més llargs. |

## 4. Criptografia híbrida

En la pràctica es combinen els dos tipus: xifrat simètric per al gruix de dades (amb una clau de sessió), i clau pública per intercanviar aquesta clau de sessió.

### 4.1. Diffie-Hellman

Mètode per generar una clau de sessió compartida **sense transmetre-la mai directament**: cada participant la calcula independentment a partir d'un secret propi i de valors públics (p, g). La seguretat es basa en la dificultat de calcular logaritmes discrets.

> ⚠️ Diffie-Hellman aplica **forward secrecy**: si un atacant obté la clau privada d'un participant, no pot calcular claus de sessió PASSADES (s'esborren de la RAM en acabar la sessió).

## 5. Control d'integritat: funcions hash

Generen un resum de mida FIXA per a qualsevol entrada. Condicions: fàcil de calcular, impossible d'invertir, sense col·lisions pràctiques.

Es compara el hash calculat en recepció amb el rebut per verificar la integritat. Avui s'usen **SHA-256/SHA-512**; MD5 i SHA-1 estan **obsolets** (vulnerabilitats de col·lisió).

> 💡 HMAC combina el hash amb una clau secreta compartida: afegeix autenticitat de l'emissor, no només integritat.

### 5.1. Usos del hash

- Validar que un fitxer no ha estat modificat.
- Comprovar la integritat de descàrregues (ex: ISO d'un SO).
- Emmagatzemar contrasenyes de forma segura (es desa el hash, no la contrasenya).
- Signatura digital: es signa el HASH del document, no l'original.

## 6. Pràctica amb OpenSSL

OpenSSL implementa la pràctica totalitat dels algorismes vistos.

### 6.1. Xifrat simètric AES-256

```
openssl enc -aes-256-cbc -pbkdf2 -salt -in fitxer.txt -out fitxer.enc -pass pass:contrasenya
```

(afegint `-d` es desxifra). El fitxer resultant és binari i il·legible sense la contrasenya correcta.

### 6.2. Generació de claus i signatura digital

```
openssl genrsa -out privada.pem 3072
openssl rsa -in privada.pem -pubout -out publica.pem
openssl dgst -sha256 -sign privada.pem -out doc.sig doc.txt
openssl dgst -sha256 -verify publica.pem -signature doc.sig doc.txt
```

Retorna `Verified OK` si tot és correcte, o `Verification failure` si el document s'ha modificat després de signar-lo.

## Resum de l'apartat

- Simètric: ràpid, problema d'intercanvi de claus. Asimètric: resol l'intercanvi, més lent.
- La criptografia híbrida combina tots dos; Diffie-Hellman negocia la clau de sessió sense transmetre-la.
- Les funcions hash (SHA-256/512) garanteixen la integritat.
- La signatura digital combina hash + clau privada: autenticitat, integritat i no-repudi.
- OpenSSL permet practicar tots aquests conceptes des de la línia de comandes.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF3/AA3-Criptografia.md) (GitHub, SMX-0226SI) — llicència CC-BY-SA-4.0.
- Practical Networking — "Cryptography".
- DCODE — "Codi de rotació o de Cèsar".
- [OpenSSL](https://openssl.org)

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
