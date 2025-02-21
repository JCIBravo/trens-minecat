# trens-minecat
Gestió d'informació i funcionament de trens al servidor de Minecraft.

| Index  |
|---|
| 1. [Pantalles programades](#pantalles-programades)  |
| ⠀1.1. [Models disponibles](#models-disponibles)  |
| 2. [Pantalles manuals](#pantalles-manuals)  |
| ⠀2.1. [Models disponibles](#models-disponibles-1)  |
| ⠀2.2. [Pantalles dinàmiques](#pantalles-dinàmiques)  |
| 3. [Pantalles de Signlink](#pantalles-de-signlink)  |
| ⠀3.1. [Models disponibles](#models-disponibles-2)  |
| 4. [Comandaments](#comandaments)  |
| 5. [Cartells Traincarts](#cartells-traincarts)  |
| ⠀5.1. [tagaudio](#tagaudio)  |
| ⠀5.2. [displaymanual](#displaymanual)  |
| ⠀5.3. [reiniciardisplay](#reiniciardisplay)  |
| ⠀5.4. [noparadisplay](#noparadisplay)  |
| ⠀5.5. [updateservice](#updateservice)  |
| ⠀5.6. [horn](#horn)  |
| ⠀5.7. [chime](#chime)  |
| 6. [Configuració](#configuració)  |
| 7. [Linies suportades](#linies-suportades)  |
| ⠀7.1. [FGC](#fgc)  |
| ⠀⠀7.1.1. [Barcelona - Vallès](#barcelona-vallès)  |
| ⠀⠀7.1.2. [Llobregat - Anoia](#llobregat-anoia)  |
| ⠀⠀7.1.3. [Lleida - La Pobla de Segur](#lleida-la-pobla-de-segur)  |
| ⠀7.2. [Renfe (WIP)](#renfe)  |
| ⠀⠀7.2.1. [Rodalies de Catalunya](#rodalies-de-catalunya)  |
| ⠀⠀⠀7.2.1.1. [Rodalia de Barcelona](#rodalia-de-barcelona)  |
| ⠀⠀⠀⠀7.2.1.1.1. [R1](#r1)  |
| ⠀⠀⠀⠀7.2.1.1.2. [R2](#r2)  |
| ⠀⠀⠀⠀⠀7.2.1.1.2.1 [R2](#r2-centre)  |
| ⠀⠀⠀⠀⠀7.2.1.1.2.2 [R2 Nord](#r2-nord)  |
| ⠀⠀⠀⠀⠀7.2.1.1.2.3 [R2 Sud](#r2-sud)  |
| ⠀⠀⠀⠀7.2.1.1.3. [R3 (Rodalia)](#r3)  |
| ⠀⠀⠀⠀7.2.1.1.4. [R4](#r4)  |
| ⠀⠀⠀⠀7.2.1.1.5. [R7](#r7)  |
| ⠀⠀⠀⠀7.2.1.1.6. [R8](#r8)  |
| ⠀⠀⠀⠀7.2.1.1.7. [R10](#r10)  |
| ⠀⠀⠀7.2.1.2. [Rodalia de Tarragona](#rodalia-de-tarragona)  |
| ⠀⠀⠀⠀7.2.1.2.1. [RT1](#rt1)  |
| ⠀⠀⠀⠀7.2.1.2.2. [RT2](#rt2)  |
|⠀ ⠀⠀7.2.1.3. [Rodalia de Girona](#rodalia-de-girona)  |
| ⠀⠀⠀⠀7.2.1.3.1. [RG1](#rg1)  |
| ⠀⠀7.2.2. [Rodalia València](#rodalia-valencia)  |
| ⠀⠀7.2.3. [Cercanías Alicante](#cercanias-alicante)  |
| ⠀⠀7.2.4. [Altres serveis](#altres-serveis)  |
| ⠀⠀⠀7.2.4.1. [Regionals i Mitja Distància](#regionals-i-mitja-distància)  |
| ⠀⠀⠀7.2.4.2. [Llarga Distància](#regionals-i-mitja-distància)  |
| 8. [Suport](#suport)  |

## Pantalles programades

`/tm crear pantalla <model> <pantalla> <nom>`
  - `model` Número de model de pantalla que es vol utilitzar.
  - `pantalla` Plantilla de línies de tren que es vol utilitzar. Veure apartat [Configuració](#Configuració) per a més informació. 
  - `nom` Nom de l'estació que es mostra a la pantalla. Només és visible en certs models.

#### Models disponibles:
_Els models 1 i 2 provenen de versions antigues i probablement desapareixeran en el futur, per la qual cosa no s'haurien d'utilitzar._
###### 1: 
![imatge](/imatges/1.png)

###### 2:
![imatge](/imatges/2.png)

###### 3:
![imatge](/imatges/3a.png)

###### 4:
![imatge](/imatges/4.png)

###### 5:
![imatge](/imatges/5.png)

_Imatge 5: JCIBravo_


## Pantalles Manuals

Visualment són iguals que les pantalles normals però la informació no s'actualitza mitjançant un horari sinó amb cartells Traincarts personalitzats.

Per actualitzar la seva informació cal col·locar un cartell Traincarts amb la següent informació:
```
[train]
displaymanual
<nom de la pantalla> <via (opcional)>
<delay>
```

La pantalla s'actualitzarà quan s'activi el cartell o un tren passi per sobre i el cartell estigui activat. La tercera línia es refereix al camp `<nom>` del comandament per aconseguir una pantalla i la quarta és un delay opcional (en segons), al cap del qual es reiniciarà la pantalla. (fins i tot sense un cartell `reiniciardisplay`)

Per generar una pantalla, caldrà utilitzar el comandament `/tm crear displaymanual <model> <nom>`, on el nom ha de coincidir amb el del cartell Traincarts.


**ACTUALITZACIÓ:** Ara des-de de la nova versió (< 1.5.11) es obligatori que el tren tingui un prefix que sigui [el nom de la linia i el seu tag (especialment pels displays de FGC)](#Linies Suportades), i un "tag d'estació" per que s'activin els cartells i no surtin els cartells de "sense parada".

Per exemple, si el codi del cartell (displaymanual, tercera linia) es ``EST3`` (o ``EST 3``), el tren ha de tenir un tag que sigui el codi (sense el número) -> ``EST``. En cas contrari, el cartell mostrará com si el tren no faci parada.


Si passa un tren sense parada, es pot utilitzar el següent cartell **(només funciona amb versions anteriors a la 1.15.11)**:
```
[train]
noparadisplay
<nom de la pantalla>
```

#### Models disponibles:

###### 1:
_És exactament igual visualment que el model 3 de pantalla normal, però no mostrarà mai el temps fins al pròxim tren._

![imatge](/imatges/3a.png)

Es pot configurar la imatge que es mostrarà quan no hi ha cap tren amb `/tm configurar displaymanual marca <nom>`. Opcions pel `<nom>` son `rodalies` o `renfe`.

_Aquestos displays seràn taronges si la marca es ``rodalies`` [ja que la majoria d'estacions tenen els displays així]() i en blanc si la marca es ``renfe``._

###### 2:
_Pròximament_

###### 3:
![imatge](/imatges/manual/3.png)

###### 4:

![imatge](/imatges/manual/4.png)

###### 5:

![imatge](/imatges/manual/5.png)

###### 6:
![imatge](/imatges/manual/6.png)

Es pot configurar la imatge que es mostrarà quan no hi ha cap tren amb `/tm configurar displaymanual marca <nom>`. Opcions pel `<nom>` son `rodalies` o `renfe`.

Atenció! Per utilitzar aquestos displays cal configurar el número d'andana. Per fer-ho, agafa l'ítem del mapa amb la mà dreta i executa el comandament `/tm configurar displaymanual andana <número d'andana>`.

###### 7:
![imatge](/imatges/manual/7.png)

#### 8
###### 8A:
![imatge](/imatges/manual/8A.png)

###### 8B:
![imatge](/imatges/manual/8.png)


#### Pantalles dinàmiques

Des de la versió 1.4, les pantalles es poden actualitzar amb informació en temps real proporcionada pels cartells `displaymanual` (encara que la informació no es mostri a cap pantalla manual).

Per fer-ho, cal prèviament registrar la línia a l'arxiu `stationList.yml`. La sintaxi per registrar una línia és la següent:
```yaml
lines:
  <nom de la línia> <destinació>|<interval entre trens (en segons)>:
    - <codi d'estació>|<temps des del spawn>
    - <altre codi d'estació>|<temps des del spawn>
```
Exemple:
```yaml
lines:
  R2 Aeroport|500:
    - Sant_Celoni|30
    - Palautordera|64
  #  ...
  R2 Sant_Celoni|500:
    - Aeroport|0
    - El_Prat|48
  #  ...
```

També cal crear les plantilles per les pantalles que es volen utilitzar (igual que en les pantalles automàtiques normals). Es pot trobar tota la informació a l'arxiu configuració.

Per registrar un tren, i que les pantalles actualitzin la seva hora d'arribada tenint en compte la seva posició, cal crear-lo amb el comandament [`/spawntrain`](#Comandaments).

## Pantalles de SignLink

Contenen una variable signlink configurable que s'actualitza cada tick.


#### Models disponibles

###### 1:

![imatge](/imatges/signlink/1.png)

Per actualitzar el nom de la variable: `/tm configurar sldisplay variable <nom>`
Per actualitzar la destinació mostrada al cartell: `/tm configurar sldisplay destinacio <nom>`

## Comandaments

`/tm crear pantalla <model> <plantilla> <nom>` Veure [Pantalles](#Pantalles).

`/tm crear displaymanual <model> <nom>` Veure [Pantalles Manuals](#Pantalles-Manuals).

`/tm configurar displaymanual <paràmetre> <valor>` Configura un paràmetre específic de la pantalla.

`/tm recarregar` Recarregar la configuració.

`/tm spawn <món> <x> <y> <z>` Genera un tren a les coordenades especificades. Aquestes coordenades han de ser les d'un cartell `spawner`, i no les de la via on ha d'aparèixer un tren.

`/tm horn` Fa sonar la botzina definit a les propietats del tren com a `horn_nom.del.so`. També es pot executar amb un cartell `[train] horn`.

~~`/tm chime` Fa sonar el so del timbre definit a les propietats del tren com a `chime_nom.del.so`. També es pot executar amb un cartell `[train] chime`.~~
_(Molt aviat)_

`/tm crear estatdelservei` Crea una pantalla gran amb totes les línies. Es pot posar un text personalitzat amb `/var edit <nom> set <valor>`

`/tm actualitzarestat` Actualitza l'estat del servei quan s'ha modificat una variable.

`/tm spawntrain -n [nom] -d [dest] -s [defaults] -h [n|s|w|e] [-o] [-l] [-r] <tren> <mon> <x> <y> <z>` Spawneja un tren en un bloc de rail qualsevol. 
```
-d,--destination <destination>   destinació del tren
-h,--heading <heading>           intenta fer aparèixer el tren cap a una direcció (n/s/e/w)
-l,--launch                      intenta accelerar el tren en la direcció -h
-n,--name <name>                 nom del tren
-o,--dontround                   no arrodoneixis el temps de spawneig. Obligatori -d -n -r
-r,--register                    registra el tren al TrainTracker. Obligatori -d -n
-s,--setdefaults <defaults>      defaults del tren
```

`/tm iteminfo` Obté informació de l'ítem agafat amb la mà (funciona només amb mapDisplays i ítems que tinguin tags).

_Nota: en la majoria de paràmetres, excepte els noms del tren, els caràcters `_` són substituits per un espai._

## Cartells Traincarts

#### tagaudio
```
[train]
tagaudio
<nom>
<delay>
```
Reprodueix un so quan el tren passa per sobre el cartell. `<nom>` pot ser el nom de so o un àlias que es pot relacionar amb un tag al tren amb la sintaxi `tagaudio|alias|nom.del.so.real`. Substituint `tagaudio` per `tagadio in` el so només es reprodueix dins el tren.

Es pot especificar, opcionalment, un delay que s'esperarà abans de reproduir el so.


#### displaymanual

```
[train]
displaymanual
<nom del display>
<delay>
```

Actualitza un `displaymanual` amb informació sobre el tren que executa el cartell. Es pot afegir, opcionalment, un retard passat el qual es reiniciarà la pantalla.

#### reiniciardisplay

```
[train]
reiniciardisplay
<nom del display>
```

Reinicia un `displaymanual`, deixant de mostrar informació sobre el tren i passant a la visualització predeterminada.

#### noparadisplay
***AVÍS: (Aquest cartell ja no funciona des-de la versió 1.5.11)***

```
[train]
noparadisplay
<nom del display>
<delay>
```

Igual que el displaymanual, però mostra un missatge a la pantalla que indica que el tren no pararà en aquesta estació.
_(S'espera eliminar aquest cartell en la versió 1.5.12)_

#### updateservice

```
[train]
updateservice
```

Actualitza el servei d'un tren registrat, tenint en compte el nou nom i destinació.

#### horn

```
[train]
horn
```

Fa sonar la bocina del tren. Per afegir la bocina al tren, has de posar al tren el tag ``horn_nom.del.so``. En cas de no tenir cap so configurat, no sona res.

#### chime

```
[train]
chime
```

***(Molt aviat)***
Fa sonar el timbre del tren. Per afegir la timbre al tren, has de posar al tren el tag ``chime_nom.del.so``. En cas de no tenir cap so configurat, no sona res.


## Configuració

A la configuració es defineixen certes variables globals i les plantilles disponibles amb línies de tren per utilitzar. La configuració d'exemple és la següent:

```yaml
#Temps (en ticks) que el plugin esperarà abans de destruir trens que hagin estat aturats. 0 desactiva la funció.
destruir-trens-en: 0

#Els trens que tinguin aquest tag no seran afectats per la configuració anterior i, per tant, no es destruiran mai.
no-destrueixis: nodestrueixis

#Els trens que tinguin aquest tag no es mostraran a l'api (/gettrains).
no-api: noapi

#Temps mínim (en segons) que es mostrarà a les pantalles. Si el temps fins al proper tren és menor que això es mostrarà
#un missatge personalitzable a cada pantalla, com "ara" o "imminent"
temps-minim-en-pantalla: 20

#pantalles d'informació que es poden utilitzar. El nom de la pantalla és el que s'utilitzarà en el comandament per
#generar-la.
#
#Format de les pantalles:
#  <nom>:
#    longitud: <longitud>
#    línies:
#      - <nom>|<expressió cron>|<destinació>|<via>|<observacions>
#
# [tots els camps són obligatoris, encara que no s'hagin d'utilitzar]
# [no es pot afegir un espai al voltant de '|', ja que s'estaria afegint al camp corresponent]

pantalles:
  exemple:
    longitud: 5
    linies:
      - R2N|45 2/10 * * * *|Sant Celoni|2|Para a totes les estacions
      - R2N|12 8/10 * * * *|Aeroport|2|Para a totes les estacions
```

## Linies suportades

A continuació, les linies que suporten en aquest plugin
* NT: Nom del tren (``/train name NT``)
* TT: Tag que necessita el tren (``/train addtag TT``)
    - _(Pot ser que en algunes linies necessitin més d'un tag, en aquest cas, el separarè amb una coma)_

#### **FGC**
###### Barcelona-Vallès
- L6
    * NT: L6_...
    * TT: FGC, L6
- L7
    * NT: L7_...
    * TT: FGC, L7
- L12
    * NT: L12_...
    * TT: FGC, L12
- S1
    * NT: S1_...
    * TT: FGC, S1
- S2
    * NT: S2_...
    * TT: FGC, S2
- S5
    * NT: S5_...
    * TT: FGC, S5
- S6
    * NT: S6_...
    * TT: FGC, S6
- S7
    * NT: S7_...
    * TT: FGC, S7


###### Llobregat-Anoia
- L8
    * NT: L8_...
    * TT: FGC, L8
- S3
    * NT: S3_...
    * TT: FGC, S3
- S4
    * NT: S4_...
    * TT: FGC, S4
- S8
    * NT: S8_...
    * TT: FGC, S8
- R5
    * NT: R5_...
    * TT: FGC, R5
- R50
    * NT: R50_...
    * TT: FGC, R50
- R6
    * NT: R6_...
    * TT: FGC, R6
- R60
    * NT: R60_...
    * TT: FGC, R60


###### Lleida-La Pobla de Segur
- RL1
    * NT: RL1_...
    * TT: FGC, RL1
- RL2
    * NT: RL2_...
    * TT: FGC, RL2


_(Completar després)_
### Renfe
#### Rodalies de Catalunya
##### Rodalia de Barcelona
###### R1
- *Servei A*
    * NT: R1_ServeiA
    * TT: R1, R1A
- *Servei B*
    * NT: R1_ServeiB
    * TT: R1, R1B
- *Servei C*
    * NT: R1_ServeiC
    * TT: R1, R1C


## Suport

Degut a que aquest plugin s'ha fet exclusivament pel [servidor de Minecraft de MineCat](http://twitter.com/MineCatOficial), <ins>no oferim cap support a cap altre servidor que tingui problemes amb aquest plugin.</ins> No obstant això, pot fer un ``git clone`` i refer el plugin per adaptar-ho al seu servidor.
