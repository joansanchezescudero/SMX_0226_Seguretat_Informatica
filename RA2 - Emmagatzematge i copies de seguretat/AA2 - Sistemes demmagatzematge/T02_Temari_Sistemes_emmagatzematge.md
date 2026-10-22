# RA2 · AA2 — Sistemes d'emmagatzematge

*On viuen les dades, i com evitar que hi visquin soles.*

## 1. Medis d'emmagatzematge

La informació s'ha de guardar en medis persistents, és a dir, que conserven les dades encara que l'equip es desconnecti. Als propis ordinadors, els dos medis principals són:

- **Discos durs (HDD)**: tecnologia magnètica, més barata i amb més capacitat per euro, però més lenta i més sensible als cops.
- **Unitats SSD**: basades en semiconductors (memòria flaix), molt més ràpides i resistents als cops, però encara més cares per gigabyte.

A banda d'aquests medis interns, hi ha sistemes externs, considerats un "tercer nivell" d'emmagatzematge: discos durs extraïbles, pendrives, cintes magnètiques i DVD.

## 2. Paràmetres de l'emmagatzematge: rendiment, disponibilitat i accessibilitat

Abans de triar un sistema d'emmagatzematge, cal saber què li demanem. Hi ha tres paràmetres bàsics:

- **Rendiment:** que llegeixi i escrigui les dades ràpidament. Es mesura amb la latència, les IOPS i el throughput.
- **Disponibilitat:** que el sistema continuï funcionant encara que alguna peça falli. S'aconsegueix amb redundància (RAID, sistemes duplicats), protecció elèctrica (SAI) i monitoratge dels discos.
- **Accessibilitat:** que els usuaris puguin arribar a les dades quan les necessiten, de manera efectiva i segura: disc ben muntat, permisos correctes i sistema de fitxers sense errors. Un disc que funciona perfectament però està mal muntat no és accessible per a ningú.

### 2.1. Com es mesura el rendiment

- **Latència:** temps que triga el disc a respondre una operació. Es mesura en mil·lisegons (ms) o microsegons (µs): com menys, millor.
- **IOPS (operacions d'entrada/sortida per segon):** nombre d'operacions de lectura o escriptura que pot fer en un segon. És clau quan hi ha moltes peticions petites i aleatòries, com en un sistema operatiu o una base de dades.
- **Throughput (velocitat de transferència):** quantitat de dades transferides per segon, en MB/s o GB/s. És clau amb fitxers grans i seqüencials, com un vídeo o una còpia de seguretat.

> 💡 Un disc pot tenir un bon throughput i poques IOPS: copiar una pel·lícula (accés seqüencial) no costa el mateix que obrir milers de fitxers petits (accés aleatori). Per això un HDD pot copiar fitxers grans a una velocitat acceptable, però fa que l'arrencada del sistema operatiu sigui lenta.

### 2.2. HDD, SSD i NVMe en xifres

|  | HDD (7.200 rpm) | SSD SATA | SSD NVMe (M.2) | Llapis USB / SD |
|---|---|---|---|---|
| **Latència** | 5–10 ms | ≈ 0,1 ms | ≈ 0,02–0,1 ms | Molt variable |
| **IOPS (aleatòries)** | 75–200 | Desenes de milers | Centenars de milers | Centenars o pocs milers |
| **Throughput** | 100–250 MB/s | Fins a ≈ 550 MB/s | 3.000–14.000 MB/s | 20–400 MB/s |
| **Connexió** | SATA | SATA | PCIe | USB o lector de targetes |
| **Cost per GB** | El més baix | Mitjà | Mitjà-alt | Variable |
| **Ús típic** | Gran capacitat, arxiu i còpies | Equips d'oficina | Servidors i equips exigents | Transport de dades |

*Valors orientatius (ordre de magnitud): cada model concret pot variar. Els SSD SATA estan limitats per la connexió SATA (≈ 600 MB/s); els NVMe es connecten directament al bus PCIe i per això són molt més ràpids.*

### 2.3. Detectar anomalies: SMART

SMART (Self-Monitoring, Analysis and Reporting Technology) és un sistema integrat als discos HDD, SSD i NVMe que registra indicadors de salut del disc: sectors defectuosos reassignats, errors de lectura, temperatura, hores d'ús o, en els SSD, el desgast de les cel·les. Si aquests valors empitjoren, cal substituir el disc ABANS que falli i es perdin dades.

A Ubuntu es pot consultar amb l'eina `smartctl` (cal instal·lar el paquet `smartmontools`): `sudo smartctl -H /dev/sda` mostra l'estat de salut general del disc i `sudo smartctl -a /dev/sda` en mostra tots els indicadors. A l'escriptori, l'aplicació Discos també mostra les dades SMART de cada disc.

## 3. La redundància: no dependre mai d'un sol disc

Duplicar la informació permet evitar-ne la pèrdua davant l'avaria d'un disc. Aquesta duplicació es pot implementar amb diverses tècniques, que sovint es combinen per evitar un únic punt de fallada (*single point of failure*):

- **RAID** (*Redundant Array of Independent Disks*): combina diverses unitats d'emmagatzematge en una sola unitat lògica. És redundància **local**, dins del mateix equip.
- **Sistemes d'emmagatzematge en xarxa**: proporcionen redundància a nivell de xarxa local (més d'un servidor o cabina de discos). Internament, ja fan servir RAID.
- **Serveis de núvol**: com Dropbox, Google Drive o OneDrive, que mantenen la informació "duplicada" a Internet.

## 4. RAID: Redundant Array of Independent Disks

El RAID combina diversos discos o unitats SSD de manera distribuïda. Segons el nivell triat, s'obté:

- **Tolerància a fallades**: si un disc falla, la informació no es perd.
- **Millora del rendiment**: la informació es distribueix entre diversos discos i es pot llegir/escriure en paral·lel.

Es pot implementar amb **maquinari** (controladores dedicades, més ràpid, sol permetre *hot swap*) o amb **programari** (el mateix sistema operatiu, més barat però amb rendiment inferior i només els nivells més bàsics).

### 4.1. RAID 0 — Data striping

Distribueix la informació entre dos o més discos **sense cap redundància**. Com que s'escriu als dos discos alhora, el rendiment augmenta. Si falla un sol disc, es perd TOTA la informació de l'array.

```mermaid
---
title: RAID 0
---
flowchart TB
    subgraph Disk0 ["disc 1"]
        direction LR
        A1["A2"]
        A3["A4"]
        A5["A6"]
        A7["A8"]
    end
    subgraph Disk1 ["disc 0"]
        direction LR
        A2["A1"]
        A4["A3"]
        A6["A5"]
        A8["A7"]
    end
    classDef block fill:#FFD54F,stroke:#FFB300,stroke-width:2px,color:#000,font-weight:bold,font-size:18px;
    class A1,A2,A3,A4,A5,A6,A7,A8 block;
    style Disk0 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk1 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
```

### 4.2. RAID 1 — Mirror

Duplica exactament la mateixa informació entre dos discos. Si un falla, l'altre ja conté tota la informació. Lectura ràpida, escriptura equivalent a un sol disc. Es perd la meitat de la capacitat total.

```mermaid
---
title: RAID 1
---
flowchart TB
    subgraph Disk0 ["disc 1"]
        direction LR
        A1["A1"]
        A3["A2"]
        A5["A3"]
        A7["A4"]
    end
    subgraph Disk1 ["disc 0"]
        direction LR
        A2["A1"]
        A4["A2"]
        A6["A3"]
        A8["A4"]
    end
    classDef block fill:#FFD54F,stroke:#FFB300,stroke-width:2px,color:#000,font-weight:bold,font-size:18px;
    class A1,A2,A3,A4,A5,A6,A7,A8 block;
    style Disk0 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk1 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
```

### 4.3. RAID 5 — Paritat distribuïda

Divideix les dades a nivell de bloc i distribueix la informació de **paritat** entre tots els discos (mínim 3). Redundància més econòmica que el mirall: només es "perd" l'equivalent a un disc. Suporta la pèrdua d'**un** disc.

```mermaid
---
title: RAID 5
---
flowchart TD
    subgraph Disk2 ["disc 2"]
        direction LR
        A1["P"]
        A2["A4"]
        A3["A6"]
        A4["P"]
    end
    subgraph Disk1 ["disc 1"]
        direction LR
        A5["A2"]
        A6["A3"]
        A7["P"]
        A8["A8"]
    end
    subgraph Disk0 ["disc 0"]
        direction LR
        A9["A1"]
        A10["P"]
        A11["A5"]
        A12["A7"]
    end
    classDef block fill:#FFD54F,stroke:#FFB300,stroke-width:2px,color:#000,font-weight:bold,font-size:18px;
    class A1,A2,A3,A4,A5,A6,A7,A8,A9,A10,A11,A12 block;
    style Disk0 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk1 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk2 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
```

### 4.4. RAID 6 — Doble paritat

Igual que el RAID 5, però amb una **segona** banda de paritat: suporta la pèrdua de **dos** discos simultàniament. Calen un mínim de quatre unitats.

```mermaid
---
title: RAID 6
---
flowchart TD
    subgraph Disk0 ["disc 3"]
        direction LR
        A1["P2"]
        A2["A4"]
        A3["A6"]
        A4["P1"]
    end
    subgraph Disk1 ["disc 2"]
        direction LR
        A5["P1"]
        A6["P1"]
        A7["A5"]
        A8["A8"]
    end
    subgraph Disk2 ["disc 1"]
        direction LR
        A9["A2"]
        A10["P1"]
        A11["P2"]
        A12["A7"]
    end
    subgraph Disk3 ["disc 0"]
        direction LR
        A13["A1"]
        A14["A3"]
        A15["P1"]
        A16["P2"]
    end
    classDef block fill:#FFD54F,stroke:#FFB300,stroke-width:2px,color:#000,font-weight:bold,font-size:18px;
    class A1,A2,A3,A4,A5,A6,A7,A8,A9,A10,A11,A12,A13,A14,A15,A16 block;
    style Disk0 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk1 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk2 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk3 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
```

### 4.5. RAID aniuat (RAID 10)

Combina RAID 1 i RAID 0 (mínim 4 unitats): primer es formen parelles en mirall, i després la informació es distribueix entre les parelles. Ràpid i segur, però només es pot perdre un disc per cada conjunt en mirall.

```mermaid
---
title: RAID 10
---
flowchart TD
    subgraph Disk0 ["disc 3"]
        direction LR
        A1["A2"]
        A2["A4"]
        A3["A6"]
        A4["A8"]
    end
    subgraph Disk1 ["disc 2"]
        direction LR
        A5["A1"]
        A6["A3"]
        A7["A5"]
        A8["A7"]
    end
    subgraph Disk2 ["disc 1"]
        direction LR
        A9["A2"]
        A10["A4"]
        A11["A6"]
        A12["A8"]
    end
    subgraph Disk3 ["disc 0"]
        direction LR
        A13["A1"]
        A14["A3"]
        A15["A5"]
        A16["A7"]
    end
    classDef block fill:#FFD54F,stroke:#FFB300,stroke-width:2px,color:#000,font-weight:bold,font-size:18px;
    class A1,A2,A3,A4,A5,A6,A7,A8,A9,A10,A11,A12,A13,A14,A15,A16 block;
    style Disk0 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk1 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk2 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
    style Disk3 fill:#F5F5F5,stroke:#9E9E9E,stroke-width:2px;
```

Altres combinacions són possibles, com el RAID 50 (RAID 5+0) o el RAID 60 (RAID 6+0), tot i que són menys habituals.

![Comparativa de velocitat i fiabilitat dels nivells de RAID](media/RAID.gif)

*[Comparativa visual dels principals tipus de RAID](https://www.instagram.com/reel/DdtTpMwCkEd/?stkn=MmU0eTB6bjNkMTRr).*

### 4.6. Comparativa de nivells de RAID

| Característica | RAID 0 | RAID 1 | RAID 5 | RAID 6 | RAID 10 |
|---|---|---|---|---|---|
| Nombre mínim de discos | 2 | 2 | 3 | 4 | 4 |
| Redundància | No | 1 disc | 1 disc | 2 discos | 1 disc |
| Capacitat utilitzable | 100% | 50% | 1 disc | 2 discos | 50% |
| Velocitat de lectura | Alta | Alta | Baixa | Baixa | Alta |
| Velocitat d'escriptura | Alta | Mitjana | Baixa | Baixa | Mitjana |
| Cost | Baix | Alt | Alt | Molt alt | Alt |

*Font: [www.raid-calculator.com](https://www.raid-calculator.com/raid-types-reference.aspx)*

## 5. Sistemes d'emmagatzematge en xarxa

En un entorn empresarial, les dades no haurien d'estar només a les estacions de treball individuals. Centralitzar-les evita la inconsistència de la informació i facilita fer còpies de seguretat centralitzades. Hi ha tres grans sistemes, de menys a més complexitat: **DAS**, **NAS** i **SAN**.

### 5.1. DAS (Direct Attached Storage)

Servidors que exposen carpetes compartides a la xarxa (SMB o NFS). Pot ser tan bàsic com un servidor normal, o tan avançat com un servidor amb cabines de discos dedicades (*hot-plug*). Inconvenients: rendiment baix si el servidor no és dedicat, disponibilitat limitada, i possible coll d'ampolla de xarxa.

![Servidor HP ProLiant DL380 amb cabina de discos dedicada](media/hp-proliant.jpg)

*[Servidor HP ProLiant DL380 Gen9](https://support.hpe.com/hpesc/public/docDisplay?docId=a00019684en_us&docLocale=en_US), un exemple real d'equip usat com a DAS.*

![Esquema d'un sistema DAS: dos servidors, cadascun amb el seu propi emmagatzematge](media/das.png)

*En un DAS, cada servidor exposa el seu propi emmagatzematge directament a la xarxa.*

### 5.2. NAS (Network Attached Storage)

Dispositius dedicats exclusivament a l'emmagatzematge en xarxa: petits servidors amb sistema operatiu especialitzat i interfície web de gestió. Molt aptes per al mercat domèstic i la petita empresa. Limitacions de CPU/RAM i possible coll d'ampolla de xarxa.

![Esquema d'un NAS i un dispositiu NAS real de D-Link](media/nas.png)

*Un NAS connecta diversos clients a través d'un switch; a la dreta, [un dispositiu NAS real](https://www.dlink.com/en/products/nas) amb diverses badies de discos.*

### 5.3. SAN (Storage Area Network)

Xarxes dedicades exclusivament a l'emmagatzematge, molt més complexes i costoses que un NAS, però amb rendiment molt superior. Utilitzen protocols optimitzats (Fibre Channel, iSCSI, FCoE) diferents dels de la LAN convencional, i requereixen switches i targetes de xarxa específiques. Els servidors s'organitzen en clústers: redundància a nivell de disc (RAID) **i** a nivell de servidor complet.

> 💡 A una escala més petita, es pot muntar un clúster d'emmagatzematge amb servidors normals de la LAN (DAS), amb tecnologies com Windows Server DFS o GlusterFS (Linux), sense la infraestructura cara d'una SAN completa.

![Cabines de discos muntades en rack, típiques d'un sistema SAN](media/cabina_de_discos.png)

*[Cabines de discos dedicades](https://www.infores.es/productos/Almacenamiento-SAN.html), com les que s'utilitzen en un SAN.*

## 6. Serveis de núvol

Pagament per ús en lloc d'infraestructura pròpia; fins i tot amb plans gratuïts en entorn domèstic (Google Drive ofereix 15 GB a qualsevol compte de Gmail). Permeten accedir a la informació des de qualsevol lloc, amb un cost inicial baix. Cal valorar-ne, però: la velocitat de sincronització amb fitxers grans, la pèrdua de control complet sobre les dades, i el compliment legal (RGPD) quan hi ha dades personals.

### 6.1. Local o núvol?

|  | Local (on-premise) | Núvol |
|---|---|---|
| **Cost** | Inversió inicial alta + manteniment | Pagament per ús |
| **Escalabilitat** | Limitada al maquinari propi | Pràcticament il·limitada |
| **Accés** | Xarxa local o VPN | Des de qualsevol lloc amb Internet |
| **Disponibilitat** | Depèn dels equips propis | Molt alta (centres de dades redundants) |
| **Control i seguretat** | Control total, però responsabilitat total | Delegats al proveïdor |
| **Depèn de** | Maquinari i personal tècnic | Connexió a Internet i proveïdor |

### 6.2. El model híbrid

Moltes empreses combinen tots dos models: guarden en local les dades sensibles i les que necessiten més velocitat, i fan servir el núvol per a les còpies de seguretat fora de l'empresa i per créixer quan cal (per exemple, en moments de més feina o per col·laborar amb personal que treballa a distància).

## Resum de l'apartat

- Els tres paràmetres bàsics de l'emmagatzematge són el rendiment (latència, IOPS, throughput), la disponibilitat i l'accessibilitat.
- HDD < SSD SATA < NVMe en rendiment; SMART permet detectar un disc que s'està degradant abans que falli.
- La redundància es pot aconseguir amb RAID (local), emmagatzematge en xarxa, o serveis de núvol.
- RAID 0 dona velocitat sense redundància; RAID 1 dona redundància total a costa de la meitat de la capacitat; RAID 5/6 ofereixen un equilibri amb paritat; RAID 10 combina velocitat i redundància amb més discos.
- DAS < NAS < SAN: complexitat i cost creixents a canvi de més rendiment, disponibilitat i escalabilitat.
- Els serveis de núvol són còmodes i barats, però cal valorar-ne velocitat, control i compliment legal.
- Local i núvol tenen avantatges diferents; el model híbrid els combina.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF2/AA2-SistemesEmmagatzematge.md) (GitHub, SMX-0226SI) — Carlos Alonso Martínez, Escola Pia de Mataró (llicència CC-BY-SA-4.0).
- [raid-calculator.com](https://www.raid-calculator.com/raid-types-reference.aspx) — "RAID Types Reference".
- NASEROS (YouTube) — ["Tipos de RAID. En qué se diferencian y cuales son los mejores"](https://youtu.be/x8MXkvgeD0w?si=PxmhBAzU1JfD0yvy).
- Pau Tomé (YouTube) — ["RAID en Windows Server"](https://youtu.be/3XO-GrcyxHg?si=gzZ1YTr-ovlSkkI4).
- IBM — ["What is a storage area network (SAN)?"](https://www.ibm.com/think/topics/storage-area-network)

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
