# Azure Data Service Go Fast - Deployment

In this section you will automatically provision all Azure resources required to run ADSGoFast Framework. We will use a pre-defined ARM template with the definition of all Azure services used for a small development environment.

## Azure services

The following Azure services will be deployed in your subscription:

Name                        | Type | Pricing Tier | Pricing Info |
----------------------------|------|--------------|--------------|
ADFIR-*suffix*	                | Virtual machine | Standard_B2ms | https://azure.microsoft.com/en-us/pricing/details/virtual-machines/windows/
ADFIR-*suffix*OsDisk            | Disk | E10 | https://azure.microsoft.com/en-us/pricing/details/managed-disks/
ADFIR-*suffix*NetInt            | Network interface ||
ads-kv-*suffix*                 | Azure KeyVault| Standard | https://azure.microsoft.com/en-au/pricing/details/key-vault/
adsgofast-srv-*suffix*          | SQL server || 
adsgofast                       | Azure SQL Database (Framework Metadata) | S0 DTU10 | https://azure.microsoft.com/en-us/pricing/details/sql-database/single/
AdventureWorksLT                | Azure SQL Database (Sample DB used for testing) | S0 DTU10 | https://azure.microsoft.com/en-us/pricing/details/sql-database/single/
adsgofast-vnet                  | Virtual network || https://azure.microsoft.com/en-us/pricing/details/virtual-network/
ADSGoFastADF-*suffix*           | Data factory (V2) | Data pipelines | https://azure.microsoft.com/en-us/pricing/details/data-factory/
appinsights-adsgofast           | Azure Monitor (Application Insights) || https://azure.microsoft.com/en-us/pricing/details/monitor/
azure-bastion-ads-go-fast       | Bastion | | https://azure.microsoft.com/en-au/pricing/details/azure-bastion/
azure-bastion-ads-go-fast-pip   | Public IP address || https://azure.microsoft.com/en-us/pricing/details/ip-addresses/
datalakestg*suffix*             | Azure Data Lake Storage Gen2 | LRS - StorageV2 | https://azure.microsoft.com/en-us/pricing/details/storage/data-lake/
FuncApp-*suffix*                | Azure Functions | Consumption plan | https://azure.microsoft.com/en-au/pricing/details/functions/
hpn-DM-ADSGoFast-Dev-RG         | App Service plan ||
logstg*suffix*                  | Azure Blob Storage | LRS - StorageV2 | https://azure.microsoft.com/en-us/pricing/details/storage/blobs/

<br>**IMPORTANT**: When you deploy the resources in your own subscription you are responsible for the charges related to the use of the services provisioned. If you don't want any extra charges associated with the resources you should delete the resource group and all resources in it.


--------------------------------------
## Deploy Azure Services
In this section you will use automated deployment and ARM templates to automate the deployment of all Azure Data Services.

1. You can deploy all Azure services required by clicking the **Deploy to Azure** button below. 

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2Fazure-data-services-go-fast-codebase%2Fmain%2FDeploy%2Fazuredeploy.json)

[![Visualize](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.svg?sanitize=true)](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2Fazure-data-services-go-fast-codebase%2Fmain%2FDeploy%2Fazuredeploy.json)

2. You will be directed to the Azure portal to deploy the ADS Go Fast ARM template from this repository. On the **Custom deployment** blade, enter the following details:


3. On the **Custom deployment** blade, enter the following details:
    <br>- **Subscription**: [your Azure subscription]
    <br>- **Resource group**: [you can select a existing Resource Group or create a new Resource Group]

    Please review the Terms and Conditions and check the box to indicate that you agree with them.

4. Click **Purchase**

![](../deploy/Media/Lab0-Image10.png)

5. Navigate to your resource group to monitor the progress of your ARM template deployment. A successful deployment should last less than 10 minutes.

    ![](../deploy/Media/Lab0-Image11.png)

5. Once your deployment is complete you are ready to start deploying the solution. Enjoy!

    ![](../deploy/Media/Lab0-Image09.png)


## Obtain the source code
Get a copy of the source code by either donwloading it as a zip file from git or cloning the repository. 

## Solution Deployment and Configuration
In this section you will use Azure DevOps to deploy the Database project, Data Factory components (Pipeline, Datasets, LinkedServices and Integration Runtime), Azure Function Application, and Administrative Web Application. Click through the links below and follow the instructions provided.


1. [Deploy Azure SQL Database](./overview-deployment-azuresql.md)

1. [Deploy Azure Data Factory Artefacts Application](./overview-deployment-adf.md)

1. [Deploy Azure Function Application](./overview-deployment-funcapp.md)

1. [Deploy Web Application](./overview-deployment-webapp.md)


## Access provisioning
The following sections will guide you through the processes required to set-up the required rights and privleges for service accounts and credentials used.

### Deployment Credentials

- Azure Data Factory MSI - Grant the managed service identity for Azure Data Factory rights as per the list below: 
    - Adventureworks Azure SQL Sample database [Read]
    - Key Vault [Read Secrets]
    - Datalake Storage Accounts [Blob Storage Contributor Role]
    - On-Prem SQL Server (Proxied by Azure VM in Demo Environment) [Read];
- Azure Functions MSI - Grant the managed service identity  rights as per the list below
    - ADS Go Fast metadata database [Read,Write and Execute]
    - Datalake Storage Accounts [Blob Storage Contributor Role]
    - Azure Data Factory [Contributor Role];
    - Application Insights for Function App & Web App [Read];
    - Log Analytics for Data Factory [Read]
- Web Application MSI - Grant the managed service identity  rights as per the list below
    - ADS Go Fast metadata database [Read,Write and Execute]
    - Datalake Storage Accounts [Blob Storage Contributor Role]
    - Application Insights for Function App & Web App [Read];
    - Log Analytics for Data Factory [Read]

### Local Development Credentials

- To facilitate local development Service Principals are used. Provision a service principal to act as a proxy for each of the MSI's in the list above. Once provisioned, grant these MSI's the equivalent rights so that they can appropriatley mimic the MSI's. Note, it is recommended that you only provision these service principals in NON-PRODUCTION environments. 

# TODO
## ADD to ARM Template
    - Create Staging database
    - Create Storage Container "datalakeraw and datalakelanding" on Data Lake Storage
    - Create Transient Storage Account and add Containers "transientin and transientout"
        - Create Storage Table "Filelist"
    - Create SendGrid Resource
    - Create Log Analytics





