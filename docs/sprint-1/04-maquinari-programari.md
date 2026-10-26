# 04 · Relació de maquinari i programari

Aquesta relació recull tots els recursos identificats en el document [03 · Recursos TIC](03-recursos-tic.md), organitzats per departament. Les quantitats coincideixen amb el nombre de treballadors de cada departament definit en [02 · Organització](02-organitzacio.md).

> En aquesta fase no s'especifiquen marques, models ni preus. Això es farà en el Bloc 2.

## 1. Maquinari

| Recurs | Departament | Quantitat | Funció |
|--------|-------------|:---------:|--------|
| Ordinador portàtil | Direcció general | 1 | Gestió de l'empresa, correu i reunions amb clients fora de l'oficina |
| Pantalla de reunions | Direcció general | 1 | Reunions i videoconferències amb clients |
| Ordinador de sobretaula | Administració | 2 | Comptabilitat, facturació, nòmines, compres i comandes |
| Impressora multifunció de xarxa | Administració | 1 | Impressió, còpia i escaneig de factures, albarans i documents |
| Ordinador de sobretaula | Producció | 1 | Planificació de la producció (cap de producció) |
| Ordinador de sobretaula | Producció | 1 | Manteniment: fitxes de les màquines i ordres de treball |
| Terminal de planta (PC industrial) | Producció | 2 | Registre de lots i producció a peu de línia (un en cada planta) |
| Impressora d'etiquetes | Producció | 2 | Etiquetes de lot i data de consum preferent (línia de galletes i barquillos i línia de xocolate) |
| Ordinador de sobretaula | Qualitat | 2 | Sistema IFS, traçabilitat i registre d'anàlisis |
| Lector de codis de barres | Qualitat | 2 | Lectura dels lots per al control de traçabilitat |
| Ordinador de sobretaula | Magatzem i logística | 1 | Inventari, expedicions i albarans |
| Terminal portàtil amb lector de codis de barres | Magatzem i logística | 3 | Entrades i eixides de mercaderia i preparació de comandes |
| Impressora d'etiquetes | Magatzem i logística | 1 | Etiquetes dels palets per a l'expedició |
| Servidor principal | Tota l'empresa | 1 | Controlador de domini, fitxers compartits i programa de gestió (ERP) |
| Servidor de còpies de seguretat (NAS) | Tota l'empresa | 1 | Còpies de seguretat automàtiques diàries |
| Router amb tallafocs | Tota l'empresa | 2 | Connexió a Internet, protecció de la xarxa i VPN entre les dues plantes |
| Switch gestionable | Tota l'empresa | 2 | Connexió dels equips per cable, un en cada planta |
| Punt d'accés Wi-Fi | Tota l'empresa | 3 | Cobertura sense fil per als terminals portàtils al magatzem i a producció |
| SAI (sistema d'alimentació ininterrompuda) | Tota l'empresa | 2 | Protecció del servidor i dels equips de xarxa davant talls de llum |

## 2. Programari

| Recurs | Departament | Quantitat | Funció |
|--------|-------------|:---------:|--------|
| Sistema operatiu d'escriptori | Tots els departaments | 10 | Sistema operatiu dels ordinadors i dels terminals de planta |
| Sistema operatiu de servidor | Tota l'empresa | 1 | Sistema operatiu del servidor principal (domini, usuaris i permisos) |
| Programa de gestió empresarial (ERP) | Direcció, Administració, Producció i Magatzem | 7 | Comandes, producció, estocs, compres i facturació en un mateix programa |
| Programa de comptabilitat i nòmines | Administració | 2 | Comptabilitat, impostos i nòmines dels treballadors |
| Programari ofimàtic | Direcció, Administració, Producció, Qualitat i Magatzem | 8 | Documents, fulls de càlcul i presentacions |
| Correu electrònic i calendari | Direcció, Administració, Producció, Qualitat i Magatzem | 8 | Comunicació interna i amb clients i proveïdors |
| Programa de videoconferència | Direcció general | 1 | Reunions a distància amb els clients |
| Programa de gestió de la qualitat i traçabilitat | Qualitat | 2 | Registres de la certificació IFS, anàlisis, lots i incidències |
| Programa de gestió del manteniment | Producció | 1 | Control de les revisions i avaries de la maquinària |
| Programa de registre de producció | Producció | 2 | Registre dels lots fabricats en els terminals de planta |
| Programa de disseny i impressió d'etiquetes | Producció i Magatzem | 3 | Creació de les etiquetes amb lot, data i codi de barres |
| Aplicació de gestió de magatzem | Magatzem i logística | 3 | Lectura de codis i moviments de mercaderia des dels terminals portàtils |
| Antivirus i protecció d'equips | Tota l'empresa | 11 | Protecció dels 10 ordinadors i del servidor contra virus i atacs |
| Programari de còpies de seguretat | Tota l'empresa | 1 | Programació i control de les còpies de seguretat al NAS |

## 3. Comprovació de les quantitats

**Ordinadors (10)**: 1 portàtil de Direcció + 2 d'Administració + 2 de Producció + 2 terminals de planta + 2 de Qualitat + 1 de Magatzem.

**Llicències d'ofimàtica i correu (8)**: tots els ordinadors excepte els 2 terminals de planta, que només s'utilitzen per a registrar la producció.

**Llicències d'ERP (7)**: Direcció (1), Administració (2), cap de producció (1), terminals de planta (2) i Magatzem (1).

## 4. Justificació

- **El maquinari s'ajusta a la plantilla**: només tenen ordinador propi els 10 llocs que el necessiten. Els 11 operaris de línia comparteixen els terminals de planta, i els mossos de magatzem fan servir els terminals portàtils.
- **La traçabilitat condiciona molts recursos**: terminals de planta, lectors, impressores d'etiquetes i el programa de qualitat permeten seguir cada lot, tal com exigeixen la certificació IFS i els supermercats.
- **Un ERP comú** evita que cada departament treballe amb dades diferents: la comanda que registra Administració la veuen Producció i Magatzem.
- **La seguretat és bàsica**: antivirus en tots els equips, tallafocs a la xarxa, SAI i còpies de seguretat diàries.
