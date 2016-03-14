## Testplan Azureservers

- Is de CentOS server aangemaakt op Azure cloud? Ja

- Is de Windows 2012 server aangemaakt op Azure cloud? Ja

- Kan ik connecteren van op elke pc aan de CentOS en Windows 2012 server? Ja

----------

Uitvoerder(s) test: Robby en Siebert

Uitgevoerd op: 04/03/2016

## Testplan LAMPstack

Testplan werkte volledig, enkel probleem met connecteren aan nieuwe VM aangezien de originele VM (image) met SSH ingesteld was met keys. 

Ook belangrijk om op te letten bij spelling bij aanmaak resourcegroup(netwerk) en VM.

- Is Apache geinstalleerd en kan je de status controlleren? Ja

- Is MariaDB geinstalleerd en kan je de status controlleren? Ja

- Is php geinstalleerd en kan je de status controlleren? Ja 

- Heb je de VM voorbereid om image van te nemen? Ja 

- Heb je Azure CLI geïnstalleerd? Ja

- Heb je image genomen? Ja

- Heb je resourcegroup aangemaakt voor het nieuwe netwerk? Ja

- Heb je de nieuwe VM aangemaakt met nieuwe user en pw? Ja

- Kan je connecteren aan de nieuwe VM mbv het ip adres en een connector zoals bv. mobaXterm? Ja

- Kan je wordpress deployen op de LAMP stack? Ja

![](https://i.gyazo.com/5308542d55ea9a3c22b5e13255f1c1dd.png)

----------

Uitvoerder(s) test: Robby en Siebert

Uitgevoerd op: 11/03/2016

## Testplan LAMPstack script

-  Heb je CLI? Ja
-  Ingelogd op Azure? Ja
-  Werkt het script? Ja
-  Kan je connecteren aan de VM? Ja
-  Kan je wordpress deployen op de LAMP stack? Ja

![](https://i.gyazo.com/30313df81af90df6a817b70aa2b56363.png)
![](https://i.gyazo.com/3384a76b8c4e3ccf2469bedb0226f906.png)
![](https://i.gyazo.com/4bd8b61d38c02b6a71c879972eba5b24.png)

![](https://i.gyazo.com/5308542d55ea9a3c22b5e13255f1c1dd.png)

----------

Uitvoerder(s) test: Robby en Siebert

Uitgevoerd op: 04/03/2016

## Testplan WISA stack

- Kan je connecteren met de server? Ja
- Is IIS geinstalleerd? Ja
- Is MySQL of SQLServer geinstalleerd (of zit het al bij je OS)? Ja
- Is ASP.net geinstalleerd? Ja

![](https://i.gyazo.com/34cd3e21fc018e18c09ee741ddcb34b8.png)

- Kan je bij localhost het IIS startscherm zien? Ja

![](https://i.gyazo.com/c9639649fc6d0eb9ff25618660b3f972.png)
----------

Auteurs testplan: Robby Den Haese, Siebert Timmermans

## Testplan WISA stack script
- Heb je Azure CLI voor PowerShell? Ja
- Ben je ingelogd op Azure via je PowerShell? Ja

![](https://i.gyazo.com/9b633f5a2f59a7c76d9c12e0972eb66f.png)

- Is de PowerShell directory aangemaakt en is het script hierin geplaatst? Ja

![](https://i.gyazo.com/b6979eee45a150898ae3296f59b941e6.png)

- Is het certificaat gedownload en is dit hierin geplaatst? Ja

![](https://i.gyazo.com/509ba332e41873910d6644eefaa6e7c7.png)

- Zijn deze modules geimplementeerd? Ja

![](https://i.gyazo.com/830669cc1d1f98271ec4d0bdbe647ef0.png)

- Krijg je geen errors bij runnen van script? Neen

![](https://i.gyazo.com/fe110fdca12322ee0bce17161b106046.png)

- Kan je connecteren met de server? Ja
- Is IIS geinstalleerd? Ja
- Is ASP.net geinstalleerd? Ja

![](https://i.gyazo.com/34cd3e21fc018e18c09ee741ddcb34b8.png)

- Kan je bij localhost het IIS startscherm zien?

![](https://i.gyazo.com/c9639649fc6d0eb9ff25618660b3f972.png)

----------

Uitvoerder(s) test: Robby en Siebert

Uitgevoerd op: 10/03/2016

### Testplan JavaEEStack


- Is Tomcat8 geïnstalleerd en kan je de status controleren? Ja

- Is MariaDB geïnstalleerd en kan je de status controleren? Ja

- Is Java OpenJDK geïnstalleerd en kan je de status controleren? Ja

- Heb je de VM voorbereid om image van te nemen? Ja
 
- Heb je Azure CLI geïnstalleerd? Ja

- Heb je image genomen? Ja

- Heb je resourcegroup aangemaakt voor het nieuwe netwerk? Ja

- Heb je de nieuwe VM aangemaakt met nieuwe user en pw? Ja

- Kan je connecteren met de nieuwe VM door gebruik te maken van het ip-adres en een SSH-client zoals bv. mobaXterm? Ja  

### Testplan JavaEEStack script

-  Heb je CLI? Ja
-  Ingelogd op Azure? Ja
-  Werkt het script? Ja
-  Kan je connecteren aan de VM? Ja



#TO DO - Java EE, LAMP en WISA private server, authors en uitvoering bijzetten bij Java EE

----------

Uitvoerder(s) test: Davy De Cock en Mike Lobbezoo

Uitgevoerd op: 06/03/2016

