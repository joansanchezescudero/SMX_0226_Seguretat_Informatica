# RA2 · AA1 — Protegint les dades

*Els programes es reinstal·len; les dades, si es perden, no tornen.*

## 1. Les dades com a actiu

La informació és un dels actius més valuosos de qualsevol empresa. Si un disc dur s'avaria, els programes es poden tornar a instal·lar sense gaire dificultat, però les dades, si es perden, normalment no es poden recuperar de cap manera. Per aquest motiu, les dades també són un dels objectius més cercats pels delinqüents: el segrest de dades (*ransomware*), un programari maliciós que xifra la informació d'una víctima i en demana un rescat econòmic per desxifrar-la, s'ha convertit en una de les principals amenaces per a les empreses d'avui dia.

Davant d'aquest escenari, disposem de dues estratègies complementàries —no excloents— per protegir la informació:

- **Continuïtat de negoci**: protegim les dades de manera que, davant d'un incident, es pugui seguir treballant sense pèrdua de dades.
- **Recuperació de desastres**: protegim les dades de manera que, davant d'un incident, es pugui recuperar la informació i tornar a l'estat anterior.

> 💡 **Important:** la continuïtat de negoci evita la interrupció mentre passa l'incident; la recuperació de desastres actua després, un cop l'incident ja ha causat una pèrdua.

## 2. Continuïtat de negoci: l'alta disponibilitat

La clau per seguir operant i ser resistents davant d'un incident és l'**alta disponibilitat**: disposar d'una infraestructura que garanteixi l'accés a les dades malgrat es produeixin incidents. En altres paraules, estem parlant de sistemes tolerants a fallades.

Per aconseguir aquesta tolerància a fallades necessitem **redundància**, és a dir, duplicació de components. Hi ha dues estratègies principals:

### 2.1. Servidors redundants

Consisteix a tenir més d'un servidor amb la mateixa informació, encara que estiguin situats a la mateixa ubicació física. Es pot implantar dins la pròpia organització, o bé fent servir serveis de núvol: pràcticament tots els proveïdors de *cloud* ofereixen la possibilitat de tenir servidors redundants, tant dins el mateix centre de dades com en ubicacions geogràfiques diferents (per exemple, un servidor a Madrid i un altre a Frankfurt).

### 2.2. Sistemes d'emmagatzematge redundants

Consisteix a tenir més d'un sistema d'emmagatzematge amb la mateixa informació. Aquesta és l'estratègia que **sempre** s'aplica en qualsevol sistema informàtic seriós: sistemes com el RAID (que estudiarem a l'apartat AA2) permeten que, davant l'avaria d'un disc o d'un SSD, el sistema continuï funcionant sense pèrdua de dades.

> ⚠️ La redundància és cara. Cal analitzar quin nivell d'alta disponibilitat necessita realment cada cas concret: no té sentit invertir en la mateixa redundància per a l'ordinador d'un becari que per al servidor de facturació d'una empresa.

## 3. Recuperació de desastres

Quan un incident ja ha provocat la pèrdua de les dades o del seu accés, l'objectiu passa a ser recuperar el funcionament normal en el mínim temps possible. Ens trobem amb dos escenaris diferenciats:

- **Recuperació dels sistemes**: fent servir imatges de restauració (còpies exactes del sistema operatiu i les aplicacions instal·lades), es pot recuperar un equip complet en un temps molt reduït, sense haver de reinstal·lar-ho tot des de zero.
- **Recuperació de les dades**: fent servir còpies de seguretat (*backup*), es poden recuperar els documents, bases de dades i altra informació generada per l'organització.

Aprofundirem en aquests dos mecanismes a l'apartat [AA3 · Còpies de seguretat](../AA3%20-%20Copies%20de%20seguretat/T03_Temari_Copies_de_seguretat.md).

## 4. Protecció de les dades: més enllà de la redundància

La protecció de les dades no s'acaba amb la redundància. Implica també la seguretat física dels equips i el **xifratge** de la informació, de manera que, si les dades són robades, no es puguin llegir sense la clau corresponent.

Hi ha, a més, un aspecte sovint oblidat: gestionar el **cicle de vida de les dades**. És a dir, com es creen, com s'emmagatzemen, com s'utilitzen i, finalment, com es destrueixen els suports físics quan arriben al final de la seva vida útil.

> 📌 **Cas real:** un estudi realitzat el 2019 (PCMag, *"Many Used Hard Drives Sold on eBay Still Contain Leftover Data"*) va descobrir que **3 de cada 5** discos durs de segona mà venuts a eBay encara contenien dades personals i confidencials dels seus antics propietaris.

## 5. Com destruir les dades de manera segura

| Tècnica | Com funciona | Permet reutilitzar el suport? |
|---|---|---|
| **Destrucció física** | Trituradores o perforadores destrueixen físicament el suport | No |
| **Desmagnetització** | Només efectiva en suports magnètics (discos, cintes) | No |
| **Sobrescriptura** | Sobreescriu la informació amb dades aleatòries; funciona en suports magnètics i flaix (SSD, USB, SD) | Sí |

Una de les estratègies de sobrescriptura més conegudes és la que recomana el Departament de Defensa dels Estats Units (estàndard **DoD 5220.22-M**): sobreescriure una vegada amb zeros, sobreescriure tres vegades amb dades aleatòries, i finalment sobreescriure una vegada amb uns.

> ⚠️ Un simple "Esborra" o un format ràpid del disc **NO** elimina realment les dades: només marca l'espai com a disponible per ser reutilitzat, però la informació original hi continua sent físicament fins que s'hi escriu a sobre.

## 6. Un risc sovint oblidat: impressores i fotocopiadores digitals

Les impressores i fotocopiadores digitals solen tenir memòria interna (sovint un disc dur) on queden emmagatzemades còpies dels documents que s'hi han imprès, escanejat o fotocopiat, de vegades durant mesos o anys.

El reportatge *"Copy Machines, a Security Risk?"* (CBS News) va destapar precisament aquest problema: fotocopiadores donades de baixa o revenudes de segona mà que conservaven milers de documents confidencials sense que ningú n'hagués estat conscient. Cal tenir en compte aquests dispositius —i qualsevol altre amb memòria interna— a l'hora de dissenyar una política de destrucció de dades.

## Resum de l'apartat

- Continuïtat de negoci (seguir operant durant l'incident) i recuperació de desastres (recuperar-se després) són estratègies **complementàries**.
- L'alta disponibilitat es construeix amb redundància: servidors redundants i, sobretot, sistemes d'emmagatzematge redundants.
- La recuperació de desastres es divideix en recuperació de sistemes (imatges) i recuperació de dades (còpies de seguretat).
- El cicle de vida de les dades acaba amb una destrucció segura: física, per desmagnetització, o per sobrescriptura (DoD 5220.22-M).
- Qualsevol dispositiu amb memòria interna —no només els discos dels ordinadors— és un risc potencial de fuita de dades.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF2/AA1-ProtegintDades.md) (GitHub, SMX-0226SI) — Carlos Alonso Martínez, Escola Pia de Mataró (llicència CC-BY-SA-4.0).
- IONOS Digital Guide — "La importancia de contar con un disaster recovery plan".
- PCMag — "Many Used Hard Drives Sold on eBay Still Contain Leftover Data" (2019).
- CBS News — "Copy Machines, a Security Risk?" (reportatge, disponible a YouTube).

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
