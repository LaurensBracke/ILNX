# Labo 2: Linux leren kennen

## Hulp zoeken

1. Hoe vraag je op de command-line documentatie op voor het *commando* `passwd`?

    ```
    $ man passwd
    alle pagina's over hoe het passwoord te veranderen
    ```

2. Hoe vraag je documentatie op voor het *configuratiebestand* `/etc/passwd`?

    ```
    $ man /etc/passwd (.conf) of man 5 passwd (man -f passwd)
    documentatie bij configuratiebestand verschijnt
    ```

3. Hoe vraag je een lijst op van alle documentatie die de string `passwd` bevat?

    ```
    $ man -k passwd of apropos passwd
    alle pagina's met die string verschijnen in lijstvorm
    ```

## Werken op de command-line

1. Wat is de huidige datum en uur?

    ```
    $ date
    UITVOER
    ```

2. Wat is de huidige directory?

    ```
    $ pwd
    /home/lbracke
    ```

3. Toon de inhoud van de huidige directory. De uitvoer zou er ongeveer zo moeten uit zien:

    ```
    $ ls 
    Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
    ```

4. Toon de inhoud van de huidige directory, maar toon voor elk bestand meer informatie en ook "verborgen" bestanden.

    ```
    $ ls -al
    total 96
    drwx------. 14 student student 4096 Sep 24 09:14 .
    drwxr-xr-x.  3 root    root    4096 Sep 20 13:46 ..
    -rw-------.  1 student student  146 Sep 20 14:06 .bash_history
    -rw-r--r--.  1 student student   18 Mar 11  2013 .bash_logout
    -rw-r--r--.  1 student student  193 Mar 11  2013 .bash_profile
    -rw-r--r--.  1 student student  124 Mar 11  2013 .bashrc
    drwx------.  8 student student 4096 Sep 20 13:54 .cache
    drwxr-xr-x. 16 student student 4096 Sep 20 13:55 .config
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Desktop
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Documents
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Downloads
    [...]
    ```

5. Toon de inhoud van de hoofddirectory van het Linux-systeem, ook vaak de root-directory genoemd. Geef een uitgebreide listing zoals in de vorige vraag, maar *zonder* verborgen bestanden.

    ```
    $eerst cd /, dan ls ls -l
    
    ```

6. Wat betekenen volgende elementen van de uitvoer hierboven?
    - 1e kolom (bv. `drwxr-xr-x.`): de permissions die je hebt op deze map of file
    - 2e kolom (getal): wat er allemaal nog in die map zit qua bestanden of mappen/ 1:file 2ofmeer: map
    - 3e kolom (bv. `root`, `student`): de gebruiker van het bestand, of wie de file bezit
    - 4e kolom (bv. `root`): in welke groep de gebruiker zit
    - 5e kolom (getal): Grootte van het bestand in bytes
    - 6e - 8e kolom (datum): wanneer het laatst bewerkt is
    - de aanduiding `->` (bv. `bin -> usr/bin`): symbolische link
7. Hoe kan je commando's die je voordien uitgevoerd hebt terug ophalen (de "commandogeschiedenis")?

    ```
    $ pijltje terug naar boven tikken tot je het hebt
    ```

## De plaats van bestanden op een Linux-systeem

Vul de tabel hieronder aan. In de linkerkolom vind je de namen van een directory, in de rechter het soort bestanden dat er in thuis hoort.

| Directory                         | Inhoud                                                  |
| :---                              | :---                                                    |
| `/bin`, `/usr/bin`                | Uitvoerbare bestandjes voor gebruiker                   |
| '/sbin', '/usr/sbin               | Uitvoerbare bestanden voor systeembeheertaken           |
| `/var`                            | Variabele data (vb logs)                                |
| '/tmp'                            | Tijdelijke bestanden                                    |
| `/opt`, `/usr/local`              | Optionele software opslaan, die niet tot PM behoort     |
| '/root'                           | Home-directory van de `root` gebruiker                  |
| '/home/student'                   | Home-directory van de gebruiker `student`               |
| '/usr/share/man'                  | De inhoud van de man-pages                              |
| '/usr/share/doc'                  | Andere documentatie                                     |
| `/lib`, `/usr/lib`, `lib64`, enz. | Gedeelde bibliotheken van programma's die in bin staan  |
| 'run/media/...'                   | De inhoud van de installatie-cd voor Guest Additions(*) |
| `/dev`                            | Usb-opslag                                              |
| `/proc`                           | Kernel-info taakbeheer                                  |
| '/etc'                            | Systeemconfiguratiebestanden                            |

(*) Je kan het insteken van de cd simuleren in het VirtualBox-venster van je VM in het menu "Devices" > "Insert Guest Additions CD image..." (of het Nederlandstalige equivalent).


## Werken met bestanden en directories

Om het verschil tussen een bestand en directory te verduidelijken, wordt in wat volgt de naam van een directory telkens afgesloten met “/”.

### Directories

Open eerst een terminalvenster, start de oefening vanuit je eigen home-directory. Ga enkel naar een andere directory als dat expliciet gevraagd wordt. Geef telkens de gevraagde commando's niet alleen om de taak uit te voeren, maar ook om te testen of dit correct gebeurd is.

In deze oefening leer je onderscheid maken tussen *relatieve* en *absolute paden*. Een *absoluut* pad begint altijd met een `/`, wat overeenkomt met de root-directory. Een *relatief* pad geldt vanaf de huidige directory.

1. Blijf in je home-directory en maak van hieruit een directory `tijdelijk/` aan onder `/tmp/`

    ```
    $ mkdir /tmp/tijdelijk
    map tijdelijk is aangemaakt in tmp
    ```

2. Verwijder deze directory meteen

    ```
    $ rmdir /tmp/tijdelijk
    map is verwijderd
    ```

3. Maak onder je home-directory een submap aan met de naam `linux/`

    ```
    $ mkdir linux
    De submap is aangemaakt
    ```

4. Ga naar deze directory

    ```
    $ cd linux/
    je bent in de map linux van de home directory
    ```

5. Maak met één commando de subdirectory `a/b/` aan onder `linux/`. Als je nadien het commando `tree` geeft, moet je de gegeven uitvoer zien.

    ```
    $ mkdir a b
    UITVOER
    $ tree
    .
    └── a
    └── b
    2 directories, 0 files
    ```

6. Verwijder directory `b/` en daarna `a/` (in twee commando's)

    ```
    $ rmdir a/b en rmdir a
    ls is leeg voor die map
    ```

7. Maak met één commando deze directorystructuur aan.

    ```
    $ mkdir -p c/{d,e}
    UITVOER
    $ tree
    .
    └── c
        ├── d
        └── e
    3 directories, 0 files
    ```

8. Verwijder in één commando de directory `c/` en alle onderliggende

    ```
    $ rm -rf c of rmdir c/e c/d c
    UITVOER
    ```

9. Maak met één commando deze directorystructuur aan. Het is de bedoeling de opdrachtregel zo kort mogelijk te maken, dus niet alle directories apart opgeven!

    ```
    $ mkdir -p f/{g,h}/i
    UITVOER
    $ tree
    .
    └── f
        ├── g
        │   └── i
        └── h
            └── i

    5 directories, 0 files
    ```

Behoud deze directorystructuur voor de volgende oefeningen over bestanden.

### Bestanden

1. Maak een leeg bestand aan met de naam `file1`

    ```
    $ touch file1
    zorg ervoor dat je je in de juiste map bevindt natuurlijk
    ```

2. Maak een *verborgen* bestand aan met de naam `hidden`. Verborgen betekent dat je het niet kan zien met een "gewone" `ls`, maar wel met de gepaste optie.

    ```
    $ touch .hidden
    gebruik ls -a commando om hidden files te zien
    ```

3. Tik volgend commando in, leg uit wat er hier precies gebeurt, wat het effect is.

    ```
    $ echo hello world > file2"
    ```

    **Antwoord: Het maakt een compleet nieuw bestand aan met naam 'file2' en met daarin de zin 'hello world'** 

4. Toon de inhoud van `file2`

    ```
    $ less, cat file2
    hello world (gebruik q commando om af te sluiten)
    ```

5. Kopieer `file1` naar een nieuw bestand `file3` in de huidige directory

    ```
    $ cp file1 file3
    UITVOER
    ```

6. Kopieer `file1` naar de directory `f/` (die zou je nog moeten hebben van vorige oefening)

    ```
    $ cp file1 f/
    bestand zit in map f en map linux
    ```

7. Kopieer `file1` en file2 in één keer naar `f/g/`. Je zou de gegeven situatie moeten krijgen.

    ```
    $ cp file1 file2 f/g/  (gebruik cd .. om 1 map naar boven te gaan)
    UITVOER
    $ tree
    .
    ├── f
    │   ├── file1
    │   ├── g
    │   │   ├── file1
    │   │   ├── file2
    │   │   └── i
    │   └── h
    │       └── i
    ├── file1
    ├── file2
    └── file3
    ```

8. *Hernoem* `file3` naar `file4`

    ```
    $ mv file3 file4
    UITVOER
    ```

9. Verplaats `file2` naar directory `f/`

    ```
    $ mv file2 f/ ( gebruik 2x tab toets om mappensysteem te vinden)
    UITVOER
    ```

10. Verplaats `file1` en `file4` in één keer naar `f/h/`. Je zou de gegeven situatie moeten krijgen.

    ```
    $ mv file1 file4 f/h/
    UITVOER
    $ tree
    .
    └── f
    ├── file1
    ├── file2
    ├── g
    │   ├── file1
    │   ├── file2
    │   └── i
    └── h
        ├── file1
        ├── file4
        └── i

    5 directories, 6 files
    ```

11. Kopieer `f/h/`, inclusief de inhoud, naar een nieuwe directory `f/j/`

    ```
    $ cp -r f/h/ f/j/
    UITVOER
    ```

### Pathname expansion (of *file globbing*)

Creëer in de directory `linux/` een aantal lege bestanden met de naam `filea` t/m `filed`, `file1` t/m `file9` en `file10` t/m `file19`. Hier is een trucje om dat snel te doen:

```
[student@localhost ~/linux] $ touch filea fileb filec filed
[student@localhost ~/linux] $ for i in {1..19}; do touch "file${i}"; done 
[student@localhost ~/linux] $ ls 
f       file11  file14  file17  file2  file5  file8  fileb 
file1   file12  file15  file18  file3  file6  file9  filec 
file10  file13  file16  file19  file4  file7  filea  filed 
```

Toon met `ls` telkens de gevraagde bestanden, niet meer en niet minder.

1. Alle bestanden die beginnen met `file`

    ```
    $ ls file*
    file1 file2 file3 file4.......
    ```

2. Alle bestanden die beginnen met `file`, gevolgd door één letterteken (cijfer of letter)

    ```
    $ ls file[a-zA-Z0-9] of ls file?
    file1 file2 filea fileb filec
    ```

3. Alle bestanden die beginnen met `file`, gevolgd door één letter, maar geen cijfer

    ```
    $ ls file[a-z]
    filea fileb filec filed
    ```

4. Alle bestanden die beginnen met `file`, gevolgd door één cijfer, maar geen letter

    ```
    $ ls file[0-9]
    file1 file2 ... file9
    ```

5. De bestanden `file12` t/m `file16`

    ```
    $ ls file1[2-6]
    file12 file13 file14 file15 file16
    ```

6. Bestandern die beginnen met `file`, *niet* gevolgd door een `1`

    ```
    $ ls file[^1]*
    file2 file3 file8 file9 filea fileb filec
    ```

### Links

Maak in de directory `linux/` twee tekstbestanden aan, met naam `tekst1a` en `tekst2a`. Beide hebben als inhoud “Dit is bestand tekst1” en “Dit is bestand tekst2”, respectievelijk.

1. Voor het volgende commando uit en geef de uitvoer:   

    ```
    $ ls -l tekst*
    Gebruik gemaakt van touch en vim (met commando's i en ESC, en q en :wq om af te sluiten en op te slaan)
    -rw-rw-r--, 1 lbracke lbracke 22 2016-10-19 10:20 tekst1a
    -rw-rw-r--, 1 lbracke lbracke 22 2016-10-19 10:20 tekst2a
    ```

2. Maak een *harde link* van `tekst1a` naar `tekst1b`
3. Maak een *symbolische link* van `tekst2a` naar `tekst2b`
4. Voor het volgende commando uit en geef de uitvoer:

    ```
    $ ls -l tekst*
    eerst "ln tekst1a tekst1b" voor de harde link, dan "ln -s tekst2a tekst2b", en vervolgens commando hierboven
    -rw-rw-r--, 2 lbracke lbracke 22 2016-10-19 10:20 tekst1a
    -rw-rw-r--, 2 lbracke lbracke 22 2016-10-19 10:20 tekst1b
    -rw-rw-r--, 1 lbracke lbracke 22 2016-10-19 10:20 tekst2a
    lrwxrwxrwx, 1 lbracke lbracke  7 2016-10-19 10:26 tekst2b -> tekst2a
    ```

5. Hoe zie je aan de uitvoer van `ls` dat `tekst1b` een harde link is en `tekst2b` een symbolische? Tip: Vergelijk met de uitvoer uit vraag 1!

    **Antwoord**: tekst1b is exact op elk vlak hetzelfde als tekst1a, dus een exact kopie, niets verschilt. Tekst2b is eigenlijk een link naar het bestand tekst2a, dus als je op 2b klikt, ga je automatisch naar 2a!

6. Verwijder de oorspronkelijke bestanden, `tekst1a` en `tekst2a`. Maak het commando zo kort mogelijk!

    ```
    $ rm tekst[12]a
    dit kan gewoon, er wordt geen foutmelding weergegeven, zelfs al is het bestand waar 2b naar linkt nu verwijderd.
    ```

7. Toon opnieuw de uitvoer van `ls -l tekst*`, en bekijk de inhoud van `tekst1b` en `tekst2b`. Wat valt je op?

    ```
    $ ls -l tekst*
    -rw-rw-r--, 1 lbracke lbracke 22 2016-10-19 10:20 tekst2a
    lrwxrwxrwx, 1 lbracke lbracke  7 2016-10-19 10:26 tekst2b -> tekst2a (laatste 2 staan in rood!!!)
    ```

    **Antwoord**: Link zal niet meer werken, aangezien linkbestand tekst2a niet meer bestaat!

### Bestanden archiveren

1. Creëer in je home-directory een archief `linux.tar.bz2` van de directory `linux/` en alle inhoud.

    ```
    $ tar -cvjf linux.tar.bz2 /linux
    lijst van alles wat er in is opgeslagen
    ```

2. Verwijder nu volledig de directory `linux/`

    ```
    $ rm -rf linux/
    map verwijdert uit lbracke
    ```

3. Toon de inhoud van het archief zonder opnieuw uit te pakken

    ```
    $ tar -tjvf linux.tar.bz2
    lijst van alles wat in archief zit
    ```

4. Pak het archief opnieuw uit in je home-directory.

    ```
    $ tar -xjvf linux.tar.bz2
    UITVOER
    ```

