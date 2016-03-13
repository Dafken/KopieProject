Vagrant Cheatsheet 
------
##Opmerking
Alvorens je begint met de vagrant installatie, installeer de virtualbox Guest Additions.

Installeren van Vagrant
------
Navigeer naar volgende link en selecteer je besturingssysteem.
[https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html "Vagrant downloaden")


Configureren van VirtualHardware
----
* Disable audio
* Disable USB
* Ensure Network Adapter 1 is set to NAT
* Add this port-forwarding rule: [Name: SSH, Protocol: TCP, Host IP: blank, Host Port: 2222, Guest IP: blank, Guest Port: 22]

Configureren van je virtueel systeem
----
Maak een gebruiker aan met naam "vagrant" en stel het password in: 
	
	useradd vagrant
	passwd vagrant 

pas de vagrant config file aan zodat vagrant toegang krijgt tot sudo, zonder dat het password prompt telkens opnieuw verschijnt

	visudo

voeg de vagrant gebruiker toe in de 

	vagrant ALL=(ALL) NOPASSWD:ALL

om te testen of het gelukt is kan je gebruik maken van volgend commando
	
	sudo pwd

als hij het root directory print zonder het password prompt dan weet je dat het geslaagd is.


Installeren van de vagrant key
-----------

Om de vagrant commando's te laten communiceren met de server via een ssh verbinding maken we gebruik van een vagrant key. Met volgende commando's kun je deze klaarzetten:

	mkdir -p /home/vagrant/.ssh
	chmod 0700 /home/vagrant/.ssh
	wget --no-check-certificate \ https:/?raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub \ -O /home/vagrant/.ssh/authorized_keys
	chmod 0600 /home/vagrant/.ssh/authorized_keys
	chown -R vagrant /home/vagrant/.ssh
