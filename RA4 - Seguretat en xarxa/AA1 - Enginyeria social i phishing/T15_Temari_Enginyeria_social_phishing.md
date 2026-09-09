# RA4 · AA1 — Enginyeria social i phishing

*La línia de defensa més feble no és la tecnologia: som nosaltres.*

## 1. El factor humà com a vector d'atac

Les eines de protecció tecnològiques (firewalls, IDS/IPS, antivirus) són cada cop més robustes. Per això els ciberdelinqüents prefereixen atacar la línia de defensa més feble: **l'usuari final**.

> 💡 L'enginyeria social no busca vulnerabilitats en el codi o el maquinari, sinó en el factor humà: manipulació psicològica perquè es revelin dades o s'executin accions compromeses.

## 2. Principals tècniques d'enginyeria social

### 2.1. Suplantació d'identitat digital

- **Phishing**: correus que simulen fonts fiables per capturar contrasenyes o dades bancàries.
- **Spear phishing**: variant personalitzada dirigida a una persona/departament concret.
- **Whaling**: spear phishing dirigit a executius (CEO, CFO), amb impacte potencial elevadíssim.

### 2.2. Canals alternatius

- **Smishing**: SMS amb enllaços maliciosos o peticions urgents.
- **Vishing**: enginyeria social telefònica, suplantant suport tècnic o entitats bancàries.

> ⚠️ Amb la IA, els atacants poden generar veus i videoconferències falses (deepfake) molt creïbles.

### 2.3. Contextualització i causalitat

- **Pretexting**: escenari fictici (ex: tècnic de TI urgent) per guanyar-se la confiança.
- **Baiting**: esquer físic/digital atractiu (ex: USB infectat amb l'etiqueta "Nòmines_2026.xlsx").

### 2.4. Observació i recol·lecció d'informació

- **Shoulder surfing**: observar tecles/pantalles quan la víctima escriu contrasenyes.
- **Dumpster diving**: cercar informació confidencial en paper no destruït adequadament.

> 📌 **Cas real:** Kevin Mitnick, hacker famós dels anys 90, expert en aquestes tècniques. Va escriure "The Art of Deception".

## 3. Impacte en organitzacions i empreses

- **Frau del CEO / del proveïdor**: suplantació per aconseguir transferències fraudulentes.
- **Ransomware**: més del 80% dels atacs comencen amb un correu de phishing.
- **Exfiltració de dades i sancions RGPD/LOPDGDD**: pèrdues econòmiques, reputacionals i legals.

## 4. Correu no desitjat (spam)

Provoca consum de recursos de xarxa i saturació de bústies.

> ⚠️ La LSSI-CE tipifica com a infracció greu l'enviament de correu comercial sense consentiment previ, però la majoria de l'spam prové de fora de l'àmbit legal.

### 4.1. Protecció contra el correu brossa

| Protocol/Tècnica | Funció |
|---|---|
| SPF | Especifica servidors autoritzats a enviar en nom d'un domini. |
| DKIM | Signatura digital del correu, per detectar-ne alteracions. |
| DMARC | Indica com tractar el correu que no compleix SPF/DKIM. |
| Llistes negres/blanques/grises | Bloqueig, confiança o retard segons la reputació del remitent. |
| Filtres heurístics | Puntuen patrons sospitosos al contingut. |
| Filtratge bayesià | Aprenentatge automàtic sobre l'historial classificat per l'usuari. |

> 💡 Eines populars: SpamAssassin, MailScanner.

## 5. Estratègies de prevenció i mitigació

1. Formació i conscienciació contínua (simulacres de phishing).
2. Autenticació multifactor (MFA/2FA).
3. Principi del mínim privilegi.
4. Polítiques de seguretat i procediments de resposta.
5. Filtres de correu i sistemes de detecció.

## Resum de l'apartat

- L'enginyeria social ataca el factor humà, no la tecnologia.
- Phishing, spear phishing, whaling, smishing, vishing, pretexting i baiting sovint es combinen.
- SPF, DKIM i DMARC són essencials per protegir el propi domini de correu.
- Mesures tècniques (MFA, filtres) + humanes (formació) = la defensa més eficaç.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF5/AA1-EnginyeriaSocialPhising.md) (GitHub, SMX-0226SI) — llicència CC-BY-SA-4.0.
- INCIBE — "Fraude del CEO".
- ESET — "Phishing".
- PowerDMARC — "All About SPF, DKIM, and DMARC".

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
