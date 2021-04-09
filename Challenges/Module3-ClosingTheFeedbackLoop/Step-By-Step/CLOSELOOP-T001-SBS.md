# Step by Step CLOSELOOP-T001

If you rather watch a video with step by step instructions, you can do that here
   [![Step by Step Video](https://img.youtube.com/vi/x7pidn6Uk6I/0.jpg)](https://www.youtube.com/watch?v=x7pidn6Uk6I)

In this task, you will set up Application Insights to monitor your application and underlying infrastructure. You need to create an Application Insights Azure resource by adding this to your Infrastructure as Code scripts and connect this to your cluster. Furthermore, you need to add Application Insights in your Web Application to gain insights into usage.

We can create all these resources manually, but since we want to do this "the DevOps way", we are going to create all resources as Infrastructure as Code. In this Step by Step we chose to create all resources with the Azure CLI.

## Create Application Insights Azure Resource

To enable Application Insights we need an Application Insights resource in our resource group

1. In your Codespace, open the file `deploy-infrastructure.ps1` in your infrastructure folder.

2. Add this code snippet to the file

      ```PowerShell
      $studentsuffix = "UniqueId"
      $resourcegroupName = "fabmedical-rg-" + $studentsuffix
      $location1 = "westeurope"
      $appInsights = "fabmedicalai-" + $studentsuffix

      az extension add --name application-insights
      $ai = az monitor app-insights component create --app $appInsights --location $location1 --kind web -g $resourcegroupName --application-type web --retention-time 120 | ConvertFrom-Json

      Write-Host "AI Instrumentation Key=$($ai.instrumentationKey)"
      ```
   > Note: Replace UniqueId with the value from Environment Details -> Azure Credentials tab.

3. Run the PowerShell script by executing the command below. Note down the AI Instrumentation Key onto a notepad. An Application Insights Resource will be created in your Azure Resource Group

    ```
    pushd
    ./deploy-infrastructure.ps1
    ```

## Add Application Insights SDK to your web application

1. First we need to install support for Application Insights in the web application. In your Codespace terminal navigate to the content-web directory and install the application insights SDK.

   ```bash
   npm install applicationinsights --save
   ```

2. To let the application know where to send the instrumentation data, open the `app.js` file in the content-web folder and add the following lines immediately after `express` is instantiated, substitute `AI Instrumentation Key` with the instrumentation key from the output of the `setup-appinsights.ps1` script.

   ```javascript
   const appInsights = require("applicationinsights");
   appInsights.setup("AI Instrumentation Key");
   appInsights.start();
   ```

   ![A screenshot of the code editor showing updates in context of the app.js file](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/hol-2019-10-02_12-33-29.png)

3. Save changes and push these changes to your repository so that GitHub Actions CI will build a new image.

   ```bash
   git add .
   git commit -m "Added Application Insights"
   git push
   ```

## Deploy the new version of the container to the cluster

1. When the GitHub Action CI is completed, (re)deploy the web container to the web application.

2. Visit the Resource and check if Application Insights is created and you will be able to see instrumentation data.


Now, you can move on to the next page.


