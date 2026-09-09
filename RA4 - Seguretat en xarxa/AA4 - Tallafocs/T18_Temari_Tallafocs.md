# RA4 · AA4 — Tallafocs (Firewall)

*El porter digital que decideix qui entra i qui surt.*

## 1. Introducció

El terme "firewall" prové de la construcció: una paret tallafocs atura la propagació d'un incendi entre dues zones d'un edifici. Un tallafocs informàtic fa el mateix amb el trànsit de xarxa: n'atura la propagació no autoritzada.

Un tallafocs és un sistema (maquinari, programari o ambdós) que controla el trànsit entrant i sortint, permetent-lo o bloquejant-lo segons regles predefinides, filtrant per IP, ports, protocols i, en els més avançats, per contingut o estat de la connexió.

> ⚠️ Un tallafocs NOMÉS filtra segons regles: no detecta malware dins d'un fitxer permès, ni protegeix d'enginyeria social. Cal combinar-lo amb antivirus, IDS/IPS i formació.

## 2. Tipus de tallafocs segons la ubicació

- **De maquinari / perimetral**: dispositiu dedicat entre la xarxa interna i Internet (pfSense, Fortinet, Cisco ASA).
- **De programari / d'equip**: instal·lat al SO, protegeix un únic equip (UFW/iptables, Windows Defender Firewall).
- **Personal**: similar al de programari, orientat a usuaris domèstics.

## 3. Filtratge de paquets vs. inspecció d'estat

- **Stateless**: analitza cada paquet independentment. Ràpid, menys segur.
- **Stateful**: manté una taula de connexions actives i només permet respostes a connexions ja establertes. Estàndard actual.

> 💡 Els NGFW (Next-Generation Firewall) hi afegeixen inspecció profunda de paquets (DPI), IDS/IPS integrat i filtratge per aplicació.

## 4. Polítiques de filtratge

| Política | Descripció |
|---|---|
| **Denegació per defecte** (whitelist) | Bloqueja tot, permet només el necessari. Més segura. |
| **Permissió per defecte** (blacklist) | Permet tot, bloqueja només el conegut com a perillós. Més còmoda, insegura davant 0-days. |

> ⚠️ Bona pràctica: denegació per defecte en trànsit ENTRANT, permissió per defecte en SORTINT.

## 5. DMZ: la zona desmilitaritzada

Subxarxa intermèdia entre la xarxa interna i Internet, on se situen serveis accessibles des de fora (web, correu, DNS públic). Si un servidor de la DMZ és compromès, el tallafocs impedeix el salt directe a la xarxa interna.

## 6. Pràctica: UFW (Uncomplicated Firewall)

Simplifica iptables/nftables amb sintaxi llegible:

```
ufw default deny incoming
ufw default allow outgoing
ufw allow 22/tcp comment 'SSH administracio'
ufw deny from <IP>
ufw enable
ufw status verbose
```

> ⚠️ En un tallafocs remot (SSH), cal permetre SEMPRE el port 22 ABANS d'activar la denegació per defecte.

## 7. Manteniment de regles

`ufw status numbered` numera les regles per poder eliminar-les amb `ufw delete <número>`. Regles obsoletes i sense documentar acumulades amb els anys són un risc tan gran com no tenir-ne cap: cal revisar-les periòdicament i comentar sempre el motiu de cada regla.

## Resum de l'apartat

- Un tallafocs filtra trànsit segons regles, però no és una solució completa per si sol.
- Es classifica per ubicació (perimetral, d'equip, personal) i tecnologia (paquets, estat, NGFW).
- La denegació per defecte (sobretot en entrant) és la política més segura.
- Una DMZ limita el dany d'un servidor exposat compromès.
- UFW facilita la gestió pràctica d'un tallafocs Linux.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF5/AA4-Tallafocs.md) (GitHub, SMX-0226SI) — llicència CC-BY-SA-4.0.
- UFW — [documentació oficial](https://help.ubuntu.com/community/UFW)
- Cloudflare — "What is a firewall?".
- [pfSense](https://pfsense.org)

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
