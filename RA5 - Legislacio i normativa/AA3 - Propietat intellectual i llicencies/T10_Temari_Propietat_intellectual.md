# RA5 · AA3 — Propietat intel·lectual i llicències

*LPI, drets d'autor i tipus de llicències de programari.*

## 1. Introducció

El compliment legal a l'àmbit tecnològic no s'acaba amb la protecció de dades (LOPD-GDD) o els serveis d'Internet (LSSI): el tercer pilar és la propietat intel·lectual del programari i dels continguts digitals, regulada per la **Llei de Propietat Intel·lectual (LPI)**.

> ⚠️ Un tècnic informàtic que munta el servidor i la web d'una empresa ha de vetllar pel compliment de les tres normatives alhora: protecció de dades, serveis d'Internet, i propietat intel·lectual del programari que instal·la.

## 2. La Llei de Propietat Intel·lectual (LPI)

El Reial Decret Legislatiu 1/1996 (LPI) protegeix les creacions originals literàries, artístiques o científiques.

El **programari es considera legalment una obra literària**: el codi font està protegit pels mateixos drets d'autor que un llibre. El titular dels drets és, per defecte, l'autor, o l'empresa si el programari es va crear com a treball per encàrrec o dins d'una relació laboral.

## 3. Drets morals i drets d'explotació

### 3.1. Drets morals

Irrenunciables i intransferibles: dret a ser reconegut com a autor, a decidir si l'obra es divulga, i a exigir-ne la integritat (que no es modifiqui de manera que perjudiqui la reputació de l'autor).

### 3.2. Drets d'explotació

Es poden transferir o llicenciar a tercers: reproducció, distribució, comunicació pública i transformació (crear una obra derivada).

> 💡 Precisament perquè els drets d'explotació es poden llicenciar, existeix el concepte de "llicència de programari".

## 4. Què és una llicència de programari

Una llicència és el contracte pel qual el titular dels drets autoritza (o no) a un tercer a utilitzar, copiar, modificar o distribuir el seu programari, i sota quines condicions.

> ⚠️ Sense llicència explícita, per defecte, **NO** es té cap dret sobre el programari ("tots els drets reservats"). Instal·lar o utilitzar programari sense la llicència corresponent és una infracció de la LPI, amb conseqüències civils i, en casos greus, penals.

## 5. Programari propietari vs. programari lliure

### 5.1. Programari propietari

El codi font no és accessible; l'usuari només rep el dret d'ús, sota condicions restrictives. Exemples: Windows, Microsoft Office, Adobe Photoshop.

### 5.2. Programari lliure (Free Software)

Segons la Free Software Foundation, garanteix quatre llibertats:

- **Llibertat 0**: executar el programa amb qualsevol propòsit.
- **Llibertat 1**: estudiar com funciona i adaptar-lo a les necessitats pròpies (requereix el codi font).
- **Llibertat 2**: redistribuir còpies per ajudar els altres.
- **Llibertat 3**: millorar el programa i publicar-ne les millores (requereix també el codi font).

> 💡 El terme "free" en "free software" fa referència a la **llibertat**, no al preu ("free speech, not free beer").

## 6. Lliure, obert i gratuït: no és el mateix

| Terme | Significat real |
|---|---|
| **Programari lliure** (free software) | Garanteix les 4 llibertats de l'usuari. |
| **Codi obert** (open source) | Codi font accessible i modificable; accent en el desenvolupament col·laboratiu. |
| **Gratuït** (freeware) | Es pot usar sense pagar, però el codi font NO és accessible ni modificable (ex: WhatsApp Desktop). |

## 7. Llicències de programari lliure/obert més usades

| Llicència | Característica principal |
|---|---|
| **GPL** (GNU General Public License) | *Copyleft*: si distribueixes una obra derivada, l'has de distribuir també amb llicència GPL i codi obert. |
| **LGPL** | Versió permissiva de la GPL per a biblioteques: es pot enllaçar des de programari propietari. |
| **MIT / BSD** | Permissives: gairebé qualsevol ús (incloent-hi derivats propietaris), només cal mantenir l'avís de copyright. |
| **Apache 2.0** | Permissiva, similar a MIT/BSD, amb clàusula explícita de protecció de patents. |

> 💡 El "copyleft" (GPL) és una estratègia legal intel·ligent: usa el mateix dret d'autor per obligar que les millores tornin a ser lliures, en lloc de restringir-ne l'ús.

## 8. Llicències Creative Commons (CC)

Pensades per a obres no necessàriament de programari: textos, imatges, música, materials educatius (com aquests mateixos apunts). Es combinen quatre condicions:

- **BY** (atribució): cal citar sempre l'autor original.
- **NC** (No comercial): no es pot fer un ús comercial de l'obra.
- **ND** (No derivades): no es pot modificar l'obra.
- **SA** (Compartir igual / Share-Alike): si es modifica, cal distribuir-la amb la mateixa llicència.

> 📌 Aquests mateixos apunts es distribueixen sota llicència **CC-BY-SA**: es poden reutilitzar i modificar sempre que se citi l'autor original i es mantingui la mateixa llicència.

## 9. Pirateria i responsabilitat professional

La BSA (Business Software Alliance) i entitats similars auditen empreses per detectar programari sense llicència. Les multes poden superar els milers d'euros per còpia il·legal, a més de l'obligació de regularitzar la situació.

Un tècnic de sistemes que instal·la programari piratejat en equips d'una empresa client pot tenir responsabilitat professional directa, no només l'empresa: per això cal documentar sempre les llicències instal·lades mitjançant un inventari de programari (**Software Asset Management, SAM**).

## 10. Gestió d'actius de programari (SAM)

- Mantenir un inventari de tot el programari instal·lat, amb el tipus de llicència i el nombre de còpies autoritzades.
- Verificar periòdicament que el nombre d'instal·lacions no supera el de llicències adquirides.
- Valorar alternatives lliures/obertes (LibreOffice, GIMP, Linux) quan el pressupost o els requisits ho permetin.

## Resum de l'apartat

- El programari és una obra protegida per la LPI, amb drets morals (irrenunciables) i d'explotació (llicenciables).
- Sense llicència explícita, per defecte no es tenen drets sobre el programari.
- Lliure, obert i gratuït són conceptes diferents: lliure fa referència a la llibertat de l'usuari, no al preu.
- GPL (copyleft) obliga a mantenir la llibertat en les obres derivades; MIT/BSD/Apache són permissives.
- Creative Commons regula obres no necessàriament de programari (BY, NC, ND, SA).
- La gestió d'actius de programari (SAM) és essencial per evitar sancions.

## Per saber-ne més

- INCIBE — "Compliment legal a l'àmbit tecnològic (LOPDGDD, LSSI i LPI)".
- Real Decreto Legislativo 1/1996, Ley de Propiedad Intelectual (LPI).
- Free Software Foundation — "What is free software?".
- Creative Commons — "About the licenses".

---
*Mòdul 0226 · Seguretat informàtica — CFGM SMX2 — Institut Puig Castellar*
