# RA1 · AA1 — Seguretat passiva

*Protegint allò físic: equips, sales i persones.*

## 1. La seguretat informàtica, una disciplina holística

Quan es parla de seguretat informàtica, la majoria de gent pensa en tallafocs, antivirus o detectors d'intrusions: mesures de programari. Però la seguretat informàtica és una disciplina **holística**, que engloba tot allò que ajuda a reduir i controlar els riscos del dia a dia d'una empresa, incloent-hi un vessant que sovint s'oblida: la seguretat física dels equips, la continuïtat elèctrica i el control d'accés a les sales.

Aquesta unitat treballa precisament aquesta base física, sobre la qual es construeix tota la resta de mesures de seguretat.

> 📌 **Cas real:** segons l'FBI, el robatori d'ordinadors portàtils i de butxaca s'ha incrementat exponencialment en els darrers anys. Quan el propietari és un alt càrrec d'una empresa, la pèrdua del dispositiu pot suposar un risc de seguretat molt important.

## 2. De la sala sencera a la butxaca

Als anys 1960-1970, un ordinador ocupava una sala sencera: només grans corporacions en tenien, i poca gent hi podia accedir físicament. Avui, portem l'equivalent a mil ordinadors a la butxaca, i s'hi pot accedir sense fils, des de fora del mateix edifici.

## 3. Seguretat física vs. seguretat lògica

| | Protegeix | Exemples |
|---|---|---|
| **Seguretat FÍSICA** | El maquinari (sales, cablejat, dispositius) | Panys, tanques, SAI, extintors |
| **Seguretat LÒGICA** | La informació (programari, contrasenyes, permisos) | Xifratge, antivirus, còpies de seguretat |

> ⚠️ Aquesta unitat (RA1) treballa la vessant FÍSICA, en els seus tres apartats: seguretat passiva, sistemes d'alimentació ininterrompuda i seguretat lògica.

## 4. Defensa en capes

Cap mesura de seguretat és infal·lible per si sola: es combinen diverses capes, de manera que si una falla, n'hi hagi una altra al darrere. Exemple típic (de fora cap a dins):

1. Tanca perimetral.
2. Murs de l'edifici.
3. Accés amb targeta.
4. Guarda de seguretat.

> 💡 Com més capes cal superar, més temps es guanya per detectar i reaccionar davant d'un atac.

## 5. Amenaça vs. risc

- **Amenaça**: qualsevol vulnerabilitat que un atacant pugui arribar a explotar (una finestra sense reixa, una porta sense pany...).
- **Risc**: la probabilitat que algú descobreixi aquella amenaça i l'exploti realment.

Segons l'origen:

- **Internes**: un incendi fortuït, una fuita d'aigua, o un empleat descontent. Difícils de controlar: coneixen el sistema per dins.
- **Externes**: atacants aliens que volen robar informació o malmetre recursos.

## 6. Ubicació de les instal·lacions

- **Visibilitat**: terrenys, cartells i logos discrets atrauen menys atacants.
- **Factors externs**: criminalitat de la zona, proximitat a policia/bombers/hospitals.
- **Accessibilitat**: accés per carretera, trànsit, proximitat a aeroports o estacions.
- **Desastres naturals**: inundacions, terratrèmols, allaus o despreniments.

> 📌 **Cas real:** algunes empreses instal·len servidors en mines abandonades per aprofitar-ne el fred natural. Un gegant d'Internet ha provat parcs de servidors flotants en vaixells: onades per energia, aigua per refrigerar i ubicació secreta = molta seguretat.

## 7. Condicions ambientals: temperatura i humitat

Uns equips escalfats es fan malbé. Per sobre dels límits interns (~80°C ordinadors/perifèrics, ~38°C discs), els components es poden fer malbé de manera irreparable. Humitat massa alta → corrosió; massa baixa → electricitat estàtica i curtcircuits.

## 8. Condicions elèctriques

Un **SAI** (Sistema d'Alimentació Ininterrompuda) garanteix la continuïtat del servei davant d'un tall extern (es tracta amb detall a l'[AA2](../AA2%20-%20Sistemes%20alimentacio%20ininterrompuda/T05_Temari_SAI.md)).

Les interferències electromagnètiques i de ràdio (cables mal aïllats, motors) també cal tenir-les en compte: els fluorescents són la font més habitual d'interferències de ràdio, per això no es passa cablejat de dades a prop seu.

## 9. Ventilació: no només fred

Un sistema d'aire condicionat de circuit tancat recicla l'aire ja filtrat de dins l'edifici. Cal filtrar-lo perquè la pols obstrueix els ventiladors de refrigeració, i certs gasos poden accelerar la corrosió dels components.

## 10. Prevenció d'incendis

Perquè hi hagi foc calen tres elements: **calor + combustible + oxigen**. N'hi ha prou d'eliminar-ne un:

- Sense combustible: escuma que aïlla el material.
- Sense oxigen: CO2 (perillós si hi ha persones).

> ⚠️ Com més combustible per m² acumulat, més ràpid es propaga: cal ordre a les zones d'emmagatzematge.

Els detectors poden ser òptics (fum) o de temperatura, manuals o automàtics. L'extinció, manual (extintors, mànegues) o automàtica (aspersors d'aigua o gas).

### Tipus de foc i com apagar-los

| Classe | Tipus | Exemple | Extinció |
|---|---|---|---|
| A | Comú | Fusta, paper | Aigua, escuma |
| B | Líquid | Petroli, carbó | CO2, escuma |
| C | Elèctric | Cables, material elèctric | CO2, pólvora seca |
| D | Metalls inflamables | Magnesi, sodi | Pólvora seca |

## 11. Quatre grans famílies de mesures de seguretat

1. **Dissuasives**: fer que l'atac sembli poc atractiu.
2. **Dificultat d'accés**: guanyar temps de reacció.
3. **Detecció d'intrusos**: saber que alguna cosa passa.
4. **Avaluació d'incidències**: decidir com respondre.

### 11.1. Mesures dissuasives

Tanques, murs, barrots, guardes de seguretat i gossos, senyals d'alerta i il·luminació nocturna.

> 💡 L'alçada d'una tanca canvia molt el seu efecte: 1 m només dissuadeix vianants casuals; 2 m és difícil d'escalar; 2,5 m transmet que l'empresa es pren la seguretat seriosament.

### 11.2. Dificultats d'accés: el "mantrap"

Una habitació amb DUES portes: s'obre la primera i un guarda identifica la persona; es tanca, i cal superar un control robust (biometria, targeta + contrasenya) per obrir la segona. Si no se supera, la persona queda atrapada entremig.

Altres controls: cadenats, targeta intel·ligent, teclat numèric, biometria.

### 11.3. Detecció i resposta

Els SDI (Sistemes de Detecció d'Intrusos) usen sensors interns i externs (perimetrals) que detecten canvis lumínics, acústics, de moviment o electromagnètics, i necessiten alimentació pròpia.

Els falsos positius existeixen: cal un protocol clar (qui truca a qui segons el tipus d'incidència) — un vidre trencat el revisa un guarda; un foc a la sala de servidors, els bombers.

## Resum de l'apartat

- La seguretat física és la base de tota la seguretat informàtica.
- Cap mesura és suficient sola: cal defensa en capes.
- L'entorn (temperatura, humitat, electricitat, incendis) és també un risc a gestionar.
- Quatre famílies de mesures: dissuadir, dificultar, detectar i avaluar.

## Per saber-ne més

- Institut Obert de Catalunya (IOC) — [Seguretat passiva](https://ioc.xtec.cat/materials/FP/Recursos/fp_smx_m06_/web/fp_smx_m06_htmlindex/WebContent/u1/a1/continguts.html), Unitat 1, apartat 1 (llicència CC BY-NC-SA, IOC 2011).
- Institut Obert de Catalunya (IOC) — [Introducció, Unitat 1](https://ioc.xtec.cat/materials/FP/Recursos/fp_smx_m06_/web/fp_smx_m06_htmlindex/WebContent/u1/introduccio.html) (llicència CC BY-NC-SA, IOC 2011).

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
