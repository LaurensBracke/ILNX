# Labo 1: Linux installeren

## VirtualBox installeren en een nieuwe VM aanmaken

1. Download en installeer de laatste versie van VirtualBox. Als je werkt op een van de klaspc's (campus Gent), dan is VirtualBox al geïnstalleerd.
2. Maak een nieuwe virtuele machine aan om straks Linux in te installeren. Let er op dat je volgende instellingen voorziet:
    - Als je op een klaspc werkt is de naam van je VM je eigen naam, bv. PietPieters
    - Het type van de VM is “Linux”, de versie “Fedora (64 bit)”
    - RAM: minstens 1024MB
    - Virtuele harde schijf van ~20GB, dynamisch
    - Videogeheugen: zoveel mogelijk (128MB)
    - 3D acceleration aanzetten
    - Maak twee virtuele netwerkadapters aan, één van het type NAT (= standaardkeuze), en één van het type "Host only"

### Procedure

Beschrijf hier de exacte procedure hoe je dit uitgevoerd hebt. Zorg er voor dat je aan de hand van je beschrijving heel vlot de installatie later kan herhalen als dat nodig is.

1. Installeer Virtualbox
2. Maak in virtualbox een nieuwe virtuele schijf aan.
3. Benoem hem met jouw naam als je op klaspc werkt.
4. je wijst ongeveer 1/4 van de mogelijke ram toe aan je virtuele schijf
5. je maakt uiteindelijk een nieuwe schijf aan op de plaats waar je wilt, je alloceert hem dynamisch en stelt ongeveer 40 GB in als maximum voor die schijf.
6. je stelt je videogeheugen in, 3d-acceleratie en netwerkadapters in.
7. je start hem op!

## Linux installeren in een VirtualBox VM

1. Download de laatste [Fedora Live Desktop CD](https://getfedora.org/en_GB/workstation/download/). Start je VM op met deze LiveCD als opstartschijf (het is niet nodig een fysieke cd te branden, je kan een VM rechtstreeks van de ISO booten). Let op dat je met heel de klasgroep niet het draadloos netwerk satureert...
2. Wijzig na opstarten voor het gemak de toetsenbordinstelling naar Belgische Azerty
3. Installeer Fedora naar de harde schijf van je VM (opm. dit is een volkomen veilige operatie en heeft geen enkele invloed op je hostsysteem).
    - Kies de juiste tijdzone, toetsenbordindeling en taal (bij voorkeur Engels)
    - Kies de voorgestelde partitionering van de harde schijf
    - Stel het wachtwoord van de “root” gebruiker in. LET OP: ben je zeker dat je in Azerty-indeling aan het typen bent? TIP: noteer dit wachtwoord onder “Description” in de instellingen van je VirtualBox VM. Als je het vergeet kan je het makkelijk terugvinden.
4. Herstart je VM in het geïnstalleerde systeem. Maak een nieuwe gebruiker aan voor jezelf en voeg die toe aan de “Administrators” groep. In Linux is de conventie om *enkel kleine letters* te gebruiken voor gebruikersnamen.
5. Zoek je weg in het nieuwe systeem.
    - Kan je een webbrowser opstarten? Kan je op het Internet?
    - Kan je een teksteditor (Gnome Editor of Gedit) opstarten?
    - Kan je een tekstverwerker (LibreOffice Writer) opstarten?
    - Kan je de inhoud van je “thuismap” tonen in het Linux-equivalent van Windows Verkenner?
    - Kan je een “terminal-venster” openen?
    - Kan je de screensaver uitschakelen?

**Opmerking** Als je een nieuw Linux-systeem installeert, krijg je al gauw de melding dat er heel wat updates beschikbaar zijn. Het is af te raden om dit in het klaslokaal te doen, opnieuw om de netwerkverbinding naar buiten niet te satureren. Doe dit dus liefst thuis.

### Procedure

Beschrijf hier de exacte procedure hoe je dit uitgevoerd hebt. Zorg er voor dat je aan de hand van je beschrijving deze taken later heel vlot kan herhalen als dat nodig is.

1. Start op met een live-cd (iso)
2. normaal wordt alles ingesteld zoals jij het wilt, je maakt juist tijdens de installatie een gebruiker en een root-wachtwoord aan.
3. Heropstarten zonder live-cd
4. laatste instellingen voltooien en updaten.

## Nieuwe software installeren

Installeer onderstaande applicaties of “packages”. Zorg er voor dat je dit zowel via de grafische gebruikersinterface kan als vanop de command-line.

- git
- nano
- ShellCheck
- vim-enhanced
- vim-X11

Installeer optioneel de “VirtualBox Guest Additions” (zie procedure in de [studiewijzer](../studiewijzer/installatie.md)). Creëer een lokale kopie van je Github repository.

### Procedure

Beschrijf hier de exacte procedure hoe je dit uitgevoerd hebt. Zorg er voor dat je aan de hand van je beschrijving deze taken later heel vlot kan herhalen als dat nodig is.

1. Virtualbox Guest Additions kan je installeren door via "invoer" en dan de cd in te voeren en de setup te volgen, zorg er wel voor dat je kernel up-to-date is!
2. gebruik yum search of dnf search string / sudo dnf install... om de paketten te installeren! Grafisch heb ik geen idee hoe het moet...

## Gebruikers en groepen aanmaken

Het doel van deze opgave is om de opdrachten en de begrippen met betrekking tot  gebruikers en groepen te bestuderen, binnen de context van Linux als een multi-user-systeem.

Tussen de vragen is ruimte voorzien om je antwoorden in te vullen. Het gaat telkens om zgn. codeblokken in Markdown, die starten en eindigen met drie backquotes. Binnen elk codeblok geef je telkens het commando dat je hebt ingetikt en de uitvoer die je krijgt.

1. Je hebt al een gebruiker aangemaakt voor jezelf. Log in als deze gebruiker. Geef hieronder telkens het commando en de uitvoer
    - Wat is het commando om de huidige directory op te vragen? Welke uitvoer toont het commando?

        ```
        $ pwd
        /home/lbracke
        ```

    - Wat is het UID van deze gebruiker?

        ```
        $ id -u   of $ id
        UID=1000(lbracke)
        ```

    - Wat is het GID van deze gebruiker?

        ```
        $ id -g   of $ id
        GID=1000(lbracke)
        ```

2. Log in als de `root`-gebruiker met het commando `su -` (let op de spatie!)
    - Wat is de home-directory van `root`?

        ```
        # pwd
        /root
        ```

    - Wat is het UID van deze gebruiker?

        ```
        # id -u
        0
        ```

    - Wat is het GID van deze gebruiker?

        ```
        # id -g
        0
        ```

3. Maak een nieuwe gebruiker aan met de naam `alice`, zonder specifieke opties
    - Geef het gebruikte commando:

        ```
        # useradd alice
        geen uitvoer
        ```

    - Voorzie een geschikt wachtwoord voor deze gebruiker (en vergeet het niet! Noteer het eventueel hier in je verslag of in de beschrijving van je VM)

        ```
        # passwd alice
        nieuw wachtwoord: alice123
        nieuw wachtwoord herhalen: alice123
        passwd: alle authenticatie tokens zijn succesvol bijgewerkt.
        ```

4. Configuratiebestanden voor gebruikersbeheer:
    - In welk bestand kan je de UID, gebruikersnaam, homedirectory, enz. van alle gebruikers terugvinden?

        ```
        # less /etc/passwd
        ```

    - In welk configuratiebestand kan je al de bestaande gebruikersgroepen nakijken, en ook de gebruikers die lid zijn van elke groep?

        ```
        #less /etc/group
        ```

    - In welk configuratiebestand vind je de *wachtwoorden* van alle gebruikers?

        ```
        #less /etc/shadow (passwoorden zijn hier getoond in allerlei karakters)
        ```

5. Gebruikersgroepen aanmaken
    - Maak een groep aan met de naam `sporten`

        ```
        # groupadd sporten
        geen uitvoer
        ```

    - In welk configuratiebestand vind je het GID van deze groep terug?

        ```
        # less /etc/group
        sporten:x:1002:
        ```

    - Wat zal het GID zijn van de groepen `zwemmen` en `judo` als je deze nu onmiddellijk zou aanmaken? Maak ze aan en controleer!

        ```
        # groupadd zwemmen judo
        GID zal 1003 en 1004 zijn!
        ```

    - Voeg de gebruiker `alice` toe aan de groepen `sporten` en `zwemmen`

        ```
        # usermod -aG sporten,zwemmen alice
        geen uitvoer, als je dan intikt "id alice", kan je zien dat ze zowel tot groep alice, sporten als zwemmen behoort.
        ```

    - Log in als `alice` door in een terminal het commando `su - alice` (let op de spaties!) uit te voeren

        ```
        # su - alice
        [alice@localhost ~] wordt geopend
        ```

    - Zorg er nu voor dat de groep `sporten` de primaire groep wordt van `alice`.

        ```
        # usermod -g sporten alice (terug root zijn!!!)
        geen uitvoer, als je intikt "id alice" zie je dat groep id nu 1002(sporten) is.
        ```

    - Zorg er voor dat `alice` uitgelogd is, ga terug naar `root`

        ```
        # exit of logout (als je rechtstreeks naar root wilt, gebruik dan vanuit alice haar account "su -")
        uitgelogd of exit staat er dan.
        ```

6. Maak nu de gebruikers in onderstaande tabel aan. Zorg er voor dat ze al meteen bij aanmaken tot de aangegeven groepen behoren. Kies zelf geschikte wachtwoorden voor deze gebruikers en vergeet ze niet (vul eventueel een kolom toe aan de tabel).

    | Gebruikersnaam | Primaire groep | Secundaire groep | Wachtwoorden
    | :---           | :---           | :---             |
    | `bob`          | `sporten`      | `judo`           |'bob123'
    | `carol`        | `sporten`      | `zwemmen`        |'carol123'
    | `daniel`       | `sporten`      | `judo`           |'daniel123'
    | `eva`          | `sporten`      | `zwemmen`        |'eva123'

    - Geef de gebruikte commando's om de gebruikers aan te maken en ook om te verifiëren of dit correct gebeurd is:

        ```
        #useradd -g sporten bob
        #usermod -aG judo bob
        #useradd -g sporten carol
        #usermod -aG judo carol
        #useradd -g zwemmen daniel
        #usermod -aG judo daniel
        #useradd -g sporten eva
        #usermod -aG zwemmen eva
        #passwd eva / bob / daniel / carol
        
        checken met id bob bijvoorbeeld... of kijken in etc/passwd of etc/shadow
        ...
        ```

    - Verwijder nu de *groep* `alice` en controleer.

        ```
        #groupdel alice
        kijken in bestand /etc/group
        ```

    - Gebruiker `daniel` gaat een tijdje niet meer sporten. Zorg er voor dat deze gebruiker tot nader order geen toegang meer kan hebben tot het systeem (zonder het wachtwoord of de gebruiker te verwijderen!).

        ```
        #usermod -L daniel (en -U voor unlock
        geen uitvoer, maar je kan checken in bestand
        ```

    - Hoe kan je controleren dat `daniel` inderdaad geen toegang meer heeft tot het systeem? In welk bestand kan dat en hoe zie je daar dan dat het account afgesloten is?

        ```
        # less /etc/shadow
        kijken of er x of uitroepteken bijstaat (er staan een uitroepteken voor zijn geencrypteerd paswoord)
        ```

    - Gebruiker `daniel` komt terug naar de sportclub. Geef hem opnieuw toegang tot het systeem.

        ```
        $ usermod -U daniel
        kijk in bestand of lock weg is
        ```

    - Gebruiker `eva` stopt helemaal met sporten. Verwijder deze gebruiker, maar doe dit zorgvuldig: zorg er in het bijzonder voor dat ook haar homedirectory verwijderd wordt.

        ```
        $ userdel -r eva
        kijk in /etc/passwd
        ```

7. Log aan als de gebruiker `carol`

    ```
    $ su - carol
    [carol@localhost]
    ```

    - Controleer of je in de “thuismap” bent van deze gebruiker. Maak onder het directory `Documenten/` een bestand `test` aan door middel van het commando `touch`.

        ```
        $ pwd (of cd intikken, en dan zit je direct in de thuismap van die gebruiker)tou
        /home/carol
        $ mkdir Documenten
        # cd Documenten
        #touch test
        
        
        ```

    - Probeer nu als gebruiker `carol` je te verplaatsen naar de “thuismap” van `alice`.

        ```
        $ cd /home/alice (je bent ingelogd als carol)
        
        ```

    - Kan je de inhoud van de mappen binnen de thuismap van `alice` bekijken?

        ```
        $ ls 
        ```

    - Probeer nu als `carol` onder het directory `Documenten/` in de “thuismap” van `alice` ook een bestand `test` te maken. Lukt dit? Kan je dit verklaren?

        ```
        # cd /home/alice/Documenten
        # touch test
        LUKT NIET!
        ```

