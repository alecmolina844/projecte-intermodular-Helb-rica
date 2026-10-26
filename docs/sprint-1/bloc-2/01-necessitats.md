# 03 · Disseny de la infraestructura i diagrama de xarxa

## 1. Diagrama de xarxa

![Diagrama de xarxa de Helbérica](../../../img/bloc-2/diagrama-xarxa.png)

## 2. Visió general

La xarxa de Helbérica es divideix en **tres zones** a la seu principal i una **xarxa remota** a la planta de xocolates:

| Zona | Xarxa | Què hi ha | Nivell de confiança |
|------|-------|-----------|---------------------|
| **Internet (WAN)** | IP pública | Connexió de fibra de l'operador | Cap: és una xarxa pública |
| **DMZ** | 172.16.10.0/24 | Servidor amb la web corporativa i l'intercanvi EDI | Mitjà: accessible des d'Internet, però aïllada |
| **Xarxa interna Segorb** | 192.168.10.0/24 | Servidors, ordinadors, impressores i Wi-Fi | Alt: només hi accedeix el personal |
| **Xarxa interna Espartal** | 192.168.20.0/24 | Terminal de planta, impressora d'etiquetes i Wi-Fi | Alt: unida a la seu per VPN |

El detall de totes les adreces IP es troba en [04 · Pla d'adreçament IP](04-adrecament-ip.md).

## 3. Components i funcions

### 3.1. Seu principal (P.I. Segorb)

| Component | Quantitat | Funció |
|-----------|:---------:|--------|
| Router de l'operador | 1 | Connexió de fibra amb IP pública fixa. Funciona en mode pont i passa tot el trànsit al servidor de comunicacions |
| **Servidor de comunicacions** (tallafocs perimetral) | 1 | Porta d'enllaç de tota l'empresa. Té tres interfícies (WAN, LAN i DMZ) i fa NAT, filtratge de trànsit, servidor VPN i proxy web |
| Servidor DMZ | 1 | Web corporativa i servidor SFTP per a l'intercanvi de comandes i albarans (EDI) amb els supermercats |
| Switch gestionable de 24 ports amb PoE | 1 | Connecta tots els equips de la xarxa interna i alimenta els punts d'accés pel mateix cable de xarxa (PoE) |
| Servidor principal | 1 | Controlador de domini (Active Directory), DNS, DHCP, fitxers compartits i ERP |
| NAS de còpies de seguretat | 1 | Rep cada nit la còpia del servidor principal |
| Ordinadors d'oficina | 8 | Direcció (portàtil), Administració, Producció, Qualitat i Magatzem |
| Terminal de planta | 1 | Registre de lots a la línia de galletes i barquillos |
| Impressores | 3 | 1 multifunció a les oficines i 2 d'etiquetes (línia de galletes i magatzem) |
| Punts d'accés Wi-Fi | 2 | Cobertura al magatzem i a la zona de producció |
| Terminals portàtils | 3 | Lectura de codis de barres al magatzem, connectats per Wi-Fi |
| SAI | 1 | Protegeix el servidor, el NAS, el tallafocs i el switch davant talls de llum |

### 3.2. Planta de xocolates (P.I. Espartal III)

| Component | Quantitat | Funció |
|-----------|:---------:|--------|
| Router amb tallafocs | 1 | Connexió de fibra i extrem de la VPN cap a la seu |
| Switch gestionable de 8 ports amb PoE | 1 | Connecta els equips de la planta |
| Terminal de planta | 1 | Registre de lots a la línia de xocolate |
| Impressora d'etiquetes | 1 | Etiquetes de lot de la línia de xocolate |
| Punt d'accés Wi-Fi | 1 | Cobertura per als terminals portàtils quan es mouen mercaderies entre plantes |
| SAI | 1 | Protegeix el router i el switch |

Les quantitats coincideixen amb el Bloc 1: **10 ordinadors** (8 d'oficina i 2 terminals de planta), **3 terminals portàtils**, **3 punts d'accés** i **4 impressores** (1 multifunció i 3 d'etiquetes). L'únic equip nou és el **servidor DMZ**, que apareix en aquesta fase en dissenyar la DMZ.

## 4. Connexions

- **Internet → servidor de comunicacions**: el router de l'operador només fa de pont. D'aquesta manera tot el trànsit passa obligatòriament pel tallafocs.
- **Servidor de comunicacions → DMZ i LAN**: cada zona va connectada a una interfície diferent del tallafocs, i ell decideix quin trànsit pot passar d'una a l'altra.
- **Switch → equips**: cablejat de categoria 6 des del switch fins a cada ordinador, terminal de planta, impressora i punt d'accés.
- **Punts d'accés → terminals portàtils**: Wi-Fi amb xifratge WPA3. És la mateixa xarxa interna, sense xarxa de convidats.
- **Seu ↔ planta de xocolates**: **túnel VPN IPsec** a través d'Internet entre el servidor de comunicacions i el router d'Espartal. Per als usuaris, les dues plantes funcionen com una sola xarxa.

## 5. La DMZ: quins servicis hi ha i per què

Una **DMZ** (zona desmilitaritzada) és una xarxa separada on es col·loquen els servidors que **han de ser accessibles des d'Internet**. Si algú ataca un d'aquests servidors, el tallafocs li impedeix arribar a la xarxa interna.

| Servici en la DMZ | Per què ha d'estar en la DMZ |
|-------------------|------------------------------|
| **Web corporativa** (HTTPS, port 443) | Clients i proveïdors la visiten des d'Internet |
| **Servidor SFTP per a EDI** (port 22) | Les cadenes de supermercats hi deixen les comandes i recullen albarans i factures de manera automàtica |

**Regles bàsiques del tallafocs:**

| Origen | Destinació | Permés? |
|--------|-----------|:-------:|
| Internet | DMZ (només ports 443 i 22) | ✅ |
| Internet | Xarxa interna | ❌ |
| Xarxa interna | Internet (a través del proxy) | ✅ |
| Xarxa interna | DMZ (per a gestionar el servidor i recollir les comandes) | ✅ |
| DMZ | Xarxa interna | ❌ |
| Planta d'Espartal (VPN) | Xarxa interna Segorb | ✅ |

Els **servidors interns** (domini, fitxers, ERP i còpies) **no estan mai en la DMZ**, perquè contenen les dades més importants i no han de ser accessibles des de fora.

## 6. Decisions tècniques

1. **Servidor de comunicacions dedicat amb tres interfícies**. És la manera més senzilla de crear una DMZ real: un únic punt que controla tot el trànsit entre Internet, la DMZ i la xarxa interna.
2. **Xarxa cablejada per als equips fixos i Wi-Fi només on cal**. El cable és més estable i segur per als ordinadors i els terminals de planta. El Wi-Fi només el necessiten els terminals portàtils del magatzem.
3. **Switches gestionables amb PoE**. Permeten alimentar els punts d'accés pel mateix cable i, si cal en el futur, separar departaments amb VLAN.
4. **VPN en lloc d'una línia dedicada entre plantes**. Les dues plantes ja tenen fibra, i una VPN és molt més barata i suficient per al trànsit de l'ERP.
5. **Servicis centralitzats a la seu**. El servidor i el NAS estan en un únic lloc, amb SAI. La planta d'Espartal només necessita equips de xarxa i de planta.
6. **Separació entre les zones**. Si el servidor de la DMZ es veu compromès, l'atacant no pot arribar ni a l'ERP ni als registres de qualitat.

## 7. Fonts tècniques consultades

- **INCIBE – Protegeix la teua empresa**: tallafocs, segmentació de xarxes i DMZ en pimes. [incibe.es/empresas](https://www.incibe.es/empresas)
- **Cisco – What Is a DMZ?** [cisco.com](https://www.cisco.com/c/en/us/products/security/firewalls/what-is-a-dmz.html)
- **Documentació de pfSense** (tallafocs de codi obert amb DMZ i VPN). [docs.netgate.com](https://docs.netgate.com/pfsense/en/latest/)
- **Wi-Fi Alliance – WPA3**. [wi-fi.org](https://www.wi-fi.org/discover-wi-fi/security)
- **Microsoft Learn – Active Directory Domain Services**. [learn.microsoft.com](https://learn.microsoft.com/es-es/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)
