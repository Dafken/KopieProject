Java EE stack opzetten 
------

##OPMERKING

In de VM die gaat gebruiken als image mag je GEEN SSH instellen met public en private keys. Dit wordt onthouden wanneer je de image achteraf gebruikt, waardoor eerst een SSH reset nodig is via Azure CLI.

Opmerking : voor root geef je het volgende commando in: 

	sudo -s


MariaDB installeren
----

	yum update -y
	yum install mariadb-server

Verifieren dat mariaDB is opertioneel

	systemctl start mariadb.service
	systemctl enable mariadb.service

kijken of alles aan het lopen is

	systemctl is-active mariadb.service

password instellen voor mariaDB:

	mysql_secure_installation

Na installeren doe: 

	mysql -u root -p

geef passwoord en je zou iets in deze aard moeten zien:

	Welcome to the MariaDB monitor.  Commands end with ; or \g.
	Your MariaDB connection id is XXXX
	Server version: 5.5.X


	Copyright (c) 2000, 2014, Oracle, Monty Program Ab and others.


	Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.


	MariaDB [(none)]> 



Java (OpenJDK 1.8.0) installeren
-----

	yum install java-1.8.0

Java installatie controle + versie (Tomcat 8 requires java SE7 of hoger) 
	
	java -version

Tomcat 8 installeren
-----
Installeren van wget (dit is nodig voor tomcat te downloaden via internet)
	
	yum install wget

Navigeer naar /opt
	
	cd /opt

Downloaden van Tomcat 8 - core versie (http://tomcat.apache.org/download-80.cgi)

	wget http://www-eu.apache.org/dist/tomcat/tomcat-8/v8.0.32/bin/apache-tomcat-8.0.32.tar.gz

Uitpakken van .tar.gz file

	tar xzf apache-tomcat-8.0.32.tar.gz


Configureer de Tomcat root (CATALINA_HOME variable) in het CentOs systeem met de volgende 2 commando's

	echo "export CATALINA_HOME=\"/opt/apache-tomcat-8.0.32\"" >> ~/.bashrc
	
	source ~/.bashrc

Starten van Tomcat 8:

	cd /opt/apache-tomcat-8.0.32
	./bin/startup.sh

Enkele commando's om te testen of Tomcat online is:

	wget http://localhost:8080
    
	tail -f logs/catalina.out
	**output Server startup in xxx ms**


-----------

Auteurs: Mike Lobbezoo en Davy De Cock



