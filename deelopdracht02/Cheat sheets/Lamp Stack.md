Lamp stack opzetten 
------

#OPMERKING#

In de VM die gaat gebruiken als image mag je GEEN SSH instellen met public en private keys. Dit wordt onthouden wanneer je de image achteraf gebruikt, waardoor eerst een SSH reset nodig is via Azure CLI.


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

Azure CLI
------

*Vanaf hier is Azure CLI nodig, dit is te downloaden op [AzureCLIGitHub](https://github.com/Azure/azure-content/blob/master/articles/xplat-cli-install.md "Download Azure CLI")*

*Herstart je computer en open de command prompt. Login op je Azure. Instructies [hier](https://github.com/Azure/azure-content/blob/master/articles/xplat-cli-connect.md "connect Azure in CLI")*

Zorg ervoor dat je in resource manager mode zit

	azure config mode arm

Stop de VM die reeds gedeprovisioned is

	azure vm stop –g <your-resource-group-name> -n <your-virtual-machine-name>

Generalizeer de VM

	azure vm generalize –g <your-resource-group-name> -n <your-virtual-machine-name>

Neem nu de image en een local file template

	azure vm capture –g <your-resource-group-name> -n <your-virtual-machine-name> -p <your-vhd-name-prefix> -t <your-template-file-name.json>

Om de image te dupliceren hebben we nu eerst een netwerkconfiguratie nodig. We doen dit door een nieuwe resourceGroup aan te maken. 

ResourceGroup voor nieuw netwerk aanmaken
----

	azure group create <your-new-resource-group-name> -l "centralus"
    
    azure network vnet create <your-new-resource-group-name> <your-vnet-name> -l "centralus"
    
    azure network vnet subnet create <your-new-resource-group-name> <your-vnet-name> <your-subnet-name>
    
    azure network public-ip create <your-new-resource-group-name> <your-ip-name> -l "centralus"
    
    azure network nic create <your-new-resource-group-name> <your-nic-name> -k <your-subnetname> -m <your-vnet-name> -p <your-ip-name> -l "centralus"


Om de NIC te verkrijgen

	azure network nic show <your-new-resource-group-name> <your-nic-name>

Deployment van de nieuwe VM
----

Via de json en resource groep kan je nu een nieuwe VM aanmaken

	azure group deployment create –g <your-new-resource-group-name> -n <your-new-deployment-name> -f <your-template-file-name.json>

Hierna wordt gevraagd om een user met pw aan te maken, geef ook de NIC mee die we opgevraagd hadden

    info:Executing command group deployment create
    info:Supply values for the following parameters
    vmName: mynewvm
    adminUserName: myadminuser
    adminPassword: ********
    networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/mynewrg/providers/Microsoft.Network/networkInterfaces/mynewnic

Iets gelijkend aan dit zou moeten getoond worden

    + Initializing template configurations and parameters
    + Creating a deployment
    info:Created template deployment "dlnewdeploy"
    + Waiting for deployment to complete
    data:DeploymentName : mynewdeploy
    data:ResourceGroupName  : mynewrg
    data:ProvisioningState  : Succeeded
    data:Timestamp  : 2015-10-29T16:35:47.3419991Z
    data:Mode   : Incremental
    data:NameType  Value
    
    
    data:------------------  ------------  -------------------------------------
    
    data:vmName  Stringmynewvm
    
    
    data:vmSize  StringStandard_D1
    
    
    data:adminUserName   Stringmyadminuser
    
    
    data:adminPassword   SecureString  undefined
    
    
    data:networkInterfaceId  String/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/mynewrg/providers/Microsoft.Network/networkInterfaces/mynewnic
    info:group deployment create command OK

Verifieer of de creatie gelukt is door te connecteren via SSH naar het IP-adres

Om het IP-adres op te vragen

	azure network public-ip show <your-new-resource-group-name> <your-ip-name>

# TO DO #
- laatste stappen verwerken in script, met parameters die we kunnen aanpassen voor elk nieuw netwerk

