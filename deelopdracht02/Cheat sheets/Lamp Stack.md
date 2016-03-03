Lamp stack opzetten 
------

Opmrking : Azure create linux centos VM:  via PuTTyGen public key genereren, daarna private key en deze mee geven bij advanced options bij connection via SSH. 


Creating Apache
----- 

	sudo yum clean all
	sudo yum -y update
	sudo yum -y insall httpd 

Er is geen firewall precies dus hier geen rekening mee houden

Apache start 

	sudo systemctl start httpd
	sudo systemctl enable httpd
	sudo systemctl status httpd
	sudo systemctl stop httpd

Opmerking : voor systemctl moet je root zijn 

	sudo -s

miss later vn toepassing ( niet zeker):

	/usr/bin/mysql_secure_installation


MariaDB installeren
----

	yum update -y
	yum install mariadb-server

Verifieren dat mariaDb is opertioneel

	systemctl start mariadb.service
	systemctl enable mariadb.service

kijken of alles aan het lopen is

	systemctl is-active mariadb.service

Na installeren doe: 

	mysql -u root -p

geef passwoord als dat nodig is en je zou iets in deze aard moeten zien:

	Welcome to the MariaDB monitor.  Commands end with ; or \g.
	Your MariaDB connection id is XXXX
	Server version: 5.5.X


	Copyright (c) 2000, 2014, Oracle, Monty Program Ab and others.


	Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.


	MariaDB [(none)]> 

voor password:

	mysql_secure_installation

PHP installeren
-----

	yum install php php-mysql php-gd php-pear -y


Image maken met Azure
------

	sudo waagent -deprovision -force

dit maakt de image zo general mogelijk 




