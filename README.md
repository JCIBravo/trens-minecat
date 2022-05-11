# trens-minecat
Gestió d'informació i funcionament de trens al servidor de Minecraft.

## Pantalles

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

**ACTUALITZACIÓ:** Ara des-de de la nova versió (< 1.5.11) es obligatori que el tren tingui un prefix en el nom del tren, i un "tag d'estació" per que s'activin els cartells i no surtin els cartells de "sense parada".

Per exemple, si el codi del cartell (displaymanual, tercera linia) es ``EST3`` (o ``EST 3``), el tren ha de tenir un tag que sigui el codi (sense el número) -> ``EST``. En cas contrari, el cartell mostrará com si el tren no faci parad

Si passa un tren sense parada, es pot utilitzar el següent cartell:
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

###### 2:
_Pròximament_

###### 3:
![imatge](/imatges/manual/3.png)

###### 4:

![imatge](/imatges/manual/4.png)

###### 6:
![imatge](/imatges/manual/6.png)

Es pot configurar la imatge que es mostrarà quan no hi ha cap tren amb `/tm configurar displaymanual marca <nom>`. Opcions pel `<nom>` son `rodalies` o `renfe`.

Atenció! Per utilitzar aquest display cal configurar el número d'andana. Per fer-ho, agafa l'ítem del mapa amb la mà dreta i executa el comandament `/tm configurar displaymanual andana <número d'andana>`.

###### 7:
![imatge](/imatges/manual/7.png)


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

`/tm horn` Fa sonar el so definit a les propietats del tren com a `horn_nom.del.so`. També es pot executar amb un cartell `[train] horn`.

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

_Nota: en la majoria de paràmetres, excepte els noms del tren, els caràcters `_` són substituits per une espai._

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


#### displaymananual

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

```
[train]
noparadisplay
<nom del display>
<delay>
```

Igual que el displaymanual, però mostra un missatge a la pantalla que indica que el tren no pararà en aquesta estació.

#### updateservice

```
[train]
updateservice
```

Actualitza el servei d'un tren registrat, tenint en compte el nou nom i destinació.

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

- **FGC**
    - Barcelona-Vallés
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


    - Llobregat-Anoia
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


    - Lleida-La Pobla de Segur
        - RL1
            * NT: RL1_...
            * TT: FGC, RL1
        - RL2
            * NT: RL2_...
            * TT: FGC, RL2


_(Completar després)_
- **Rodalies de Catalunya**
    - Rodalia de Barcelona
        - R1
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
