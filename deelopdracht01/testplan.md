# Testplan taak 1: Deelopdracht 1, labo's

(Een testplan is een *exacte* procedure van de handelingen die je moet uitvoeren om aan te tonen dat de opdracht volledig volbracht is en dat aan alle specificaties voldaan is. Een teamlid moet aan de hand van deze procedure in staat zijn om de tests uit te voeren en erover te rapporteren (= zie testrapport). Geef bij elke stap het verwachte resultaat en hoe je kan verifiëren of dat resultaat ook behaald is. Kies zelf de structuur: genummerde lijst, tabel, secties, ... Verwijder deze uitleg als het plan af is.)

## Testplan labo 1, Console verbinden met Switch ##
1. Verbind de Switch met de PC via een console kabel
2. Gebruik Tera Term om via de console te kunnen werken, te downloaden op [Tera Term](http://logmett.com/index.php?/download/free-downloads.html "Tera download")
3. Kies de Serial radio button die verbonden is met de COM-poort
4. Hou er rekening mee dat Tera Term eerst verbonden moet zijn voordat de switch opgestart wordt
5. Via show version kan je de IOS versie van de switch bekijken bij "System image file"
6. Configuring the clock
	1. Switch> show clock
	2. Switch> enable (privileged EXEC)
	3. Switch# clock set 15:08:00 Feb 28 2016
	4. Switch# show clock

## Testplan labo 2, 2 Switches met 2 PCs verbinden, via ethernet ##
1. Verbind de Ethernetkabel aan de Switch 1 op F0/1 met F0/1 op Switch 2
2. Verbind de PC-A via de NIC poort en de F0/6 poort op Switch 1
3. Verbind de PC-B via de NIC poort en de F0/18 poort op Switch 2
4. Check of lichtje groen zijn
5. Configuring IP
	1. Navigeer naar de netwerkconnectie die je net gelegd hebt Netwerk en Internet
	2. Rechterklik om aan de properties te geraken
	3. Kies de properties van IPv4
	4. Vul het IP-adres in, 192.168.1.10 met subnet 255.255.255.0
6. Verify de connectivity
	1. open het cmd.exe
	2. bekijk het IP-adres met ipconfig /all
	3. ping 192.168.1.11
	4. Als dit niet werkt, troubleshoot of probeer opnieuw
7. Configure en verify Switch
	1. Gebruik Tera Term om te connecteren tussen Switch en PC A
	2. Switch> enable
	3. Switch# configure terminal - toegang tot configuration
	4. Switch(config)# hostname S1 - verander hostname van Switch
	5. S1(config)# no ip domain-lookup - tegenhouden van ongewenste DNS lookups
	6. Passwords toevoegen
		1. S1(config)# enable secret class 
		2. S1(config)# line con 0 
		3. S1(config-line)# password cisco 
		4. S1(config-line)# login 
		5. S1(config-line)# exit 
		6. S1(config)#
	7. MOTD banner toevoegen
		1. S1(config)# banner motd # 
		2. Enter TEXT message. End with the character '#'. Unauthorized access is strictly prohibited and prosecuted to the full extent of the law. #
		3.  S1(config)# exit 
		4.  S1#
	8. De configuratie bewaren
		1. S1# copy running-config
		2.  startup-config Destination filename [startup-config]? [Enter]
		3.   Building configuration... [OK] 
		4.   S1#
	9. Tonen van de current configuratie
		1. S1# show running-config
	10. Display IOS
		1. S1# show version
	11. Display status van geconnecteeerde interfaces van de switch
		1. S1# show ip interface brief
8. Doe hetzelfde voor S2, met het andere IP adres

Appendix initializeren en reloaden van switch

1. Kijken of VLANs zijn toegevoegd op de switch
	1. Switch# show flash 
2. Deleten van VLAN file
	1. Switch# delete vlan.dat 
	2. Delete filename [vlan.dat]?
	3. Enter tweemaal
3. Cleanen van de startup config file
	1. Switch# erase startup-config
	2. Erasing the nvram filesystem will remove all configuration files! Continue? [confirm] 
	3. [OK] 
	4. Erase of nvram: complete
4. reloaden van de switch
	1. Switch# reload
	2. enter voor confirmatie
	3. Je kan prompt krijgen om running config te saven voor de reload, kies hier no
5. Bypassen van de initial config dialoog
	1. Kies hier nee


		
## Testplan labo 3, Netwerk met switch en router ##

Verbinden van de Devices

1. PC-A verbinden met F0/6 van S1
2. F0/5 van S1 verbinden met G0/1 van R1
3. G0/0 van R1 verbinden met PC-B

Opmerking

----------

Indien het een router met end device is heb je crossover cable nodig, zodat communicatie mogelijk is. Hierbij volstaat een lan cable niet, dit is enkel een passthrough.

Configureren van de devices en veriferen van de connectie

IP adressen toewijzen aan de PC's 

1. PC-A IP: 192.168.1.3,  Subnet Mask: 255.255.255.0, Default gateway: 192.168.1.1
2. PC-B  IP: 192.168.0.3,  Subnet Mask: 255.255.255.0, Default gateway: 192.168.0.1
3. ping van PC-B naar PC-A
4. Voor de instructies hiervoor zie vorige labo's

Configureren van de router

1. privileged mode
	1. Router> enable
2. config mode
	1. Router# conf t
3. device name geven
	1. Router(config)# hostname R1
4. disable DNS lookup voor ongewenste lookups
	1. R1(config)# no ip domain-lookup 
5. Passwoord voor enable -> class
	1. R1(config)# enable secret class
6. cisco als console passwoord
	1. R1(config)# line con 0 
	2. R1(config-line)# password cisco 
	3. R1(config-line)# login 
	4. R1(config-line)# exit 
7. cisco als vty password + enable login
	1. R1(config)# line vty 0 4 
	2. R1(config-line)# password cisco 
	3. R1(config-line)# login 
	4. R1(config-line)# exit 

8. Encrypteren van de clear text passwoorden
	1. R1(config)# service password-encryption

9. Banner aanmaken
	1. R1(config)# banner motd #
	2.  Enter TEXT message.  End with the character '#'.   
	3.  Unauthorized access prohibited! 
	3. # 
	4. R1(config)#

10. Configureer en activeer beide interfaces van de router
	1. R1(config)# int g0/0 
	2. R1(config-if)# description Connection to PC-B. 
	3. R1(config-if)# ip address 192.168.0.1 255.255.255.0 
	4. R1(config-if)# no shut
	5. R1(config-if)# int g0/1 
	6. R1(config-if)# description Connection to S1. 
	7. R1(config-if)# ip address 192.168.1.1 255.255.255.0 
	8. R1(config-if)# no shut 
	9. R1(config-if)# exit 
	10. R1(config)# exit

11. Saven van de running config naar de startp config
	1. R1# copy running-config startup-config
	2. Enter

12. Clock zetten, zie labo 1

13. Ping van PC B naar PC A, zie labo 2

Appendix labo 2: Initializeren en reloaden van de router

1. Connecteer aan de router
	1. Router> enable
2. Erase de startup config file van de nonvolatile RAM
	1. Router# erase startup-config
	2. enter
3. Reloaden van de router
	1. Router# reload
	2. enter
	3. bij prompt kies no om de running config niet te saven
4. Bypassen van de initial config dialog
	1. Would you like to enter the initial configuration dialog? [yes/no]: no 
5. Terminaten van autoinstall programma
	1. Would you like to terminate autoinstall? [yes]: yes 

Initializen van de Switch en reloaden

Zie labo 2 voor instructies




Auteurs testplan: Robby Den Haese, Siebert Timmermans


