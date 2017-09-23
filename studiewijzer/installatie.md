# Linux installeren

## Leerdoelen

- VirtualBox kunnen installeren en een nieuwe VM aanmaken
- Linux kunnen installeren binnen een VirtualBox VM
- Softwarepakketten kunnen installeren in een Linux-systeem
- Gebruikers en groepen kunnen beheren

## Voorbereiding

Raadpleeg de gerefereerde bronnen *voor* het begin van de les!

- VirtualBox kunnen installeren en een nieuwe VM aanmaken
    - Handleiding VirtualBox: <https://www.virtualbox.org/manual/ch01.html#intro-installing>
- Linux kunnen installeren binnen een VirtualBox VM
    - Screencast "Installatie Fedora 18 onder VirtualBox" <http://www.youtube.com/watch?v=1Rcf8-yk6_o> (dit is voor een oudere versie van Fedora, maar de installatie loopt nog steeds op ongeveer dezelfde manier)
- Softwarepakketten kunnen installeren in een Linux-systeem
    - Screencast: “Fedora 18 tips & tricks”, <http://www.youtube.com/watch?v=Ib5J67XQ8J4>
    - Fedora System Administrator's Guide, hst 6, "DNF" <https://docs.fedoraproject.org/en-US/Fedora/24/html/System_Administrators_Guide/ch-DNF.html>
- Gebruikers en groepen kunnen beheren
    - Screencast: “Gebruikers en groepen”, <http://www.youtube.com/watch?v=5MfeegzjbSY>
    - Linux Fundamentals, Deel VII, Local user management, p.186. <http://linux-training.be/linuxfun.pdf>

Belangrijke begrippen:

- Virtuele machine (VM): een gesimuleerd computersysteem waarop je een besturingssysteem/software kan installeren
- Hostsysteem: de fysieke machine waarop virtuele machines draaien.


## Agenda Les 1

- Uitleg organisatie cursus, cursusmateriaal, enz.
- Uitleg verloop van de lessen
- Toelichting opdracht 1, Linux installeren
- Installatie Fedora 24 ahv. screencast, demo.

## Je werk bijhouden met Git

Op deze manier kan je binnen je VM je werk efficiënt bijhouden:

- Zorg dat je op je VM de nodige software geïnstalleerd hebt (zoals in de labo-opgave beschreven).
- Open een terminal en voer uit: `ssh-keygen` (dit zal gebruikt worden om de toegang naar Github te vereenvoudigen). Beantwoord alle vragen met `<Enter>`.
- In de directory `~/.ssh` is er nu een bestand met de naam `id_rsa.pub` aangemaakt. Kopieer de inhoud van dat bestand.
- Ga naar je Github-repository en klik helemaar rechtsboven op het icoontje met je "avatar". Kies in het menu "Settings" en vervolgens in het menu links "SSH and GPG keys". Klik op "New SSH Key". Kies als titel bv. "VM voor Besturingssystemen/Linux" en plak in het tekstvak "Key" de inhoud van `id_rsa.pub`.
- Open een terminal en voer uit: `git clone git@github.com:HoGentTIN/ilnx-GITHUBGEBRUIKER.git` (met je eigen Github gebruikersnaam; je kan de juiste URL kopiëren op Github, via de groene knop "Clone or Download").
- Er wordt nu een nieuwe directory aangemaakt met de naam `ilnx-GITHUBGEBRUIKER`. Ga naar deze directory en open het bestand `README.md` (hetzij via de command-line, hetzij via de GUI). Vul onder de hoofding "Gegevens student" alle gevraagde informatie in.
- Registreer deze wijzigingen in Git:

    ```
    $ git add .
    $ git commit -m "Gegevens student ingevuld"
    $ git push
    ```

## Installatie VirtualBox Guest Additions

VirtualBox Guest Additions is een verzameling drivers die je op je VM kan installeren om die beter te integreren met je host-systeem: grootte van de desktop die zich aanpast aan de grootte van het venster, tekst knippen en plakken tussen host en VM, gedeelde mappen, enz. Op het Internet zijn verschillende [HOWTO’s](http://www.if-not-true-then-false.com/2010/install-virtualbox-guest-additions-on-fedora-centos-red-hat-rhel/) te vinden, en je kan ook de [VirtualBox documentatie](https://www.virtualbox.org/manual/ch04.html) naslaan. Hier een korte opsomming van de te volgen stappen.

1. Zorg dat je kernel de laatste versie is:

    ```console
    $ sudo dnf update kernel
    ```

2. Herstart de VM als er een nieuwe versie geïnstalleerd is.
3. Installeer de nodige packages:

    ```console
    $ sudo dnf install dkms kernel-devel kernel-headers
    ```

4. In het menu van het VM-venster, kies Devices > Install Guest Additions of gebruik snelkoppeling Host+D. Dit simuleert het insteken van een installatie-cd in de virtuele machine.
5. In een grafische omgeving krijg je een dialoogvenster te zien dat vraagt om de installatie op te starten. Bevestig dit. Als dit niet gebeurt, ga dan naar de directory van de installatie-cd (ga kijken in `/run/media/USER/CDNAAM/`, met `USER` je eigen gebruikersnaam en `CDNAAM` het label van de Guest Additions installatie-cd). Voer in deze directory het volgende commando uit:

    ```console
    $ sudo sh ./VBoxLinuxAdditions.run
    ```

6. Herstart opnieuw de VM, daarmee zou de installatie moeten compleet zijn. Je kan dit uittesten door bv. "Seamless mode" aan te zetten

## Installatie optionele configuratiebestanden

In de Github-repository <https://github.com/bertvv/server-dotfiles> worden voor een aantal in deze cursus heel vaak gebruikte tools (zoals Bash, Vim, Nano) configuratiebestanden aangeboden die het werken een stuk zouden moeten vergemakkelijken. In de README vind je installatie-instructies, maar voor het gemak herhalen we die hier:

Open eerst een terminalvenster, blijf in je eigen home-directory en voer volgende commando's uit:

```
$ git init
$ git remote add -t \* -f origin https://github.com/bertvv/server-dotfiles.git
$ git checkout --force master
$ install-vim-plugins
```

Als je zelf wijzigingen wil aanbrengen aan deze configuratie, is het best dat je een *fork* van deze repository voor jezelf aanmaakt. Wanneer je eigen repository op Github klaar is, voer je volgende commando's uit:

```
$ git remote remove origin
$ git remote add origin git@github.com:GITHUBGEBRUIKER/server-dotfiles.git
```

met uiteraard je eigen Github gebruikersnaam.
