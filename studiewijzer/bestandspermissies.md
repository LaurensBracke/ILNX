# Bestandspermissies

## Leerdoelen en voorbereiding

- Bestandspermissies en eigendomsrechten
    - Cobbaut, hst VIII. 25. Standard file permissions, pp. 215-224
    - Cobbaut, hst VIII. 26. Advanced file permissions, pp. 225-229
    - Screencast "Bestandspermissies" <http://www.youtube.com/watch?v=nt6Ra5E3qLA >

Belangrijkste commando's:

| Commando | Taak                                                  |
| :---     | :---                                                  |
| `chown`  | Verander de eigenaar (en groep) van een bestand       |
| `chmod`  | Verander bestandspermissies                           |
| `chgrp`  | Verander de groep waartoe een bestand behoort         |
| `umask`  | Stel bestandspermissies voor nieuwe bestanden in      |
| `ls -l`  | Toon permissies van bestanden in de huidige directory |

Belangrijke begrippen:

- *Soorten toegangsrechten*: lezen (read, `r`), schrijven (write, `w`), uitvoeren (eXecute, `x`)
- *octale notatie:* Cijfercode gebruikt bij o.a. `chmod` die bestandspermissies voorstelt. Bestaat uit drie of vier cijfers, telkens van 0 t/m 7. Bv. 644, 1755, enz.
- *setuid:* Speciaal type permissie voor uitvoerbare bestanden. Diegene die het commando uitvoert krijgt de rechten van de *eigenaar* van het bestand.
- *setgid:* Speciaal type permissie, zoals *setuid*, maar wie het commando uitvoert krijgt de rechten van de *groep* waartoe het bestand behoort.
- *restricted deletion* of *sticky bit:* Speciaal type permissie. Enkel de eigenaar kan het bestand verwijderen.
