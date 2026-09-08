# RA2 · AA3 — Còpies de seguretat

*La diferència entre un ensurt i un desastre.*

## 1. Per què cal fer còpies de seguretat

Les dades presents als ordinadors, tant particulars com empresarials, han d'estar assegurades davant d'accidents, atacs informàtics o errors humans. Les motivacions poden ser econòmiques (el cost d'una pèrdua de dades), legals (moltes legislacions obliguen a conservar determinada informació durant un període de temps, com els historials clínics o la documentació fiscal) o fins i tot sentimentals.

> ⚠️ Els sistemes d'alta disponibilitat com el RAID (vist a l'apartat [AA2](../AA2%20-%20Sistemes%20demmagatzematge/T02_Temari_Sistemes_emmagatzematge.md)) **només** protegeixen contra errors de maquinari. NO protegeixen contra esborrats accidentals, atacs de *ransomware* que xifren les dades, o modificacions no desitjades. Per a això calen còpies de seguretat de debò.

## 2. Tres conceptes que no s'han de confondre

- **Backup**: còpies de les dades amb l'objectiu de preservar-les i poder-les recuperar en cas de contingència.
- **Archiving**: emmagatzematge de dades per a períodes molt llargs (anys), habitualment per motius legals. No permet recuperació ràpida, però garanteix la conservació a llarg termini.
- **Imatges del sistema**: còpia del sistema operatiu amb les aplicacions instal·lades, per restaurar-lo ràpidament (no se centren en la informació d'usuari).

El backup assegura dos objectius fonamentals de la seguretat de la informació: la **integritat** i la **disponibilitat** de les dades.

## 3. Preguntes que cal respondre abans de començar

### 3.1. Què volem protegir?

No totes les dades tenen la mateixa importància ni són igual de recuperables. Decidir quines dades són crítiques és una tasca prèvia imprescindible: fer còpia d'absolutament tot pot ser inviable per cost i temps.

### 3.2. On farem les còpies?

| Tipus | Avantatges | Punt feble |
|---|---|---|
| **Locals** | Ràpides de fer i recuperar | Es perden en el mateix incident (incendi, robatori, inundació) |
| **Remotes en xarxa** | Centralitzen totes les còpies | Sovint a la mateixa ubicació física que l'original |
| **A Internet** | Separació física real | Cal bona connexió; qüestions legals i de confiança en el proveïdor |

> 📌 **Cas real:** l'incendi del centre de dades d'OVHcloud a Estrasburg (2021) va destruir informació de clients que només tenien còpies al mateix edifici.

### 3.3. La regla 3-2-1

El **US-CERT** (l'equip de resposta a emergències informàtiques dels EUA) va establir l'"estratègia 3-2-1", avui l'estàndard de referència del sector:

1. **3** còpies de les dades: l'original i **dues** còpies de seguretat.
2. **2** suports diferents (per exemple, cinta externa + servei a Internet).
3. **1** còpia en una ubicació remota (*backup offsite*): un altre edifici o el núvol.

D'aquesta manera, un incendi pot destruir l'original i la còpia local, però la còpia *offsite* —que no ha patit el desastre— continua disponible.

### 3.4. Amb quins dispositius?

| Suport | Punts forts / febles | Durada aprox. |
|---|---|---|
| Discos durs | Baix cost, bona relació preu/capacitat, fiabilitat limitada | 10-15 anys (offline) |
| Unitats SSD | Millor rendiment i fiabilitat, més cares, es degraden sense alimentació | ~1 any sense alimentar |
| Òptics (CD/DVD/BR) | Bons per a còpies immutables, cars i limitats en capacitat | ~20 anys |
| Cintes (LTO/DLT) | Lentes però molt duradores i fiables | ~50 anys |
| RDX | Velocitat de disc + cartutx extraïble | — |

### 3.5. Amb quina freqüència?

La freqüència determina la **finestra de recuperació** (*recovery window*): el temps màxim de dades que es podrien arribar a perdre. És un compromís entre disponibilitat necessària, cost i impacte en el negoci.

## 4. Com fer les còpies: tres estratègies

- **Còpia completa** (*full backup*): totes les dades. Lenta i ocupa molt espai, però la més fàcil de restaurar (un sol arxiu).
- **Còpia incremental**: només el que ha canviat des de l'última còpia (completa o incremental). Molt ràpida, però restauració lenta (cal tota la cadena).
- **Còpia diferencial**: només el que ha canviat des de l'última còpia **completa**. Restauració més senzilla que la incremental (només calen dos arxius).

| Volum de dades | Dades modificades/dia | Estratègia recomanada |
|---|---|---|
| < 50 GB | — | Completa |
| > 50 GB | < 4 GB | Diferencial (completa setmanal + diferencials diàries) |
| > 50 GB | > 4 GB | Incremental (completes més sovint + incrementals) |

> 💡 Els arxius de còpia se solen comprimir (.zip, .bz2...) per optimitzar l'espai i el temps de transferència.

## 5. Esquemes de rotació

Les còpies antigues no se substitueixen immediatament: es van rotant, per poder recuperar versions antigues si cal. Això dona un horitzó de recuperació més ampli i reparteix el desgast dels suports.

### 5.1. Grandfather-father-son (GFS)

- **Fill** (*son*): còpia incremental/diferencial diària, una cinta per dia de la setmana, reutilitzada cada setmana.
- **Pare** (*father*): còpia completa setmanal, una cinta per setmana del mes.
- **Avi** (*grandfather*): l'última completa del mes s'extreu de la rotació i es guarda com a còpia mensual (i, a l'any, com a arxiu a llarg termini).

### 5.2. Torres de Hanoi

Esquema més complex, basat en el trencaclosques matemàtic del mateix nom: màxima cobertura temporal amb el mínim de suports. Cada suport (A, B, C, D...) s'utilitza amb una freqüència que es duplica a cada lletra:

| Suport | Freqüència | Tipus de còpia habitual |
|---|---|---|
| A | Dies alterns | Incremental/diferencial |
| B | Cada 4 dies | Incremental/diferencial |
| C | Cada 8 dies | Completa |
| D | Cada 16 dies | Completa |

> ⚠️ Per la seva complexitat, recomanable només amb sistemes automatitzats de gestió de suports.

## 6. Comprovar les còpies de seguretat

Si el sistema de còpies falla, no es podran restaurar les dades quan calgui: cal fer proves de restauració periòdiques.

> 📌 **Cas real:** l'any 1998, Pixar va arribar a perdre 90 minuts de la pel·lícula *Toy Story 2* per un error al sistema de còpies. Només es va poder recuperar perquè, per sort, una treballadora en tenia una còpia personal al seu propi equip.

Aquestes proves també entrenen el personal per restaurar sota pressió real. Consell professional: en restaurar una base de dades, no sobreescriguis les dades existents — així pots comparar totes dues versions.

## 7. La política de còpies de seguretat

Defineix, a més de què/on/com/quan: els responsables, el temps de retenció, els procediments de restauració, com es protegeixen físicament les còpies (xifratge, armaris ignífugs, serveis com Iron Mountain per a l'arxiu a llarg termini), i el calendari de renovació i destrucció segura dels suports (veure [AA1](../AA1%20-%20Protegint%20les%20dades/T01_Temari_Protegint_les_dades.md)).

## 8. Programari de còpia de seguretat

| Sistema | Eines habituals |
|---|---|
| **Windows** | Còpia de seguretat de Windows (nativa, VHD); Cobian (gratuït); Acronis Backup (professional) |
| **Linux** | `tar` + `cron`; `rsync` (còpia remota eficient); Duplicity (backup xifrat); Areca Backup; Acronis |

## 9. Imatges de restauració del sistema

Una imatge conté l'estructura i el contingut complets d'un disc o partició: permet restaurar tot el sistema en pocs minuts, en lloc d'hores reinstal·lant-ho tot.

| Cas d'ús | Què copia | Destí |
|---|---|---|
| **Clonació de discos** | Només el contingut real (no l'espai lliure) | Un altre equip |
| **Imatge de disc** | Similar a la clonació, comprimible | Un fitxer de "respaldament" |
| **Imatge forense** | TOT, bloc a bloc, inclòs l'espai no usat + hash de verificació | Investigacions/peritatges |

**Eines**: Windows (eina nativa, Acronis True Image, Clonezilla, FOG) · Linux (Clonezilla, `dd`, PartImage) · Forense (FTK Imager, Guymager).

## Resum de l'apartat

- Backup, archiving i imatges del sistema resolen problemes diferents.
- La regla 3-2-1 (3 còpies, 2 suports, 1 *offsite*) és l'estàndard de referència.
- Completa, incremental i diferencial es trien segons el volum de dades i la freqüència de canvis.
- GFS i Torres de Hanoi organitzen la rotació de suports en el temps.
- Una còpia mai comprovada no és fiable: cal provar-ne la restauració periòdicament.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF2/AA3-CopiesSeguretat.md) (GitHub, SMX-0226SI) — Carlos Alonso Martínez, Escola Pia de Mataró (llicència CC-BY-SA-4.0).
- DataCenterDynamics — notícia sobre l'incendi del centre de dades d'OVHcloud a Estrasburg (2021).
- INCIBE — "Guía de copias de seguridad"; NAKIVO — "Backup Types Explained".
- Redstor — "Five of the biggest scare stories in data backup history" (cas Pixar).
- [clonezilla.org](https://clonezilla.org) — documentació oficial.

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
