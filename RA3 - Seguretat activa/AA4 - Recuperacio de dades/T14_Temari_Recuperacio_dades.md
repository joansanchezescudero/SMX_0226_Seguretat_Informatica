# RA3 · AA4 — Recuperació de dades

*Quan la prevenció ha fallat: l'últim recurs per recuperar la informació.*

## 1. Introducció

La recuperació de dades (Data Recovery) és el conjunt de tècniques, eines i procediments per accedir, extreure i restaurar informació de dispositius d'emmagatzematge quan ha estat inaccessible, corrompuda, esborrada o danyada.

> ⚠️ Encara que la prevenció (còpies de seguretat, RAID) és la primera línia de defensa, la recuperació lògica és el darrer recurs per restablir la **Disponibilitat** i la **Integritat** dins el triat CIA de la seguretat.

## 2. Causes de la pèrdua de dades

- **Errors humans**: esborrat accidental, format incorrecte, desconnexió durant una escriptura.
- **Atacs maliciosos**: ransomware (xifra/destrueix MFT/GPT), wipers, modificació del MBR/VBR.
- **Errors de sistema**: talls de tensió mentre s'actualitzen metadades (estat "dirty").
- **Degradació física**: desgast de cel·les flaix, sectors defectuosos, danys de firmware.

Es classifica la pèrdua en avaries **físiques** (suport danyat) o **lògiques** (sistema de fitxers corromput, maquinari intacte).

## 3. Avaries físiques

El suport o el firmware estan danyats. Requereix un entorn controlat (sala blanca). Empreses especialitzades: Recovery Labs, Ontrack, DriveSavers, Gillware.

## 4. Avaries lògiques

El maquinari funciona, però les dades són inaccessibles per errors al sistema de fitxers, la taula de particions, o accions malicioses.

### 4.1. Protocol d'actuació

- **No escriure MAI** sobre el suport afectat: qualsevol escriptura pot sobreescriure les dades a recuperar.
- **Treballar sobre una còpia** (imatge) del suport, no sobre l'original — essencial en peritatges forenses.

## 5. Tècniques de recuperació

### 5.1. Undelete (basada en el sistema de fitxers)

En esborrar un fitxer, el SO NO elimina el contingut real: només marca l'entrada com a "lliure". Si els sectors no s'han sobreescrit, es pot recuperar escanejant la taula d'assignació.

### 5.2. Carving de fitxers (raw recovery)

S'utilitza quan la taula de particions o les metadades estan corruptes: s'analitza el disc sector per sector buscant **magic numbers**.

| Format | Capçalera | Peu |
|---|---|---|
| PDF | `%PDF` (45 50 44 46) | — |
| JPEG | FF D8 FF E0 | FF D9 |
| ZIP/DOCX/XLSX | `PK` (50 4B 03 04) | — |

> 💡 Als sistemes *nix, l'ordre `file` consulta aquests magic numbers per identificar el tipus d'un fitxer.

Inconvenient: no recupera noms de fitxer ni estructura de carpetes; en sistemes molt fragmentats, els fitxers poden quedar incomplets.

### 5.3. Recuperació de la taula de particions

Restaura l'MBR o la GPT si s'han corromput: es busquen els Boot Sectors/Superblocks i es reescriu la taula original, fent el volum accessible sense restaurar fitxer per fitxer.

## 6. Eines de recuperació de dades

| Eina | Interfície | Ús |
|---|---|---|
| dd / ddrescue | CLI | Còpia de disc sector per sector. |
| FTK Imager | CLI | Creació d'imatges forenses. |
| TestDisk | CLI/TUI | Recuperació de particions. |
| PhotoRec | CLI/TUI | Carving de fitxers. |
| Foremost / Scalpel | CLI | Carving de fitxers. |
| Recuva | GUI (Windows) | Recuperació de fitxers. |
| Autopsy | GUI | Anàlisi forense digital avançada. |

## 7. Pràctica: carving amb Foremost

```
foremost -t jpg,pdf -i disc_danyat.img -o recuperat/
```

Escaneja una imatge sector per sector buscant capçaleres de JPEG i PDF, i en recupera el contingut a la carpeta de sortida, sense necessitar cap sistema de fitxers vàlid. L'informe `audit.txt` indica el nombre de fitxers trobats, la mida i l'offset de cadascun.

## 8. Exemple d'actuació pas a pas

1. Crear una imatge del dispositiu amb `dd`, `ddrescue` o FTK Imager.
2. Executar TestDisk sobre la imatge, per recuperar particions eliminades o corrompudes.
3. Si les particions no es poden recuperar, executar PhotoRec o Foremost per fer carving de fitxers.

## Resum de l'apartat

- Avaries físiques → recursos professionals; avaries lògiques → eines de programari.
- Regla d'or: mai escriure sobre l'original, treballar sempre sobre una còpia.
- Tres tècniques: undelete, carving (magic numbers) i recuperació de la taula de particions.
- Flux habitual: imatge → TestDisk (particions) → PhotoRec/Foremost (carving) si cal.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF3/AA4-RecuperacioDades.md) (GitHub, SMX-0226SI) — llicència CC-BY-SA-4.0.
- IBM Think — "¿Qué es la recuperación de datos?".
- [TestDisk & PhotoRec](https://www.cgsecurity.org) — documentació oficial.
- Foremost — documentació oficial.

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
