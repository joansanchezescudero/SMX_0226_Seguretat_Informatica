# 0226 · Seguretat Informàtica — CFGM SMX2

Material del mòdul professional 0226 (Seguretat Informàtica), CFGM Sistemes Microinformàtics i Xarxes, 2n curs — Institut Puig Castellar.

Estructura per Resultat d'Aprenentatge (RA) i, dins de cada RA, per activitat d'aprenentatge (AA). RA2-RA5 segueixen el desglossament del repositori [Materials de SMX-0226SI](https://github.com/SMX-0226SI/Materials) (Carlos Alonso Martínez, Escola Pia de Mataró, CC-BY-SA-4.0), adaptat a l'estil i plantilla propis del centre. RA1 es basa en el material de l'[Institut Obert de Catalunya (IOC)](https://ioc.xtec.cat/materials/FP/Recursos/fp_smx_m06_/web/fp_smx_m06_htmlindex/WebContent/u1/introduccio.html) (llicència CC BY-NC-SA, IOC 2011), amb les diapositives de teoria elaborades directament pel professor.

Cada AA inclou:
- Una presentació de teoria (`.pptx`).
- Una pràctica guiada d'exercicis (`.docx`), amb captures de pantalla reals quan la pràctica implica programari.
- Un temari d'estudi (`.md`, amb versió `.docx` per imprimir/editar offline), per a l'estudi autònom de l'alumnat. El `.md` es pot llegir directament des de GitHub (amb diagrames inclosos).

Per a RA2 (NF2), a més, hi ha dues pràctiques complementàries per AA (A06/A07) basades en els projectes reals "EverPia" i "EverPia III" (repositoris `NF2AA2-GestioDiscos` i `NF2AA3-CopiesSeguretat` de SMX-0226SI), amb captures de pantalla reals fetes expressament per a aquesta guia. Per a RA1-AA3 (Seguretat lògica), hi ha també una pràctica complementària (A04) d'administració real d'usuaris, grups i ACL a Ubuntu.

Les hores de cada RA s'han calibrat per aproximar-se al màxim a la distribució horària oficial del mòdul (programació DOGC): quan el material de referència ("Materials") no cobria prou hores per si sol, s'ha ampliat el nombre o la profunditat dels AA (és el cas de RA4 i RA5).

## Contingut

- **RA1 · Seguretat passiva** (24h)
  - [AA1 · Seguretat passiva](<RA1 - Seguretat passiva/AA1 - Seguretat passiva/T04_Temari_Seguretat_Passiva.md>)
  - [AA2 · Sistemes d'alimentació ininterrompuda](<RA1 - Seguretat passiva/AA2 - Sistemes alimentacio ininterrompuda/T05_Temari_SAI.md>)
  - [AA3 · Seguretat lògica](<RA1 - Seguretat passiva/AA3 - Seguretat logica/T06_Temari_Seguretat_Logica.md>)

- **RA2 · Emmagatzematge i còpies de seguretat** (26h)
  - [AA1 · Protegint les dades](<RA2 - Emmagatzematge i copies de seguretat/AA1 - Protegint les dades/T01_Temari_Protegint_les_dades.md>)
  - [AA2 · Sistemes d'emmagatzematge](<RA2 - Emmagatzematge i copies de seguretat/AA2 - Sistemes demmagatzematge/T02_Temari_Sistemes_emmagatzematge.md>)
  - [AA3 · Còpies de seguretat](<RA2 - Emmagatzematge i copies de seguretat/AA3 - Copies de seguretat/T03_Temari_Copies_de_seguretat.md>)

- **RA3 · Seguretat activa** (24h)
  - [AA1 · Malware](<RA3 - Seguretat activa/AA1 - Malware/T11_Temari_Malware.md>)
  - [AA2 · Vulnerabilitats](<RA3 - Seguretat activa/AA2 - Vulnerabilitats/T12_Temari_Vulnerabilitats.md>)
  - [AA3 · Criptografia](<RA3 - Seguretat activa/AA3 - Criptografia/T13_Temari_Criptografia.md>)
  - [AA4 · Recuperació de dades](<RA3 - Seguretat activa/AA4 - Recuperacio de dades/T14_Temari_Recuperacio_dades.md>)

- **RA4 · Seguretat en xarxa** (38h)
  - [AA1 · Enginyeria social i phishing](<RA4 - Seguretat en xarxa/AA1 - Enginyeria social i phishing/T15_Temari_Enginyeria_social_phishing.md>)
  - [AA2 · Inventari i monitorització de la xarxa](<RA4 - Seguretat en xarxa/AA2 - Inventari i monitoritzacio/T16_Temari_Inventari_Monitoritzacio.md>)
  - [AA3 · Signatura digital](<RA4 - Seguretat en xarxa/AA3 - Signatura digital/T17_Temari_Signatura_digital.md>)
  - [AA4 · Tallafocs](<RA4 - Seguretat en xarxa/AA4 - Tallafocs/T18_Temari_Tallafocs.md>)

- **RA5 · Legislació i normativa** (20h)
  - [AA1 · Protecció de dades (RGPD/LOPD-GDD)](<RA5 - Legislacio i normativa/AA1 - Proteccio de dades/T08_Temari_Proteccio_dades.md>)
  - [AA2 · LSSI (comerç electrònic i serveis d'Internet)](<RA5 - Legislacio i normativa/AA2 - LSSI/T09_Temari_LSSI.md>)
  - [AA3 · Propietat intel·lectual i llicències (LPI)](<RA5 - Legislacio i normativa/AA3 - Propietat intellectual i llicencies/T10_Temari_Propietat_intellectual.md>)

**Curs complet: RA1-RA5 (132h totals).**

Les pràctiques de RA3-AA2/AA3/AA4 (A12, A13, A14) i RA4-AA2/AA3/AA4 (A16, A17, A18) inclouen captures de terminal 100% reals: nmap, OpenSSL (xifrat AES, claus RSA, signatura digital, certificats X.509), foremost (recuperació de dades), tshark (captura de trànsit) i UFW (tallafocs), totes executades expressament per elaborar cada guia.

## Quadre d'hores per RA

| RA | Contingut | Hores oficials | Hores del material de referència | Ajust aplicat |
|---|---|---|---|---|
| RA1 | Seguretat passiva | 24h | — | Material propi (IOC + professor); coincideix amb els 3 apartats oficials |
| RA2 | Emmagatzematge i còpies de seguretat | 26h | ~26h | Cap (coincideix) |
| RA3 | Seguretat activa | 24h | 24h | Cap (coincideix exactament) |
| RA4 | Seguretat en xarxa | 38h | ~32h | +1 AA ampliat en profunditat (pràctiques amb més abast) per cobrir el gap de 6h |
| RA5 | Legislació i normativa | 20h | ~12h | +1 AA nou: "Propietat intel·lectual i llicències (LPI)", per cobrir el gap de 8h |
