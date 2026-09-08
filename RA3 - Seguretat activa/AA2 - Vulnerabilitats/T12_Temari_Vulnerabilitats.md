# RA3 · AA2 — Vulnerabilitats

*Amenaces, vulnerabilitats i risc: com es mesura la nostra exposició.*

## 1. Amenaces i vulnerabilitats

Les **amenaces** són accions externes que afecten la seguretat dels nostres sistemes. No sempre són atacs intencionats: també cal considerar accidents o errors humans. Aquestes amenaces exploten **vulnerabilitats**, factors interns febles o defectes que debiliten la seguretat d'un sistema. La combinació de vulnerabilitats amb amenaces determina el **risc**.

### 1.1. Classificació de les amenaces

| Amenaça | Efecte |
|---|---|
| Interrupció | Un recurs deixa d'estar disponible. |
| Intercepció | Un intrús accedeix a la informació. |
| Modificació | La informació és alterada sense autorització. |
| Fabricació | Es crea un producte fals (ex: web falsa) per robar informació. |

> ⚠️ Bona part de les amenaces es basen en hàbits poc segurs: comptes d'administrador pel treball diari, enllaços poc fiables, pendrives desconeguts, manca d'actualitzacions.

## 2. Vulnerabilitats

Una vulnerabilitat és un error en un sistema que permet violar la política de seguretat definida.

> ⚠️ Una vulnerabilitat **0-day** encara no ha estat reportada: no existeix cap solució ni actualització que la corregeixi. Especialment perillosa.

Política proactiva: actualitzacions de SO/aplicacions/firmware, estar informat de noves vulnerabilitats, usar escàners.

### 2.1. Registre de vulnerabilitats (CVE)

La base de dades **CVE-Mitre** assigna un identificador únic amb el format `CVE-AAAA-NNNNN`. Es classifiquen per gravetat (Low/Medium/High/Critical) i pel sistema **CVSS** (puntuació de 0 a 10).

> 💡 Score: calculat tècnicament (dificultat d'explotació, privilegis necessaris, impacte real). Gravetat: etiqueta de text per a una valoració ràpida de la urgència.

### 2.2. Eines de detecció de vulnerabilitats

Metasploit, Nessus, OpenVAS (derivat de Nessus, obert), Vera (serveis web).

> 📌 **Actualitat:** amb la IA, també s'utilitzen models per detectar vulnerabilitats — Claude Mythos (Anthropic) n'ha detectat múltiples, algunes existents des de fa molts anys.

## 3. Risc i impacte

- **Risc**: probabilitat que una amenaça aprofiti una vulnerabilitat. *Quina probabilitat hi ha que ens ataquin?*
- **Impacte**: mida del dany (econòmic, reputacional, legal). *Si l'atac té èxit, quant costa?*

$$Risc = Probabilitat \times Impacte$$

> 📌 **Exemple:** un ordinador de recepció sense contrasenya té impacte ALT (historial mèdic confidencial). Si és visible a tothom, el risc és ALT; si està en un despatx tancat, el risc baixa (mateix impacte, menys probabilitat).

## 4. Exploits i pentesting

Els **exploits** aprofiten una vulnerabilitat per obtenir accés: **locals** (accés físic) o **remots** (via xarxa). Bases de dades com exploitDB en recopilen milers.

Els **pentests** (proves de penetració) són atacs controlats per trobar vulnerabilitats i determinar la viabilitat i l'impacte real d'un atac.

## 5. Eines de detecció d'intrusions

### 5.1. Inspecció de logs

No evita un atac, però permet saber que se n'ha patit un i com. Els atacants sovint intenten esborrar-los — això mateix ja és un indici.

### 5.2. IDS/IPS

**IDS** (detecció): compara paquets amb una base de dades d'atacs i genera alertes. **IPS** (prevenció): a més, actua (bloqueja, denega). Poden protegir un equip (HIDS) o tota la xarxa (NIDS). Exemples: Suricata, OSSEC/Wazuh.

### 5.3. Honeypots

Trampes que simulen ser una víctima real: registren les accions de l'atacant i mantenen els sistemes reals fora de perill. Exemples: T-Pot, FaPro.

## 6. Pràctica: escàners de xarxa

Eines com **Nmap** descobreixen dispositius i serveis actius sense necessitat d'agents instal·lats. Exploració **activa** (envia paquets) o **passiva** (només escolta).

> ⚠️ En pentesting, sempre s'usa mode passiu per no ser detectat.

`nmap --top-ports 20 -sV -Pn <IP>` escaneja els 20 ports més habituals i n'informa l'estat. Un sistema ben protegit mostra només els serveis estrictament necessaris com a "obert": menys ports oberts, menys "superfície d'atac".

## Resum de l'apartat

- Amenaça (extern) + vulnerabilitat (intern) = risc = probabilitat × impacte.
- CVE cataloga vulnerabilitats amb identificador i puntuació CVSS.
- Exploits aprofiten vulnerabilitats; el pentesting les busca de manera controlada.
- IDS/IPS, honeypots i logs aporten capacitat de detecció, no només prevenció.
- Nmap i similars permeten auditar quins serveis estan realment exposats.

## Per saber-ne més

- Repositori ["Materials"](https://github.com/SMX-0226SI/Materials/blob/main/NF3/AA2-vulnerabilitats.md) (GitHub, SMX-0226SI) — llicència CC-BY-SA-4.0.
- [CVE-Mitre](https://cve.mitre.org/) · [NVD-NIST](https://nvd.nist.gov/)
- INCIBE-CERT — Guía de gestión de riesgos.
- [Nmap](https://nmap.org)

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
