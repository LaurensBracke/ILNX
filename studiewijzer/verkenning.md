# Linux leren kennen

## Leerdoelen

- Hulp zoeken
- Werken op de command line
- De plaats van bestanden op een Linux-systeem
- Werken met bestanden en directories
- Bestanden bewerken met een teksteditor

## Voorbereiding

- Hulp zoeken
    - Cobbaut, hst II.5, "man-pages"
    - <http://explainshell.com/>: op deze website kan je een commando intikken met opties, enz. en je krijgt de relevante delen van de man-page te zien.
    - <https://linux.die.net/man/>: een uitgebreide verzameling Linux man-pages online.
    - Als je in Google "man COMMANDO" ingeeft, vind je ook snel de man-page terug.
- Werken op de command line
    - Zie verder in de sectie "De tekstconsole"
- De plaats van bestanden op een Linux-systeem
    - Cobbaut, Hst II.9, “the Linux file tree”
- Werken met bestanden en directories
    - Screencast “Werken met bestanden en directories”, <http://youtu.be/QChM_j8RsWA>
    - Cobbaut, Hst II.6, “Working with directories”
    - Cobbaut, Hst II.7, “Working with files”
- Bestanden bewerken met een teksteditor
    - Zie verder in de sectie "Linux teksteditors"
    - Cobbaut, Hst V.18, "Introduction to Vi"

## Agenda

Week 3:

- Overlopen eventuele nog niet opgeloste problemen vorige week
- Toelichting nieuwe opdracht
- Werken aan nieuwe opdracht, individuele remediëring

Week 4

- Overlopen eventuele nog niet opgeloste problemen vorige week
- Werken aan de opdracht, individuele remediëring

## Achtergrondinformatie

### De tekstconsole

Wanneer je in Linux een tekstconsole opent (bv. via het programma *Terminal*), kom je terecht in de zgn. Bash shell. Bash (*Bourne Again Shell*) is een commando-interpreter die op de meeste distributies van Linux en ook op MacOS X (zij het in dat geval een oude versie) als standaard geïnstalleerd staat. Ook op Windows is Bash beschikbaar, hetzij via [Cygwin](https://www.cygwin.com/), het versiebeheersysteem Git ([Git Bash](https://git-for-windows.github.io/)), of [Ubuntu for Windows](https://insights.ubuntu.com/2016/03/30/ubuntu-on-windows-the-ubuntu-userspace-for-windows-developers/).

De eerste versie van Bash dateert van 1989 en het is zelf gebaseerd op de nog oudere *Bourne Shell* (1976; genaamd naar de oorspronkelijke auteur).

Bash omvat enerzijds een interactieve prompt, maar is anderzijds ook een krachtige scripting-taal voor het automatiseren van systeembeheertaken of verwerken van (tekst-)data.

Een goed begrip van de werking van de commandoprompt is essentieel om productief te kunnen werken op een Linux-systeem. Eerst en vooral, de structuur van een opdrachtregel ziet er als volgt uit:

```console
$ COMMANDO [OPTIE]... [ARGUMENT]...
```

- Het dollarteken, de prompt, geeft aan dat Bash klaar is om invoer van de gebruiker te ontvangen. Wanneer je aangemeld bent als `root`, dan krijg je in de plaats een hekje `#` te zien. Je kan het uitzicht van deze prompt naar eigen wens aanpassen (bv. tonen van de huidige directory, gebruiker, hostnaam, kleuren gebruiken, enz.).
- Het eerste woord van de opdrachtregel is het uit te voeren `COMMANDO`. Hieronder meer daarover. **Merk op dat spaties belangrijk zijn!** Het einde van het commando wordt aangegeven door de *eerste spatie*. Cijfers en sommige leestekens zijn toegelaten in commandonamen.
- Na het commando volgen de opties, die het gedrag van het commando wijzigen. Opties beginnen met `-` of `--`. Hieronder meer daarover.
- Tenslotte volgen de argumenten. Dit zijn de "objecten" waarop het commando wordt uitgevoerd. Heel vaak gaat het over bestanden.
- Wanneer je `<Enter>` indrukt, wordt de opdrachtregel afgesloten en zal Bash die interpreteren voordat het opgegeven commando effectief uitgevoerd word, zal Bash eerst nog zgn. expansie proberen toepassen, bv. het vervangen van een variabele door de waarde. Hieronder meer daarover.
- De rechte haken rond `[OPTIE]` en `[ARGUMENT]` geven aan dat dit optioneel is, dat je dus niet verplicht bent een optie of argument op te geven. De drie punten `...` geven aan dat je er meerdere mag opgeven. Deze notatie wordt ook gebruikt in de man-pages.

#### Commando's

Wanneer je een commando invoert na de prompt, zal Bash op de volgende manier te werk gaan om dit uit te voeren:

- Eerst wordt nagegaan of het gaat over een ingebouwd commando van Bash, zoals `alias`, `set`, `exit`, enz. Zie `man builtins`.
- Vervolgens zal Bash zoeken in een aantal vastgelegde directories (vastgelegd in de *omgevingsvariabele* `${PATH}`) naar een uitvoerbaar (executable) bestand met dezelfde naam als het opgegeven commando. Als het gevonden wordt, zal Bash het opstarten, of zoniet een foutboodschap afdrukken.

Zo toon je de inhoud van de omgevingsvariabele `${PATH}` (kan er voor jouw systeem anders uitzien):

```console
$ echo ${PATH}
/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin
```

Met het commando `which` kan je opzoeken of een bepaald commando beschikbaar is op je Linux-systeem:

```console
$ which ls
/usr/bin/ls
$ which foo
/usr/bin/which: no foo in (/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin)
$ foo
bash: foo: command not found
```

#### Opties

Bij de meeste commando's kan je het gedrag wijzigen als je opties meegeeft. De twee meest voorkomende notaties zijn:

- *Korte opties*, een `-` gevolgd door een letter, bv. `-a`, `-h`, `-?`, enz.
    - Korte opties kunnen aan elkaar geschreven worden, bv. `-a -b -c` is hetzelfde als `-abc`.
- *Lange opties,** een `--` gevolgd door een woord, bv. `--all`, `--dry-run`, `--help`, `--verbose`, enz.

Opties kunnen zelf ook argumenten hebben. In de man-page van het commando kan je opzoeken wanneer een optie een argument nodig heeft of optioneel toelaat.

- Meestal komt er een spatie tussen optie en argument, bv. `git commit -m 'tikfouten verbeterd'`
- Soms wordt er *geen* spatie verwacht, bv. `cut -d:`
- Bij lange opties wordt er vaak een `=` tussen optie en argument geschreven, bv. `head --lines=15`

Dit hangt allemaal af van commando tot commando. Lees altijd de man-page! Sommige commando's volgen immers de conventies niet en hanteren een specifieke syntax.

#### Expansie

Expansie omvat de verschillende manieren waarop de Bash interpreter de commandoregel herschrijft voordat het effectief uitgevoerd wordt. Er zijn maar liefst zeven vormen van expansie, die hieronder opgesomd worden. Het is niet nodig om "van buiten" te leren welke vormen er zijn en in welke volgorde die toegepast worden, maar het is wel belangrijk dat je *begrijpt* hoe dit werkt.

- *Brace expansion:* een verkorte notatie met accolades, bv. `a{b,c,d}e` wordt omgezet in `abe ace ade`.
- *Tilde expansion:* een tilde `~` wordt omgezet in het volledige pad van de home-directory van de huidige gebruiker.
- *Parameter expansion:* expressies van de vorm `${PARAMETER}` hebben specifieke betekenissen. Enkele voorbeelden:
    - `${naam}` wordt vervangen door de waarde van de variabele `naam`
    - `${naam:=waarde}`: als de variabele `naam` nog geen waarde heeft, geef ze dan nu de waarde `waarde`
    - `${naam#patroon}`: verwijder `patroon` van het *begin* van de waarde van de variabele `naam`
    - ...
- *Command substitution:* een expressie van de vorm `$(commando)` wordt vervangen door de uitvoer van het opgegeven commando tussen de haaktjes (opties en argumenten zijn toegelaten)
- *Arithmetic expansion:* rekenkundige expressies van de vorm `$(( expressie ))` worden uitgerekend
- *Process substitution:* hiermee kan je de uitvoer van een commando gebruiken als de invoer van een ander commando (later meer hierover in het hoofdstuk over *redirection*).
- *Word splitting:* de commandoregel, na toepassen van de vorige types van expansie, wordt opgesplitst in verschillende "woorden". Elk woord wordt als een aparte optie/argument beschouwd. Normaal geldt de spatie als het splitsingsteken, maar je kan dit ook instellen (via de shellvariabele `${IFS}`).
- *Filename expansion:* tenslotte worden "wildcards" in bestandsnamen verwerkt (bv. `*`, `?`, `[...]`). Later in de cursus wordt dit in meer detail besproken

Pas na toepassen van al deze expansieregels wordt het commando effectief uitgevoerd. Je kan het resultaat van expansie door de shell bekijken. Na uitvoeren van het commando `set -x` wordt telkens de resulterende commandoregel getoond. Met `set +x` zet je dit terug uit.

### Linux texteditors

ls er iets is waar Linux goed in is, dan is het wel het manipuleren van tekst. De volledige configuratie van een Linux-systeem zit vervat in tekstbestanden (die je kan vinden in de `/etc/`-directory). Verder is Linux gebouwd voor en door programmeurs (wat ook vooral een tekst-gebaseerde bezigheid is) die voor zichzelf de beste tools ontwikkeld hebben om met tekst om te gaan. In hoofdstuk 4 bespreken we enkele command-line tools om tekst te bekijken en te bewerken, maar hier hebben we het alvast over de belangrijkste teksteditors, in het bijzonder Gedit, Nano en Vim. Er zijn er nog veel meer, maar als je met deze drie kan werken, kom je al heel ver.

#### Gedit

*Gedit* is de afkorting van *Gnome editor*, en is de standaard teksteditor voor de grafische omgeving Gnome Shell en ook in Fedora. Gedit heeft syntax-markering in kleur voor de meeste bestandstypes en je kan de functionaliteit van de editor ook uitbreiden a.h.v. plugins. In de Windows-wereld kan je hem waarschijnlijk het best vergelijken met Notepad++, alhoewel Gedit zonder plugins misschien niet dezelfde functionaliteit heeft. Verder valt hier niet veel over te vertellen, Gedit gedraagt zich zoals een teksteditor onder Windows, en je kan ongeveer dezelfde toetsenbordcombinaties gebruiken: opslaan met `Ctrl+S`, kopieren met `Ctrl+C`, plakken met `Ctrl+V`, enz.

#### Nano

*Nano* is een editor die je in een terminalvenster gebruikt, en wellicht ook de meest toegankelijke. Nano probeert zo eenvoudig mogelijk te zijn, dus is vrij beperkt qua functionaliteit. De belangrijkste toetsenbordcombinaties worden steeds onderaan afgebeeld, dus je kan er snel mee aan de slag (bv. `^X` staat voor `Ctrl-X`). Standaard is er geen syntax-markering, maar die kan je wel aanzetten door het configuratiebestand `/etc/nanorc` aan te passen.

Je opent een bestand (in de huidige directory) met het commando:

```console
$ nano BESTANDSNAAM
```

#### Vim

Vim staat voor *Vi IMproved*, dus een verbeterde versie van Vi. Die laatste is een afkorting van *vi*sual [editor]. Dit is een van de oudste editors in de UNIX-wereld en dateert van 1976. Dat heeft twee gevolgen. Enerzijds is Vi of Vim op vrijwel elke variant van Linux en UNIX geïnstalleerd, dus het is een van de meest universele editors van het platform. Anderzijds is deze geschreven in een tijdperk waar er heel andere opvattingen waren over gebruiksvriendelijkheid... In de praktijk komt het erop neer dat Vi bijzonder krachtig en uitgebreid is, met tientallen beschikbare add-ons, maar dat het niet evident is om er mee aan de slag te gaan. We geven hier enkele tips waarmee je je al kan behelpen. Met de ingebouwde help-functie, de interactieve les (via het commando `vimtutor`), en de massa’s informatie die je op het Internet hierover vindt, kan je je in de loop van de tijd verder bekwamen.

Je start Vi op dezelfde manier als Nano, dus vanop de commandline, met het te openen bestand als argument:

```console
vim BESTAND
```

Een eerste belangrijk concept dat je moet vatten voordat je met Vim aan de slag gaat is dat van de modi. Wanneer je Vim opstart, kom je terecht in de zgn. *normal mode*. In deze modus kan je commando’s geven (zoals opslaan, Vim verlaten, sorteren, enz.), maar geen tekst invoeren. Daarvoor moet je eerst naar *insert mode* overgaan, wat o.a. kan met het commando `i`. Onderaan het venster verschijnt dan de melding `---INSERT---`, het teken dat je kan tekst invoeren. In deze insert mode kan je niet meteen Vim verlaten. Om dan terug te gaan naar normal mode, druk je `[Esc]` in.

In onderstaande tabel vind je een kort overzichtje van de belangrijkste commando’s waar je alvast mee aan de slag kan. Deze gelden allemaal voor normal mode. Als je in insert mode zit, moet je dus eerst `[Esc]` in drukken.

| **Taak**                      | **Commando/sneltoets** |
| :---                          | :---                   |
| Opslaan                       | `:w`                   |
| Opslaan en afsluiten          | `:wq` of `zz`          |
| Afsluiten zonder opslaan      | `:q!`                  |
| Naar *insert mode* overgaan   | `i`                    |
| Een regel knippen             | `dd`                   |
| Een regel kopiëren            | `yy`                   |
| Plakken (na de cursor)        | `p`                    |
| Plakken (op de cursorpositie) | `P`                    |
| Zoeken naar PATROON (regex)   | `/PATROON[Enter]`      |
| Vorige/volgende zoeken        | `N` / `n`              |

Voor een lijstje met nog meer commando's, ga eens kijken naar <https://github.com/bertvv/cheat-sheets/blob/master/src/Vim.md>.

### Tekstbestanden bekijken

Naast deze teksteditors zijn er ook enkele commando’s die nuttig zijn voor het bekijken van tekstbestanden zonder ze te bewerken: cat en less.

Met `cat BESTAND` druk je de inhoud van BESTAND af op de terminal. Dit is perfect voor kleine bestandjes, maar voor grote stukken tekst die meer dan één scherm innemen is cat minder geschikt.

Met `less BESTAND` kan je bestanden openen om te bekijken, pagina per pagina. Je kan naar boven en beneden met de pijltjes, spatiebalk, `[PgUp]` en `[PgDn]`. Er is ook een zoekfunctie die werkt zoals die in Vim: `/STRING`. Je kan less verlaten met de `q` toets. Met `h` open je de help-functie.
