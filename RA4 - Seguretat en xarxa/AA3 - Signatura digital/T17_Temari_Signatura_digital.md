# RA4 · AA3 — Signatura digital

*Del hash xifrat a la confiança: com sabem que un document és autèntic.*

## 1. Introducció

En el món físic, la signatura permetia identificar una persona i garantir la seva autorització sobre un document. En el món digital calen mecanismes equivalents, i aquí apareixen dos conceptes que sovint es confonen:

- **Signatura digital**: mecanisme TÈCNIC i criptogràfic per xifrar i protegir les dades d'un document.
- **Signatura electrònica**: concepte LEGAL que atorga validesa a la voluntat de signar un document digital.

> 💡 La signatura digital és la tecnologia; la signatura electrònica és el concepte legal que li dona validesa jurídica.

## 2. Com funciona la signatura digital

Es basa en criptografia asimètrica + funcions hash (RA3).

### 2.1. Procés de signatura

1. Generació del hash (ex: SHA-256) del document.
2. Xifrat del hash amb la clau PRIVADA del signant → és la signatura.
3. S'envia el document + la signatura.

### 2.2. Procés de verificació

1. El receptor rep document + signatura.
2. Desxifra la signatura amb la clau PÚBLICA del signant.
3. Calcula un nou hash del document rebut.
4. Si coincideixen → document autèntic i íntegre.

### 2.3. Objectius de seguretat garantits

- **Autenticitat**: l'emissor és qui diu ser.
- **Integritat**: el document no s'ha alterat.
- **Vinculació (no-repudi)**: el signant no pot negar haver-lo signat.

## 3. El problema de la identitat

Com garantir que una clau pública és realment de qui diu ser?

### 3.1. Sistemes descentralitzats

Els usuaris es validen mútuament les claus (OpenPGP, "xarxa de confiança"). Servidors com keys.openpgp.org en publiquen les signatures.

### 3.2. Certificats digitals

Format habitual: **X.509**. Conté la clau pública, la identitat del titular, número de sèrie, dades de l'emissor i data de caducitat, signat per una **CA**.

> 💡 En entorns privats es poden usar claus **autosignades**; en entorns públics cal una CA reconeguda.

## 4. Trusted Third Party (TTP) i autoritats de certificació

Una TTP és una entitat neutral que dona fe que una clau pública pertany a qui diu. Igual que confiem en un DNI perquè confiem en l'organisme emissor, confiem en un certificat perquè confiem en la CA.

### 4.1. Funcions de la CA

- Validar la identitat del sol·licitant.
- Emetre i signar certificats.
- Gestionar la revocació.

Les CA poden ser **públiques** (DigiCert, Let's Encrypt, FNMT, CatCert) o **privades** (ús intern).

### 4.2. Model jeràrquic

**CA Arrel** (molt protegida, instal·lada de fàbrica) → **CA Intermèdia** (emissió diària) → Certificat de domini/servidor/usuari.

> 📌 **Cas real:** DigiNotar (2011), CA atacada que va permetre emetre certificats falsos per a Google; l'incident va provocar la seva fallida.

## 5. Infraestructura de clau pública (PKI)

| Component | Funció |
|---|---|
| CA | "Notari digital": emet, signa i revoca certificats. |
| RA | Verifica la identitat abans que la CA emeti el certificat. |
| VA | Comprova en temps real l'estat del certificat (OCSP). |
| TSA | Certifica la data/hora exacta d'una signatura. |

## 6. Atacs a la identitat

Els atacs homogràfics registren dominis amb caràcters visualment similars (ex: òmicron grega per "o") per enganyar amb un certificat "vàlid" d'un domini fals.

> ⚠️ Precaucions: mai compartir la clau privada; comprovar sempre el domini i la validesa del certificat; no fer clic en enllaços sospitosos.

## 7. Signatura electrònica: el marc legal (eIDAS)

El Reglament eIDAS (UE 910/2014) defineix tres nivells:

| Nivell | Validesa | Exemple |
|---|---|---|
| Simple | Molt limitada, fàcil d'impugnar | Nom al final d'un correu |
| Avançada | Identificació única + integritat | Contracte signat des del mòbil amb SMS |
| Qualificada | Equivalent a la manuscrita | DNIe, FNMT, idCAT + dispositiu segur (QSCD) |

## 8. Pràctica amb OpenSSL

```
openssl req -x509 -newkey rsa:3072 -keyout priv.pem -out cert.pem \
    -days 365 -nodes -subj "/C=ES/O=Empresa/CN=domini"
openssl x509 -in cert.pem -noout -subject -issuer -dates -fingerprint -sha256
```

En un certificat **autosignat**, `subject` i `issuer` coincideixen.

## Resum de l'apartat

- Signatura digital (tecnologia) i electrònica (validesa legal) són conceptes diferents.
- La signatura digital combina hash + xifrat amb clau privada: autenticitat, integritat i no-repudi.
- Els certificats X.509 i les CA resolen el problema de confiar en una clau pública desconeguda.
- El model PKI (CA, RA, VA, TSA) organitza la infraestructura de confiança.
- eIDAS defineix 3 nivells de signatura electrònica amb diferent validesa jurídica.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF5/AA3-SignaturaDigital.md) (GitHub, SMX-0226SI) — llicència CC-BY-SA-4.0.
- Reglament eIDAS (UE) 910/2014.
- Signicat — "Electronic signature: what is it and how to use it".
- [OpenSSL](https://openssl.org)

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
