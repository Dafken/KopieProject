#WISA stack setup
------

IIS 8.5 through PowerShell
----------

cmdlet PowerShell command to install all of IIS 8.5

	import-module servermanager

	add-windowsfeature web-server -includeallsubfeature

*note: you must be logged in as administrator to run the cmdlet*

If you want management tools for roles and features, add the IncludeManagementTools parameter to the code snippet

SQL Server
----------
Seeing it's not easily possible to install SQL Server or MySQL through PowerShell, we decided to use the Azure image of Windows Server 2012 R2 with SQL Server 2016 preinstalled

This will also make our scripting process more efficiënt

ASP.NET through CMD
----------
1. Make sure you are running as admin in cmd

1. At the command prompt, type the following: dism /online /enable-feature /featurename:netfx3

1. Wait for the command to complete. It could take several minutes.

1. Close the command prompt window.

#WISA stack script
------




----
Authors: Robby and Siebert
