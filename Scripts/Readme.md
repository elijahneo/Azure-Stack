ConfigASDK.ps1
==============
Description
-----------

The purpose of this script is to automate as much as possible post deployment tasks in Azure Stack Development Kit
This include :
* Set password expiration
* Disable windows update on all infrastructures VMs and ASDK host
* Tools installation (git, azstools, Azure Stack PS module)
* Registration with Azure
* Windows Server 2016 and Ubuntu 14.04.4-LTS images installation
* MySQL Resource Provider Installation
* Deployment of a MySQL 5.7 hosting Server on Windows Server 2016 Core
* Attach MySQL hosting server to MySQL Resource Provider
* SQL Resource Provider Installation
* Deployment of a SQL 2014 hosting server on Windows 2016
* Attach SQL Hosting server to SQL Resource Provider
* AppService Resource Provider sources download to c:\Temp
* Set new default Quotas for Compute, Network, Storage and keyvault
* Create a simple offer and plan to provide IaaS capabilities to tenants

Instructions
------------

* Login as your service adminstrator on your ASDK host.
* Edit the script and set the proper value to the following variables :
	
		$ISOPath = "PATH_TO_WIN2016_ISO"                             # path to your windows 2016 evaluation ISO
		$rppassword = "ADMINPASSWORD_FOR_RP_INSTALLATION"            # the password that you want to set for Resource Providers administrator account
		$azureRegSubscriptionId = "YOUR_SUBSCRIPTION_ID"             # your Azure subscription ID for registration
		$azureRegDirectoryTenantName = "YOUR_AAD_TENANT_NAME"        # your Azure Tenant Directory Name for registration
		$azureRegAccountId = "YOUR_AZURE_SERVICE_ADMIN"              # your Azure Global Administrator account ID for registration
		$azureDirectoryTenantName = "YOUR_AAD_TENANT_NAME"           # your Azure Tenant Directory Name for Azure Stack 
	
* Open an elevated powershell window and run the script using -AAD parameter if you are using Azure AD otherwise the script will assume this is an ADFS deployment. 
* If you want to also register your installation in order to enable telemetry and market place syndication add the -Register parameter.
* You will be prompted for credential, these are your azure stack service administrator credential.
* If you enabled registration, once azure stack powershell module is installed you will be prompted again for credentials, these will be your azure credentials for registration.
* mysqlrp administrator will be "mysqlrpadmin" and sqlrp administrator will be "sqlrpadmin". These logins are also applicable for hosting servers.
	
This script can take up to 3 hours to finish.
Once the script is finished you can proceed with app service installation then create a new plan including the paas services.
	
Usage Example:
-------------

	ConfigASDK.ps1 -AAD -Register