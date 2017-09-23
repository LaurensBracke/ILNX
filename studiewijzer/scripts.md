# Systeembeheertaken automatiseren met scripts

## Leerdoelen

- De shell-omgeving gebruiken en aanpassen
    - Commando's (zie tabel hieronder)
    - Configuratiebestanden: `/etc/profile`, `~/.bash_profile`, `~/.bashrc`, `~/.bash_logout`
    - Variabelen in Bash: omgevingsvariabelen, shellvariabelen
- Eenvoudige scripts aanpassen en schrijven
    - Commando's: `for`, `of`, `read`, `seq`, `test`, `while`
    - Instellen van de script interpreter met de "shabang" (`#!`)
    - Scripts uitvoerbaar maken
    - Standaard Bash syntax, logische structuren (lussen en tests)
    - Parameters (positionele parameters `${0}`, `${1}`, `${2}`, enz. en speciale parameters `$#`, `$?`, `$*`, `$@`)
    - Commandosubstitutie (`$(commando)`)
    - Scripts debuggen en testen

Belangrijke commando's:

| Commando | Taak                                                |
| :---     | :---                                                |
| `export` | Stel een variabele in als een omgevingsvariabele    |
| `env`    | Toon de omgevingsvariabelen                         |
| `set`    | Bash-instellingen wijzigen (vb. `set -n`, `set -x`) |
| `unset`  | Verwijder de gespecifieerde variabele               |
| `alias`  | Definieer een "shortcut" voor een commando          |

## Voorbereiding

Het is belangrijk om de oefeningen in het boek van Cobbaut te maken die hieronder aangegeven worden!

- De shell-omgeving gebruiken en aanpassen
    - Werken met variabelen: Cobbaut hst III. 12. Variables, pp. 89-99
- Eenvoudige scripts aanpassen en schrijven
    - Cobbaut hst. VI. Scripts. pp. 156-185

## Sjabloon voor een Bash-script

Het gebruiken van een vaste structuur voor je scripts maakt het makkelijker te doorgronden en als je dit vastlegt als een sjabloon in je favoriete teksteditor (als die deze functionaliteit ondersteunt), kan helpen om snel een robuust script te schrijven. Hier komt het sjabloon (je kan het downloaden van <https://gist.github.com/bertvv/7727082>), daarna volgt wat uitleg.

```bash
#!/usr/bin/env bash
#
# Script name -- purpose
#
# Author: 

set -o errexit  # abort on nonzero exitstatus
set -o nounset  # abort on unbound variable
set -o pipefail # don't hide some errors in pipes

#
# Functions
#

usage() {
cat << _EOF_
Usage: ${0} 

_EOF_
}

#
# Variables
#

#
# Command line parsing
#

if [ "$#" -ne "1" ]; then
    echo "Expected 1 argument, got $#" >&2
    usage
    exit 2
fi

#
# Script proper
#

```

### De "shebang"

Op regel 1 wordt via de “shebang” of “hashbang” (= de karakters #!) aangegeven dat het om een Bash-script gaat. Voor Perl zou je `/usr/bin/env perl` kunnen schrijven. Zowel `#!/bin/bash` als `#!/usr/bin/env bash` komen in de praktijk voor. Met de eerste schrijfwijze wordt sowieso `/bin/bash` als interpreter gebruikt, in de andere wordt gezocht in de omgevingsvariabele `${PATH}` naar het commando `bash` dat het eerst voorkomt. Dit is iets flexibeler, want op sommige distributies kan het commando op een andere plaats staan (bv. `/usr/bin/bash`).

### Bash-instellingen voor robuustere scripts

De regels met `set -o [...]` helpen bij het voorkomen van vaak voorkomende fouten door de uitvoering van het script meteen af te breken in enkele gevallen:

- `set -o errexit`: van zodra een commando ergens in het script afsluit met een exit-status verschillend van 0 (dus als er iets misgelopen is)
- `set -o nounset`: als je de waarde van een variabele opvraagt die niet geïnitialiseerd is (standaard wordt die beschouwd als een lege string)
- `set -o pipefail`: wanneer de eerste commando's in een "pipe" (`cmd1 | cmd2 | cmd3`) falen wordt de pipe onderbroken

### Variabelen en functies

Het is best om variabelen vooraan in het script te definiëren. Geef variabelen een standaardwaarde die zin heeft voor het script.

Scripts zijn over het algemeen een stuk minder complex dan een volwaardige applicatie, maar een aantal principes die jullie in de programmeervakken meegekregen hebben, blijven ook hier gelden. Probeer in het bijzonder copy-paste-code te vermijden door die in te kapselen in functies (het DRY-principe, *don't repeat yourself*). Je kan functies ook vooraan in het script plaatsen. Hier is alvast een functie `usage` gedefinieerd die afdrukt hoe het commando gebruikt moet worden (met een *here document*). Vul de uitleg aan met specifieke uitleg over jouw script. Beschrijf ook de mogelijke opties en argumenten. De positionele parameter `${0}` staat voor de naam van het script.

### Het eigenlijke script

Helemaal onderaan komt de eigenlijke functionaliteit van het script. Het komt relatief vaak voor dat dit de aanroep van één commando is, of een “one-liner” van enkele commando’s met pipes (`|`) er tussen.

## Bash scripting tips en trucs

Er zijn op het net zeer veel voorbeelden van shell-scripts te vinden, wat hopelijk inspirerend kan werken. Maar er loopt een levendige discussie over wat een goede *stijl* is. Bash heeft niet altijd een voor de hand liggende syntax, dus stijl is belangrijk om er voor te zorgen dat scripts leesbaar blijven. Complexe en onleesbare scripts hebben meer kans op fouten.

Daarom geven we graag enkele tips mee die kunnen helpen bij het sneller schrijven van robuuste Bash scripts.

- Begin elk Bash-script met een "shebang"
- De voertaal bij het schrijven van scripts is Engels, zowel voor code, commentaar als uitvoer. Gebruik van Nederlands leidt tot een moeilijk leesbaar en verwarrend geheel in combinatie met de Engelse commando’s en syntax van Bash.
- Let op indentatie, en pas die consequent en strikt toe
    - Gebruik spaties, nooit tabs
    - Kies een indentatiebreedte en blijf er bij (typische keuze is 2)
    - Een goede teksteditor kan scripts automatisch correct indenteren. Vb. Vim: tik in normal mode `gg=G` in. `gg` gaat naar het begin van het bestand, `=` is het commando voor indenteren, `G` wil zeggen “tot aan het einde van het bestand”.
- Splits regels die te lang zijn (= 80 karakters). Je kan een commando splitsen door aan het einde van een regel een backslash (`\`) schrijven.
- Schrijf variabelen altijd als `${variabele}`, niet als `$variabele`. Bij de eerste notatie is duidelijker waar de variabelenaam eindigt, bijvoorbeeld als je die gebruikt binnen strings. Gebruik kleine letters in je eigen variabelen, zodat er duidelijk onderscheid is met shellvariabelen die buiten het script gedefinieerd zijn.
- Zet strings waar mogelijk tussen aanhalingstekens. Dit geldt in het bijzonder als die variabelen bevatten waar bv. bestandsnamen met spaties in voorkomen:

    ```console
    $ file='Mijn bestand'
    $ touch $file   # geen aanhalingstekens, dit loopt verkeerd
    $ ls –l
    total 0
    -rw-rw-r--. 1 bert bert 0 Dec  1 02:14 bestand
    -rw-rw-r--. 1 bert bert 0 Dec  1 02:14 Mijn
    $ touch "${file}"  # aanhalingstekens => correct
    $ ls –l
    total 0
    -rw-rw-r--. 1 bert bert 0 Dec  1 02:14 bestand
    -rw-rw-r--. 1 bert bert 0 Dec  1 02:14 Mijn
    -rw-rw-r--. 1 bert bert 0 Dec  1 02:14 Mijn bestand
    ```

- Gebruik bij **command substitution** de notatie `$(commando)` ipv omgekeerde aanhalingstekens (backquotes, backticks) ```commando```
- Als je tekst wil afdrukken over verschillende regels, gebruik dan geen herhaalde `echo`s, maar een *here document*. Dit maakt een script veel leesbaarder.

Als voorbeeld van een uitgebreidere stijlgids kan je deze van Google eens doornemen: <http://google-styleguide.googlecode.com/svn/trunk/shell.xml>

### Debuggen

- Schrijf eerst en vooral **niet te veel code ineens**. Begin met één of enkele commando's, test het script, bekijk de uitvoer, en breid het script uit.
- Test vóór het uitvoeren of de syntax van je script correct is met `bash -n SCRIPT`
- Als je script fouten bevat die je niet meteen vindt, kan het helpen om te loggen welke commando's *precies* uitgevoerd worden, na expansie. Dit kan met `bash -x SCRIPT`.
    - Als je enkel van één stuk code de debug-uitvoer wil bestuderen, dan kan je ervoor `set -x` schrijven en `set +x` erna.
- Installeer en gebruik ShellCheck. Dit is een zgn. statische code-analysetool die vaak voorkomende fouten in Bash scripts kan opsporen. Er bestaat een Vim-plugin, [syntastic](https://github.com/scrooloose/syntastic) die ShellCheck controles uitvoert telkens je opslaat.
