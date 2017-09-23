# Labo 4: Webserver/LAMP stack

In dit labo zullen we een webserver opzetten in de VM die je in het vorige labo gemaakt hebt.
Een van de populairste toepassingen van Linux als server is de zgn. LAMP-stack. Deze afkorting staat voor Linux + Apache + MySQL + PHP. De combinatie vormt een platform voor het ontwikkelen van webapplicaties waar vele bekende websites gebruik van maken (bv. Facebook).

Als je gebruik maakt van andere bronnen (bv. blog-artikel of HOWTO die je op het Internet vond), voeg die dan toe aan je logboek. Zo kan je die later makkelijk terug vinden.

## De Apache webserver installeren

Het is belangrijk dat je controleert voordat je aan dit labo begint, dat je twee netwerkinterfaces hebt op je virtuele machine. De ene moet van het type *NAT* zijn. Deze heeft verbinding met het internet en heeft typisch als IP-adres 10.0.2.15. De andere netwerkinterface moet van het type *Host-only* zijn. Via deze kan je communiceren met de host-machine en je webserver testen. Als je niets hebt veranderd de standaardinstellingen van VirtualBox, is het IP-adres hoogstwaarschijnlijk 192.168.56.101.

1. Installeer Apache op je virtuele machine en verifieer dat hij draait en vanop je host-machine bereikbaar is.
2. Installeer ondersteuning voor PHP en verifieer dat dit werkt, bijvoorbeeld met een eenvoudige PHP-pagina

### Procedure

Beschrijf hier de exacte procedure hoe je dit uitgevoerd hebt. Zorg er voor dat je aan de hand van je beschrijving deze taken later heel vlot kan herhalen als dat nodig is. Test ook telkens na elke stap dat die correct verlopen is.

1. doe eerst sudo dnf install httpd php, test het met sudo systemctl status httpd
2. ping vervolgens naar 127.0.0.1 om te zien of de webserver aanstaat, normaal niet.
3. Je kan je verbindingen testen door de commando's "service httpd status", "netstat -tl" of "ps -ef /httpd"
4. start vervolgens de server op via commando "sudo systemctl start httpd", normaal zullen de commando's van hierboven nu resultaat geven.
5. Probeer nu vanop je hostmachine naar 192.168.56.102 te surfen, maar dat gaat niet (firewall op linux -> http aanklikken!), normaal werkt het nu wel, ook 127.0.0.1 werkt!
6. tik vervolgens "sudo nano /var/www/html/index.php" om een php bestand aan te maken voor de server, om te zien of dit werkt!
7. tik in het bestand volgende zin "<?php phpinfo(); ?>" en sla het bestand op.
8. Wanneer je nu naar 127.0.0.1 op linux of 192.168.56.102 op de host surft, krijg je een pagina met alle info over php en weet je dus dat het werkt!

## MariaDB (MySQL)

MariaDB is de naam van een variant (fork) van de bekende database MySQL. Onder Fedora is MySQL zelf niet meer beschikbaar, maar MariaDB is volledig compatibel. Installeer MariaDB op je virtuele machine. Voer daarna het script `mysql_secure_installation` uit om het root-wachtwoord voor MariaDB in te stellen. Installeer ook PHPMyAdmin, dit is een webinterface voor het beheer van MySQL/MariaDB.


### Procedure

Beschrijf hier de exacte procedure hoe je dit uitgevoerd hebt. Zorg er voor dat je aan de hand van je beschrijving deze taken later heel vlot kan herhalen als dat nodig is. Test ook telkens na elke stap dat die correct verlopen is.

1. Geef in: "sudo dnf install mariadb-server phpmyadmin
2. sudo service mariadb status (staat nog inactief) dus moeten hem opstarten met "sudo systemctl start mariadb"
3. er staat een standaard mysql nu geinstalleerd, maar we gaan die voor de veiligheid aanpassen via het commando "sudo mysql_secure_installation. daar vul je je root paswoord in (of maakt er 1 aan) (Josperke1994) en vul op alle vragen verder ja in!
4. Nu moet wel de webserver opnieuw opgestart worden! door "sudo systemctl restart httpd".
5. nu kunnen we surfen op linux naar 127.0.0.1/phpmyadmin en daar de gegevens invullen.

## Webapplicatie

Kies een webapplicatie gebaseerd op PHP en installeer op je webserver. Enkele voorbeelden die je kan gebruiken: Drupal, Wordpress, Joomla, MediaWiki, enz.,


### Procedure

Beschrijf hier de exacte procedure hoe je dit uitgevoerd hebt. Zorg er voor dat je aan de hand van je beschrijving deze taken later heel vlot kan herhalen als dat nodig is. Test ook telkens na elke stap dat die correct verlopen is.

1. Download wordpress en pak het uit in var/www/html.
2. geef de map wordpress de naam 'blog'
3. vervolgens kunnen we dus surfen naar 127.0.0.1/blog, die ons zal aanmoedigen om eerst een databank aan te maken met een gebruiker.
4. in phpmyadmin maak je de database wordpress en een gebruiker 'wpuser' (inloggen met root en wachtwoord via 127.0.0.1/phpmyadmin)
5. die vul je dan in in de setup
6. vervolgens moet je nog via nano in de map blog een bestand aanmaken (wp-content of zoiets) en die opvullen met code die wordpress je geeft.
7. Alles opslaan en dan nog wat gegevens invullen voor wordpress om een account aan te maken.
8. Worpress werkt nu al op je linux, om het te doen werken op je host zal je het url van je website moeten aanpassen naar 192.168.56.102/blog!

## Netwerkconfiguratie en troubleshooting

1. Welk(e) IP-adres(sen) heeft je VM? Vul onderstaande tabel aan (voeg rijen toe zoveel als nodig). Welk commando gebruikte je?

    ```
    $ ifconfig of ipaddr
    UITVOER
    ```

    | Interface | IP-adres | Netwerkmasker |
    | :---      | :---     | :---          |
    | enp0s3 | 10.0.2.15 | 10.0.2.255 |
    | enp0s8 | 192.168.56.102 | 192.168.56.255 |
    | lo | 127.0.0.1 | 0.0.0.0 |

2. Via welke router/default gateway kan je VM naar het Internet? Welk commando gebruikte je?

    ```
    $ ip route of route [-n]
   default via 10.0.2.2 dev enp0s3 ....
    ```

3. Wat is het IP-adres van `www.hogent.be`?

    ```
    $ ping www.hogent.be (dig, nslookup of host kan ook)
    PING www.hogent.be (178.62.144.90) 56(84) bytes of data
    ```

4. Om het IP-adres van websites en dergelijke op te kunnen vragen, moet je VM kunnen contact maken met een DNS-server. Hoe weet Linux welke DNS-server(s) beschikbaar is/zijn? Geef het configuratiebestand en de huidige inhoud ervan.

    ```
    $ cat /etc/resolv.conf
    #Generated by NetworkManager
    search hogent.be
    nameserver 193.190.173.1
    nameserver 193.190.173.2
    ```

5. In welk(e) configuratiebestanden worden de instellingen van je netwerkinterfaces bijgehouden? Geef hieronder telkens ook de inhoud van deze bestanden:

    ```
    $ less /etc/sysconfig/network-scripts/ifcfg-#naam van de interface dan#
    HWADDR=08:00:27:91:36:71
    Type=Ethernet
    BOOTPROTO=dhcp
    defroute=yes
    peerdns=yes
    peerroutes=yes
    ipv4_failure_fatal=no
    ipv6init=yes
    ipv6_Autoconf=yes
    ipv6_defroute=yes
    ipv6_peerdns=yes
    ipv6_peerroutes=yes
    ipv6_failure_fatal=no
    ipv6_addr_gen_mode=stable-privacy
    name=enp0s3
    uuid=201f178a-1371-3621-96cd-476ccc8dbc7f
    onboot=yes
    autoconnect_priority=-999
    ```

6. Met welk commando test je of een host op het netwerk op dit moment online is? Probeer dit uit  vanop je VM met het IP-adres van je host-systeem en voeg de uitvoer hieronder in. Welk protocol uit de TCP/IP familie wordt door deze tool gebruikt?

    ```
    $ ping ip-adress van je host of ICMP
    38 packets transmitted, 38 received, 0 lost
    ```

7. Met het commando `ss -tln` kan je opvragen welke services er draaien op je systeem, ahv. de open netwerkpoorten. Leg uit wat de opties (`-tln`) betekenen. Probeer het commando uit op je VM wanneer Apache en MariaDB draaien en voeg de uitvoer hieronder in. Geef voor elke open poort beneden de 10.000 welke netwerkservice er mee geassocieerd is.

    ```
    $ ss -tln (t enkel tcp, l serverpoorten, n poortnummers) of netstat -tln
    listen 0 5 127.0.0.1:631
    listen 0 5 ::1:631
    listen 0 80 :::3306
    listen 0 128 :::80
    
    -tlnp (list TCP (-t) server (-l) port numbers (-n) with the process
behind them (-p). The -p option requires root, hence the sudo)
    ```

## Systeemlogbestanden

Om oorzaken te vinden van problemen op een Linux-systeem, maken systeembeheerders intensief gebruik van zgn. logbestanden. De meeste netwerkservices houden hun eigen logbestand(en), of maken gebruike van het algemene logsysteem dat op recente versies van Fedora `journald` heet.

1. In welke directory horen alle logbestanden volgens de Linux Filesystem Hierarcy Standard thuis?

  **Antwoord:**
  /var/log

2. Met welk commando kan je de algemene systeemlogs bekijken op een recente versie van Fedora?

    ```
    $ /var/log/journal of /var/log/dnf.log
    UITVOER
    ```

3. Met welk commando (incl. opties) kan je de logs blijven bekijken terwijl er nieuwe boodschappen toegevoegd worden? (Ter info: dit afsluiten kan met `<Ctrl-C>`

    ```
    $ tail -f /var/log/dnf.log
    UITVOER
    ```

4. Met welk commando kan je de logs voor een bepaalde netwerkservice bekijken?

    ```
    $ sudo cat.log | less | more
    UITVOER
    ```

5. Open in één console het algemene logbestand en hou het open voor nieuwe boodschappen (zoals hierboven gevraagd). Open nu een andere console waar je de host-only netwerkinterface opnieuw opstart. Wat gebeurt er in de logs? Bekijk in het bijzonder de lijnen met `dhclient`.

    ```
    $ COMMANDO
    Je krijgt boodschappen over het vernieuwen van het ip adress door de dhcp server.
    ```

6. Wat is de naam van het logbestand waar je kan opvolgen welke webpagina's er opgevraagd worden aan je webserver? **Antwoord:** `BESTAND`
    ```
    $ /var/log/httpd/access.log
    ```
7. Open dit bestand met `tail -f` en laad een webpagina via een webbrowser. Wat gebeurt er in het logbestand?

    ```
    $ uitvoeren van ophalen hoofdpagina (phpinfo)
    UITVOER ( /var/log/mysqld.log )
    ```

## Gebruikte bronnen

- 
