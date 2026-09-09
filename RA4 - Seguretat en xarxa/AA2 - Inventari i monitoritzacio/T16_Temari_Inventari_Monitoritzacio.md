# RA4 · AA2 — Inventari i monitorització de la xarxa

*Saber què hi ha connectat i què hi circula, per poder-ho protegir.*

## 1. Introducció

Per protegir una xarxa cal, en primer lloc, conèixer-la: saber quins dispositius hi ha connectats, com estan interconnectats i quin trànsit hi circula. Aquest coneixement es construeix mitjançant l'**inventari** (què hi ha) i la **monitorització** (què hi passa).

> ⚠️ Imagineu una empresa amb 1.000 equips connectats: seria inviable comprovar-ho tot manualment. Cal automatitzar-ho.

### 1.1. Mapa físic vs. mapa lògic

El **mapa físic** representa la ubicació real dels equips i el cablejat. El **mapa lògic** representa com estan interconnectats (subxarxes, VLANs, encaminament), independentment de la seva ubicació física. Tots dos són complementaris.

## 2. Inventari automàtic de dispositius

### 2.1. Protocol SNMP

Permet gestionar i monitoritzar dispositius de xarxa. Model client-servidor: els dispositius actuen com a **agents** que recopilen informació, i un **gestor SNMP** centralitzat la recull periòdicament.

### 2.2. Escàners de xarxa

Eines com **Nmap** descobreixen dispositius enviant paquets i analitzant respostes, sense necessitar cap agent instal·lat. Exploració **activa** (envia paquets) o **passiva** (només escolta).

> ⚠️ En pentesting, es prefereix sempre el mode passiu, per no ser detectat.

`nmap -sn 192.168.1.0/24` fa un descobriment d'amfitrions: identifica dispositius actius sense escanejar-ne els ports. Combinat després amb `-sV` sobre cada IP, es pot identificar quins serveis executa cada dispositiu.

## 3. Sniffers: monitorització del trànsit

Un sniffer (com **Wireshark**) captura i analitza en temps real els paquets que circulen per la xarxa.

- **Ús legítim**: diagnosticar problemes, analitzar rendiment, verificar el trànsit.
- **Risc de seguretat**: en una xarxa NO xifrada, un atacant pot capturar contrasenyes i dades privades; eines avançades permeten fins i tot modificar paquets (man-in-the-middle).

### 3.1. Mode promiscu i port mirroring

Una targeta de xarxa normal només rep el trànsit destinat a ella mateixa. Per veure TOT el trànsit calen:

1. **Mode promiscu**: la targeta accepta tots els paquets, siguin o no destinats a l'equip.
2. **Port mirroring** al switch: duplica el trànsit d'un port/VLAN cap a un altre port amb el sniffer.

> 💡 Alternativa: un "LAN tap" físic instal·lat entre el switch i el router/servidor.

## 4. Pràctica: tshark

La versió de línia de comandes de Wireshark. `tshark -i <interfície> -w captura.pcap` captura trànsit; `tshark -r captura.pcap -Y '<filtre>'` en llegeix i filtra el contingut (ex: `-Y http`).

## 5. Protecció del trànsit de xarxa

- **TLS**: assegura HTTPS i altres protocols (SMTP, IMAP, FTP).
- **SSH** en lloc de Telnet.
- **VPN**: connexions xifrades sobre xarxes no confiables.

## 6. Seguretat en xarxes sense fils

A una xarxa cablejada cal accés físic per intrusió; a una sense fils, es pot accedir des de qualsevol punt dins l'àrea de cobertura.

### 6.1. Evolució dels protocols Wi-Fi

| Protocol | Estat |
|---|---|
| WEP | Obsolet i molt insegur des de 2004 (RC4, clau estàtica). |
| WPA | Millora WEP (TKIP), també vulnerable; no recomanat. |
| WPA2 | AES 128 bits. Popular i segur, amb vulnerabilitats conegudes (KRACK). |
| WPA3 | El més recent: AES 192 bits (empresarial), clau única per comunicació, SAE en lloc de PSK. |

> ⚠️ Cal configurar WPA3 (o WPA2 com a mínim) a qualsevol xarxa Wi-Fi.

## Resum de l'apartat

- L'inventari (SNMP, Nmap) permet saber automàticament què hi ha connectat.
- La monitorització (Wireshark/tshark) analitza el trànsit real, però mal utilitzada és també un risc.
- Mode promiscu + port mirroring (o un LAN tap) capturen tot el trànsit des d'un sol punt.
- El xifrat (TLS, SSH, VPN) és la defensa fonamental contra la captura de trànsit.
- WPA3 (o WPA2 mínim) és l'estàndard Wi-Fi recomanat.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF5/AA2-InventariMonitoritzacio.md) (GitHub, SMX-0226SI) — llicència CC-BY-SA-4.0.
- [Wireshark](https://www.wireshark.org) · [Nmap](https://nmap.org)
- Kaspersky — "¿Qué es WEP, WPA, WPA2 y WPA3?".

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
