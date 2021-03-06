# Deploy and Configure Function Application 

- Open the Azure Function project located at "\solution\FunctionApp\" in Visual Studio
- Deploy the solution to the App Service Environment created by the ARM deployment script. 
- Once deployed you will need to set the Function App settings via the Azure Portal. Use the **App Settings Template** provided below to create the appropriate settings. Note, you may not have some of the required information yet as some of it is created later in the deployment and configuration process. If you don't know what to fill out just leave a placeholder value there for now.  
- For local development and testing create a "Local.Settings" file in the solution using the **App Settings Template** template. Note, you may not have some of the required information yet as some of it is created later in the deployment and configuration process. If you don't know what to fill out just leave a placeholder value there for now.


**App Settings Template**
```jsonc
{
    "AzureWebJobsStorage": "UseDevelopmentStorage=true", //Only needed for local development environment

    "FUNCTIONS_WORKER_RUNTIME": "dotnet",

    "AZURE_TENANT_ID": "72f988bf-86f1-41af-91ab-2d7cd011db47",
   
    "TenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    
    "AZURE_CLIENT_ID": "###", //Service Prinicpal Client Id. Only needed for local development environment (note repeated below due to use of legacy auth provider AND new auth provider)
    
    "ApplicationId": "####", //Service Prinicpal Client Id. Only needed for local development environment 
    
    "AZURE_CLIENT_SECRET": "####", //Service Prinicpal Auth Key. Only needed for local development environment (note repeated below due to use of legacy auth provider AND new auth provider)

    "AuthenticationKey": "####", //Service Prinicpal Auth Key. Only needed for local development environment

    "UseMSI": true, //Set to true in Azure function deployments and false for local developement deployments

    "FrameworkWideMaxConcurrency": 400, //Max number of concurrent tasks supported

    "AdsGoFastTaskMetaDataDatabaseServer": "#######.database.windows.net", //Address of the framework configuration database

    "AdsGoFastTaskMetaDataDatabaseName": "AdsGoFast",//Database name of the framework configuration database

    "AdsGoFastTaskMetaDataDatabaseUseTrustedConnection": false, //Only needed for local development environment

    "TaskMetaDataStorageAccount": "###", //Only needed for local development environment when we don't want to use a configuration database

    "TaskMetaDataStorageContainer": "###",//Only needed for local development environment when we don't want to use a configuration database

    "TaskMetaDataStorageFolder": "###",//Only needed for local development environment when we don't want to use a configuration database

    "SQLTemplateLocation": ".\\SqlTemplates\\", //Location of SQL Template files ... for local development you should not need to change this. For cloud delployment you need to change to D:\home\site\wwwroot\SqlTemplates\

    "KQLTemplateLocation": ".\\KqlTemplates\\", //Location of KQL Template files ... for local development you should not need to change this. For cloud delployment you need to change to D:\home\site\wwwroot\KqlTemplates\

    "HTMLTemplateLocation": ".\\HTMLEmailTemplates\\", /* !!!!!!! New !!!!!!! */ //Location of Email Template files ... for local development you should not need to change this. For cloud delployment you need to change to D:\home\site\wwwroot\HTMLEmailTemplates\

    "EnablePrepareFrameworkTasks": true, //Set to false to "turn-off" the prepare tasks function for local development environments. 

    "EnableRunFrameworkTasks": true, //Set to false to "turn-off" the run tasks function for local development environments. 

    "EnableGetADFStats": true, //Set to false to "turn-off" the get ADF stats functions for local development environments. 

    "AzureFunctionURL": "http://localhost:7071", //Set to your Azure function App base address for cloud deployments.

    "GetSASUriSendEmailHttpTriggerAzureFunctionKey": "#####", //Set to the value of the Azure Function key. This allows the main functions in the Azure function app to call the GetSASUriSendEmailHttpTrigger function via an HTTP Post.

    "RunFrameworkTasksHttpTriggerAzureFunctionKey": "#####", //Set to the value of the Azure Function key. This allows the main functions in the Azure function app to call the RunFrameworkTasksHttpTriggerr function via an HTTP request.

    "SENDGRID_APIKEY": "##########",//Set to your Sendgrid Key

    "AZStorageCacheFileListHttpTriggerAzureFunctionKey": "NA",/* !!!!!!! New !!!!!!! */   //Set to the value of the Azure Function key. This allows the main functions in the Azure function app to call the AZStorageCacheFileListHttpTrigger function via an HTTP request.

    "DefaultSentFromEmailAddress": "noreply@######.com",/* !!!!!!! New !!!!!!! */ //Set to default sent from address (system wide)

    "DefaultSentFromEmailName": "Ads Go Fast (No Reply)",/* !!!!!!! New !!!!!!! */ //Set to default sent from address name (system wide)

    "GenerateTaskObjectTestFiles": false,/* !!!!!!! New !!!!!!! */ //Provides the ability to generate UnitTest files instead of calling ADF or AF for task processing

    "TaskObjectTestFileLocation": ".\\UnitTestResults\\"/* !!!!!!! New !!!!!!! */ //Location of UnitTest Files... for local development you should not need to change this. For cloud delployment you need to change to D:\home\site\wwwroot\UnitTestResults\

  }
  ```