# RA1 · AA2 — Sistemes d'alimentació ininterrompuda

*Que un tall de llum no aturi mai la feina.*

## 1. El problema: un tall de llum no avisa

Una pèrdua sobtada de corrent atura l'ordinador a l'instant: pot malmetre el maquinari i provocar la pèrdua de dades vitals que encara no s'havien desat. Un **SAI** (Sistema d'Alimentació Ininterrompuda, UPS en anglès) garanteix una alimentació contínua i de bona qualitat, encara que hi hagi talls de llum.

> 💡 Igual que cada cotxe necessita un model de pneumàtic i una pressió concrets, cada equip necessita un SAI adequat. Un SAI domèstic no serveix per a un centre de dades, i mai s'hi ha de connectar més càrrega de la que suporta.

## 2. Quatre maneres de fer malbé un equip

- **Apagades**: tall total del subministrament.
- **Sobretensions**: el voltatge puja per sobre del normal.
- **Baixades de tensió**: el voltatge baixa per sota del normal.
- **Variació de freqüència**: el senyal ja no va als 50 Hz habituals a Europa.

## 3. Sobretensions

Un dispositiu electrònic està dissenyat per rebre un voltatge màxim concret; superar-lo el pot fer malbé a l'instant (per exemple, un LED de 1,35 V que suporta com a màxim 1,6 V es fondria a 3 V).

### 3.1. Causes habituals

- Apagades i talls de llum.
- Llamps (les més perilloses).
- Curtcircuits.
- Grans motors o aires condicionats que alteren la línia.

> 💡 Un descarregador de sobretensió és una protecció bàsica i econòmica per a PC, monitors i impressores (no tots els endolls múltiples en porten). Davant d'una tempesta, el més segur és desendollar l'equip.

## 4. Baixades de tensió

Menys serioses que les sobretensions: la majoria d'equips toleren fluctuacions grans. Sovint causades per un motor gran que arrenca i "roba" tensió a la resta de la línia. Un **regulador de voltatge (VRM)** manté el nivell de voltatge, eliminant tant sobretensions com baixades.

## 5. El SAI: bateria + protecció en un sol aparell

- **Bateria**: subministra electricitat quan falla la línia principal.
- **Protecció**: filtra sobretensions, baixades i soroll de línia.
- **Autonomia**: de pocs minuts a diverses hores, segons el model.

> 💡 Si cal encara més temps, el SAI pot donar marge fins que arrenqui un grup electrogen.

## 6. Les 6 parts principals d'un SAI

1. Circuits d'inversió/conversió (altern ↔ continu).
2. Bateria (determina mida i autonomia).
3. Interruptor principal.
4. Connectors de sortida.
5. Indicadors d'estat (LED, alarmes sonores).
6. Programari de control (monitoratge des de l'ordinador).

### 6.1. Indicadors d'estat

| Indicador | Significat |
|---|---|
| De línia (online) | Funciona amb corrent de la línia elèctrica normal. |
| De bateria (on battery) | Funciona amb l'energia de la bateria. |
| Sobrecàrrega (overload) | Més equips connectats dels que el SAI pot gestionar. |
| Substituir bateria | La bateria està en mal estat. |

### 6.2. El programari de monitoratge

Connectant un cable (avui, normalment USB) del SAI a l'ordinador: estat (càrrega, condicions ambientals), registre (historial d'esdeveniments), diagnòstic (comprovacions programades), alarmes a l'ordinador, i apagada automàtica que tanca el sistema de forma segura.

## 7. Tipus de SAI

| Tipus | Funcionament | Ús habitual |
|---|---|---|
| **Standby** (offline) | La bateria només actua quan falla la línia. Transferència breu. | Barat, per a PC domèstics. |
| **Interactiu de línia** (offline) | L'inversor sempre és a la sortida: resposta més ràpida. | Petites empreses, servidors web. |
| **Online** | L'ordinador sempre rep corrent de la bateria. Zero temps de transferència. | Car, per a centres de dades. |

### 7.1. La gran diferència: el "temps de transferència"

En els SAI standby/interactius hi ha un breu interval (fracció de segon) entre el tall de llum i el moment en què la bateria alimenta l'ordinador — prou curt per no notar-se, però existeix. En un SAI **online**, l'ordinador sempre rep alimentació de la bateria: zero temps de transferència, la protecció més robusta que existeix.

## 8. Escollir el SAI: càrrega, autonomia i capacitat

- **Càrrega**: el conjunt d'equips connectats.
- **Autonomia**: temps que el SAI pot alimentar la càrrega.
- **Capacitat**: la potència màxima que pot subministrar.

Exemple real (SAI APC Back-UPS 550VA):

| Càrrega (VA) | Autonomia |
|---|---|
| 80 VA | 43 min |
| 160 VA | 22 min |
| 320 VA | 9 min |
| 480 VA (87% capacitat) | 4 min |

> ⚠️ Com més càrrega connectada, menys autonomia. Amb només 4 minuts, cal decidir de seguida si n'hi ha prou per aturar els equips ordenadament.

## 9. Compte amb les unitats: Watts (W) ≠ Voltamperes (VA)

- **Potència real (W)**: la que consumeix realment la càrrega.
- **Potència aparent (VA)**: la que subministra el SAI (sempre ≥ que la real).

> ⚠️ Error habitual: un SAI de 300 W / 500 VA NO serveix per a una càrrega de 400 W, encara que "400 no arribi a 500". Cal comparar W amb W, mai W amb VA.

## 10. A l'hora de decidir i ubicar el SAI

- Quina càrrega haurà de suportar? Suma la potència real (W) de tots els equips.
- Quanta autonomia vols? Pocs minuts o hores, segons la criticitat.
- De quin espai disposes? Prop dels equips, amb bona ventilació.

> 💡 Alguns SAI generen molta calor: en una sala mal climatitzada poden malmetre el propi maquinari que haurien de protegir. Cables sempre ben recollits, mai enmig del pas.

## Resum de l'apartat

- 4 problemes elèctrics: apagades, sobretensions, baixades de tensió, variació de freqüència.
- Un SAI combina bateria + protecció elèctrica.
- 3 tipus de SAI: standby, interactiu de línia i online (sense temps de transferència).
- Escollir un SAI: calcula sempre en watts (W), mai en VA, i pensa l'autonomia necessària.

## Per saber-ne més

- Institut Obert de Catalunya (IOC) — [Sistemes d'alimentació ininterrompuda](https://ioc.xtec.cat/materials/FP/Recursos/fp_smx_m06_/web/fp_smx_m06_htmlindex/WebContent/u1/a2/continguts.html), Unitat 1, apartat 2 (llicència CC BY-NC-SA, IOC 2011).

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
