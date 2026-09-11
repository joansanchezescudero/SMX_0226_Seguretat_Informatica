# RA1 · AA3 — Seguretat lògica

*Qui ets i què pots fer.*

## 1. Molt abans dels ordinadors

Els sentinelles militars, quan s'acostava algú desconegut, calia que diguessin una senya (una pregunta) i responguessin la contrasenya correcta per demostrar que eren del bàndol amic. Avui, la lògica és exactament la mateixa: el sistema ha de saber si ets "amic" (usuari autoritzat) o "enemic" (intrús) abans de deixar-te entrar.

## 2. El concepte clau: autenticació vs. autorització

- **Autenticació**: verifica QUI ets ("demostra que ets tu"). Contrasenya, targeta, empremta...
- **Autorització**: determina QUÈ pots fer ("tens permís per a això?"). Consulta la base de dades d'autorització.

> 💡 Primer cal AUTENTICAR-SE per entrar; després, el sistema AUTORITZA (o no) cada acció que es vulgui fer.

## 3. Objectes, subjectes i drets d'accés

- **Objecte**: el recurs amb accés controlat (fitxer, directori, registre...).
- **Subjecte**: qui vol accedir-hi (normalment, un usuari, a través d'un procés).

3 classes de subjecte: **propietari** (creador), **grup** (privilegis compartits) i **altres**. 5 drets d'accés possibles: lectura, escriptura, execució, esborrament, creació.

## 4. Control d'accés discrecional (DAC): la matriu de control d'accés

Files = subjectes, columnes = objectes; cada cel·la indica els drets d'aquell subjecte sobre aquell objecte.

| Subjecte | /home/albert | /home/berta | /etc/passwd |
|---|---|---|---|
| Albert | Lectura, escriptura, cd | — | Lectura |
| Berta | — | Lectura, escriptura, cd | Lectura |
| Carme | Lectura, escriptura, cd | Lectura, escriptura, cd | Lectura, escriptura |

Es pot descompondre de dues maneres:

- **Llistes de control d'accés (ACL)**: per columnes — cada objecte porta la llista de qui hi pot accedir. Windows funciona així.
- **Capacitats**: per files — cada subjecte porta la llista del que pot fer. Linux/UNIX combinen ambdós sistemes.

> 📌 **Cas real:** l'any 2002, una periodista es va fer famosa per aconseguir accés al compte de correu de Saddam Hussein sense grans coneixements tècnics. El mal ús de les contrasenyes és, encara avui, una de les 10 amenaces més habituals.

## 5. Política de contrasenyes

| Febles | Robustes |
|---|---|
| Menys de 10 caràcters | Majúscules i minúscules |
| Una paraula de diccionari | Text + números + alfanumèrics |
| Nom de familiar, mascota... | Mínim 10 caràcters |
| Un patró: 1234, qwerty... | Sense relació amb dades personals |

### 5.1. Truc pràctic: robustes i fàcils de recordar

1. Pensa una frase fàcil de recordar: *"Això és una manera de recordar una contrasenya"*.
2. Agafa la inicial de cada paraula: `A·é·u·m·d·r·u·c`.
3. Canvia "una" per "1" i afegeix un símbol final: `Ae1MdR1c!`

> 💡 Resultat: una contrasenya de 9 caràcters, amb majúscules, minúscules, números i símbols, que es pot reconstruir mentalment en pocs segons.

### 5.2. Una contrasenya robusta... mal protegida no serveix

L'**enginyeria social** és l'atac més comú: un atacant truca fent-se passar per l'administrador de sistemes i demana la contrasenya; com que l'usuari no el coneix en persona, se la dona sense sospitar res.

Normes bàsiques: no dir-la mai per telèfon ni correu; no dir-la a companys, encara que siguin superiors; no apuntar-la mai en un paper; canviar-la com a mínim cada sis mesos.

## 6. Sistemes biomètrics

- Basats en un atribut físic ("alguna cosa que ÉS"): empremtes, iris, retina, palmell, cara.
- Basats en el comportament ("alguna cosa que FA"): signatura, forma d'escriure... poden canviar amb el temps.

### 6.1. Cap sistema és infal·lible

- **Fals positiu**: el sistema ACCEPTA un impostor que hauria d'haver estat denegat.
- **Fals negatiu**: el sistema DENEGA l'accés a un usuari que hauria d'haver estat acceptat.

## 7. Els 3 factors d'autenticació

- Alguna cosa que **SAPS**: contrasenya, PIN — econòmic, però es pot esbrinar.
- Alguna cosa que **TENS**: clau, targeta — es pot perdre o robar.
- Alguna cosa que **ETS o FAS**: empremta, retina, veu — sistemes biomètrics.

> 💡 L'autenticació multifactor combina 2 o 3 factors (ex: contrasenya + targeta) per a un nivell de seguretat molt més alt.

## 8. Autorització: criteris per autoritzar l'accés

- **Rols**: segons la funció (un auditor només necessita lectura).
- **Grups**: ex: a un institut, "alumnat" i "professorat" tenen permisos diferents.
- **Localització**: física (des d'on ets) o lògica (des de quina IP).
- **Hora d'accés**: ex: un servidor només accessible de 8h a 20h.

## 9. A la pràctica: sistemes UNIX/Linux

### 9.1. Llegint els permisos: rwx

```
-rw-rw-r--  1  joan  profes   seguretat.doc
```

- Usuari (joan): `rw-` → lectura i escriptura.
- Grup (profes): `rw-` → lectura i escriptura.
- Altres: `r--` → només lectura.

> 💡 r = lectura, w = escriptura, x = execució. Sense permís d'execució en un directori, ningú no hi pot entrar, encara que en tingui de lectura.

### 9.2. Tres ordres per gestionar permisos

| Ordre | Funció | Exemple |
|---|---|---|
| `chmod` | Canvia els permisos (rwx) | `chmod u=rwx freebsd.pdf` |
| `chown` | Canvia l'usuari propietari | `chown joan qualificacions.doc` |
| `chgrp` | Canvia el grup propietari | `chgrp profes qualificacions.doc` |

> ⚠️ Només l'administrador del sistema o el propietari del recurs poden fer aquests canvis.

## 10. Vigilància del sistema: registres, incidències i alarmes

- **Registres del SO**: intents d'accés, rendiment, dispositius usats, bloquejos d'usuaris...
- **Registres de seguretat**: antivirus, tallafocs, encaminadors, proxies...

> 💡 Un decrement molt accentuat del rendiment pot ser un indicador que hi ha un virus o un cavall de Troia treballant en segon pla.

### 10.1. Bones pràctiques

- Evitar tenir massa fonts de registres disperses.
- Sincronitzar l'hora de tots els sistemes.
- Utilitzar sempre el mateix format de dades.
- No ometre mai l'activitat dels comptes d'administrador.

> ⚠️ Un atacant intentarà esborrar les proves del seu pas: sense registres, mai sabrem que hi ha hagut un atac. Només l'administrador i el personal de seguretat haurien de poder veure, modificar o esborrar-los.

## Resum de l'apartat

- Autenticació (qui ets) i autorització (què pots fer) són conceptes diferents i complementaris.
- Una contrasenya robusta és llarga, variada i ben protegida.
- 3 factors d'autenticació: el que saps, el que tens, i el que ets/fas.
- Els permisos (rwx) i els registres del sistema són el dia a dia de la seguretat lògica.

## Per saber-ne més

- Institut Obert de Catalunya (IOC) — [Seguretat lògica](https://ioc.xtec.cat/materials/FP/Recursos/fp_smx_m06_/web/fp_smx_m06_htmlindex/WebContent/u1/a3/continguts.html), Unitat 1, apartat 3 (llicència CC BY-NC-SA, IOC 2011).

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
