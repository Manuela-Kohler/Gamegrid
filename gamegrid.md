# Gamegrid - Objektorientierte Programmierung

**Ziel: Ein kleines Spiel programmieren**

## Spielvorschläge

### 1 Pacman-Labyrinth
Spielidee: <br>
Pacman wird durch das Spielfeld gesteuert und muss alle Orangen fressen, während er Geistern ausweicht. <br>

#### Pflicht-Anforderungen:
+ Spielfenster: 15x15 Zellen, 40 Pixel
+ Klasse `Pacman` (animiert, tastaturgesteuert)
+ Klasse `Orange`: 30 Orangen an zufälligen Positionen
+ Klasse `Ghost`: 2-3 Geister, die sich automatisch bewegen (mit `act()`-Methode)
+ Kollisionserkennung: Pacman frisst Orangen -> +1 Punkt
+ Kollisionserkennung: Geist berührt Pacman -> Game Over mit `setStatusText()` und `doPause()`
+ Punktezähler und Statusmeldungen
+ Gewinnmeldung bei allen gefressenen Orangen


#### Erweiterungen (Optional):
* Geister bewegen sich zufällig: `self.turn(random.randint(0,3)*90)` bei Rand
* Power-Orangen(grössere Orangen): Pacman kann 5 Sekunden lang Geister fressen
* Mehrere Leben: 3 Leben, bei Geist-Kollision -1 Leben
* Level-System: Level 2 mit mehr Geistern.

#### Hilfestellung:
`````
from gamegrid import *
import random

score = 0
totalPills = 30

class Pacman(Actor):
    def __init__(self):
        Actor.__init__(self, True, "sprites/pacman.gif", 2)
    
    def tryToEat(self):
        # Pillen fressen
        pass
    
    def checkGhost(self):
        # Geist-Kollision prüfen
        pass

class Pill(Actor):
    def __init__(self):
        Actor.__init__(self, "sprites/pill_0.gif")

class Ghost(Actor):
    def __init__(self):
        Actor.__init__(self, "sprites/ghost_0.gif")
    
    def act(self):
        self.move()
        # Randprüfung und zufällige Drehung
        pass

def keyCallback(e):
    # Tastatursteuerung
    paki.tryToEat()
    paki.checkGhost()

makeGameGrid(15, 15, 40, Color.black, False, keyPressed=keyCallback)
# Actors hinzufügen
show()
doRun()
`````

### 2 Fisch-Jagd
Spielidee: <br>
Ein grosser Fisch (vom Spieler gesteuert) jagt kleine Fische. Gleichzeitig muss er Haien ausweichen.

#### Pflicht-Anforderungen:
+ Spielfenster: 12x12, Hintergrundbild `"sprites/reef.gif"`
+ Klasse `BigFish` (tastaturgesteuert): `"sprites/nemo.gif"`(grösser skaliert)
+ Klasse `SmallFish`(bewegt sich automatisch): `"sprites/fish_0.gif"` mit Animation
+ Klasse `Shark`(bewegt sich automatisch): `"sprites/shark.gif"`
+ 10 kleine Fische, 2 Haie - alle bewegen sich automatisch
+ Kollision: BigFish frisst SmallFish -> + 1 Punkt
+ Kollision: Shark berührt BigFish -> Game Over
+ Punktezähler und Statusmeldungen
+ Gewinnmeldung bei 10 gefressenen Fischen

#### Erweiterungen (optional):
+ Haie verfolgen den grossen Fisch (siehe WebTigerPython Kapitel ["Verfolgung"](https://www.python-online.ch/index.php?inhalt_links=gamegrid/navigation.inc.php&inhalt_mitte=gamegrid/verfolgung.inc.php))
+ Neue Fische spawnen nach: Alle 5 Sekunden erscheint ein neuer Fisch
+ Geschwindigkeit erhöht sich: Nach 5 gefressenen Fischen wird alles schneller
+ Highscore-System mit Textdatei
+ Power-Up: Sternchen sammeln -> 5 Sekunden Unverwundbarkeit

#### Hilfestellung:
`````
from gamegrid import *

score = 0

class BigFish(Actor):
    def __init__(self):
        Actor.__init__(self, True, "sprites/nemo.gif", 2)
    
    def tryToEat(self):
        # SmallFish fressen
        pass
    
    def checkShark(self):
        # Hai-Kollision prüfen
        pass

class SmallFish(Actor):()
    def __init__(self):
        Actor.__init__(self, "sprites/fish_0.gif", 2)
    
    def act(self):
        self.move()
        self.showNextSprite()
        # Randprüfung
        pass

class Shark(Actor):
    def __init__(self):
        Actor.__init__(self, "sprites/shark.gif")
    
    def act(self):
        self.move()
        # Randprüfung
        pass

def keyCallback(e):
    # Tastatursteuerung
    bigFish.tryToEat()
    bigFish.checkShark()

makeGameGrid(12, 12, 50, Color.blue, "sprites/reef.gif", False, keyPressed=keyCallback)
# Actors hinzufügen
show()
doRun()
`````

### 3 Algen-Sammler
Spielidee: Ein Fisch wird mit den Cursortasten gesteuert und muss alle Algen im Meer einsammeln.

#### Pflicht-Anforderungen:
+ Spielfenster: 10x10, Hintergrundbild `"sprites/reef.gif"`
+ Klasse `Fish` (animiert): `"sprites/nemo.gif"`
+ Klasse `Alga`: `"sprites/alga.gif"`
+ 20 Algen an zufälligen Positionen
+ Tastatursteuerungen (4 Richtungen)
+ Punktezähler mit `"setStatusText()"`
+ Gewinnmeldung, wenn alle Algen gesammelt sind

#### Erweiterungen (optional):
+ Zeitlimit mit `addActor()` und einem Timer-Actor
+ Hindernisse (Steine mit `"sprites/rock.gif"`) einbauen - Fisch darf nicht durchschwimmen
+ Mehrere Level: Nach 20 Algen spawnen 30 neue
+ Hai-Gegner: Bei Berührung Game Over
+ Geschwindigkeitsbonus: Sammle alle Algen in unter 30 Sekunden.

#### Hilfestellung:
`````
# Grundgerüst
from gamegrid import *

score = 0
totalAlgae = 20

class Fish(Actor):
    def __init__(self):
        Actor.__init__(self, True, "sprites/nemo.gif", 2)
    
    def tryToEat(self):
        global score
        # Hier Code für Kollisionserkennung

class Alga(Actor):
    def __init__(self):
        Actor.__init__(self, "sprites/alga.gif")

def keyCallback(e):
    # Hier Code für Tastatursteuerung
    pass

makeGameGrid(10, 10, 60, Color.blue, "sprites/reef.gif", False, keyPressed=keyCallback)
# Hier Fish und Algen hinzufügen
show()
doRun()
`````


## Vorgehen

Gehe zum Tutorial über [Gamegrid](www.python-online.ch/gamegrid) der WebTigerPython-Distribution.
Arbeite die Tutorials zu:
+ [Spielfenster](https://www.python-online.ch/index.php?inhalt_links=gamegrid/navigation.inc.php&inhalt_mitte=gamegrid/spielfenster.inc.php)
+ [Actors](https://www.python-online.ch/index.php?inhalt_links=gamegrid/navigation.inc.php&inhalt_mitte=gamegrid/actors.inc.php) 
+ [Actors bewegen](https://www.python-online.ch/index.php?inhalt_links=gamegrid/navigation.inc.php&inhalt_mitte=gamegrid/bewegen.inc.php)
+ [Animierte Actors](https://www.python-online.ch/index.php?inhalt_links=gamegrid/navigation.inc.php&inhalt_mitte=gamegrid/animierteActors.inc.php)
+ [Kollisionen im Gitter](https://www.python-online.ch/index.php?inhalt_links=gamegrid/navigation.inc.php&inhalt_mitte=gamegrid/kollisionen.inc.php)
+ [Tastatursteuerung](https://www.python-online.ch/index.php?inhalt_links=gamegrid/navigation.inc.php&inhalt_mitte=gamegrid/keyevents.inc.php)

durch und implementiere die relevanten Bestandteile direkt in dein Spielprojekt.