# 03 · Identificació dels recursos TIC

## 1. Punt de partida

Per a decidir quins recursos informàtics necessita Helbérica tenim en compte tres característiques de l'empresa:

- **Té 23 treballadors**, però la majoria (14) són operaris de producció que treballen a peu de màquina i no necessiten un ordinador propi.
- **Té dues instal·lacions a Xixona**: la fàbrica de galletes i barquillos, amb les oficines (Polígon Segorb), i la planta de xocolates (Polígon Espartal III). Les dues han d'estar connectades.
- **Treballa per a grans cadenes de supermercats amb certificació IFS**. Això obliga a registrar la **traçabilitat de cada lot** (matèries primeres, producció, controls de qualitat i expedició) i a guardar aquestes dades de manera segura.

> En aquesta fase només identifiquem els recursos. El disseny de la xarxa i el diagrama es faran en el Bloc 2.

## 2. Ordinadors i dispositius per departament

| Departament | Equip | Quantitat | Ús principal |
|-------------|-------|:---------:|--------------|
| Direcció general | Ordinador portàtil | 1 | Gestió, correu i reunions amb clients fora de l'empresa |
| Administració | Ordinador de sobretaula | 2 | Comptabilitat, facturació, compres i comandes (ERP) |
| Producció | Ordinador de sobretaula | 1 | Cap de producció: planificació i seguiment de la producció |
| Producció | Ordinador de sobretaula | 1 | Manteniment: registre d'avaries i manteniment preventiu |
| Producció | Terminal tàctil de planta | 2 | Un per fàbrica: registre de lots i producció a peu de línia |
| Qualitat | Ordinador de sobretaula | 2 | Registres de qualitat, traçabilitat i documentació IFS |
| Magatzem i logística | Ordinador de sobretaula | 1 | Cap de magatzem: inventari i expedicions |
| Magatzem i logística | Terminal portàtil amb lector de codis de barres (PDA) | 2 | Entrades i eixides de mercaderia lligades a cada lot |

**Total**: 1 portàtil, 7 ordinadors de sobretaula, 2 terminals de planta i 2 PDA.

### Justificació

- **No es dona un ordinador a cada operari**: els operaris treballen a les línies de producció. És més pràctic posar un **terminal tàctil compartit** a cada fàbrica, protegit contra la pols i fàcil de netejar, on registren els lots.
- **Les PDA del magatzem** permeten llegir els codis de barres dels palets i caixes. Així es registra automàticament què entra i què ix i a quin lot pertany, cosa necessària per a la traçabilitat.
- **El gerent té un portàtil** perquè es desplaça a reunions amb els clients.

## 3. Servidors

| Servidor | Quantitat | Funcions generals |
|----------|:---------:|-------------------|
| Servidor principal | 1 | Usuaris i permisos (domini), carpetes compartides per departament i base de dades del programa de gestió (ERP) i de traçabilitat |
| NAS de còpies de seguretat | 1 | Còpies de seguretat automàtiques del servidor |

### Justificació

- Un **únic servidor** és suficient per a una empresa de 23 treballadors i centralitza tota la informació en un lloc.
- El **NAS de còpies** és imprescindible: si es perden les dades de traçabilitat, l'empresa no pot demostrar d'on ve cada lot i podria perdre la certificació IFS i els clients.
- El servidor s'ubica a la **seu de Segorb**, on hi ha les oficines.

## 4. Dispositius de xarxa

| Dispositiu | Quantitat | Funció |
|------------|:---------:|--------|
| Router amb connexió de fibra | 2 | Un per instal·lació: accés a Internet i connexió segura (VPN) entre les dues fàbriques |
| Switch gestionable | 2 | Un per instal·lació: connectar ordinadors, servidor, impressores i punts d'accés |
| Punt d'accés Wi-Fi | 3 | Cobertura sense fil per a les PDA i el portàtil: 2 a Segorb (oficines i magatzem) i 1 a la planta de xocolates |
| SAI (sistema d'alimentació ininterrompuda) | 1 | Protegir el servidor, el NAS i el switch principal contra talls de llum |

### Justificació

- Com que hi ha **dues instal·lacions separades**, cada una necessita el seu router i el seu switch. La **VPN** entre els routers permet que la planta de xocolates treballe amb el mateix servidor que la seu.
- Els **punts d'accés** són necessaris perquè les PDA es mouen pel magatzem i no es poden connectar per cable.
- El **SAI** evita que un tall de llum apague de colp el servidor i corrompa les dades.

## 5. Impressores i altres perifèrics

| Perifèric | Quantitat | Departament | Funció |
|-----------|:---------:|-------------|--------|
| Impressora multifunció de xarxa | 1 | Administració (compartida) | Imprimir, escanejar i fotocopiar documents de tota l'oficina |
| Impressora d'etiquetes | 2 | Producció / Magatzem | Una per fàbrica: imprimir les etiquetes de lot i de palet amb codi de barres |
| Lector de codis de barres | 2 | Producció | Un per terminal de planta: llegir els codis de les matèries primeres que entren a la línia |

### Justificació

- Amb **una sola multifunció** per a l'oficina n'hi ha prou, perquè hi treballen poques persones.
- Les **impressores d'etiquetes** són imprescindibles en una fàbrica que treballa per a grans cadenes: cada caixa i cada palet ha d'eixir etiquetat amb el seu número de lot.

## 6. Resum

| Tipus de recurs | Total |
|-----------------|:-----:|
| Ordinadors (sobretaula + portàtil) | 8 |
| Terminals de planta | 2 |
| PDA amb lector | 2 |
| Servidors (servidor + NAS) | 2 |
| Routers | 2 |
| Switches | 2 |
| Punts d'accés | 3 |
| SAI | 1 |
| Impressores (multifunció + etiquetes) | 3 |
| Lectors de codis de barres | 2 |

Els recursos proposats són **senzills i ajustats** a una petita empresa industrial. Se centren en el que realment necessita Helbérica: **gestionar les comandes, controlar la producció i garantir la traçabilitat** que exigeixen els seus clients.
