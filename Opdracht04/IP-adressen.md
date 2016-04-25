#IP-adressen#
------

##Lage kost##

Aantal hosts: 

- Productieomgeving: 19
- Vergaderzaal: 8
- Kantoor1: 46
- Kantoor2: 17
- Patchkast: 14 (routerpoorten verbonden met switchpoorten en switchpoorten verbonden met andere switchen)

Totaal: 90 devices + 90 poorten op switchen + 14 poorten patchkast = 194

Gebruikte klasse: Klasse C

Aantal subnets: 1 

Totale mogelijke hosts: 254 -> 2 tot de 8ste - 2 (netwerkID en BroadcastID)

nodige hostbits: 8 


Subnetmask: 11111111.11111111.11111111.00000000  = 255.255.255.0

Range: 192.168.1.0 -> 192.168.1.255 


| Nr. Subnet | Naam subnet | netwerk adres | subnetmask | CIDR | Adresrange | Broadcast | #hosts | 
|:--|:--|:--|:--|:--|:--|:--|:--|
|1|Lagekost| 192.168.1.0 | 255.255.255.0 | /24 | 192.168.1.1 - 192.168.1.254 | 192.168.1.255 | 254 | 

----------

Uitvoerder(s) : Robby Den Haese, Siebert Timmermans

Uitgevoerd op:



