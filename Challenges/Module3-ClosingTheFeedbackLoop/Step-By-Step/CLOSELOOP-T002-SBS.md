# Step by Step CLOSELOOP-T002

If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/KeucYraZ5Qo/0.jpg)](https://www.youtube.com/watch?v=KeucYraZ5Qo)

In this task your are going to create a continuous deployment pipeline in GitHub Actions that triggers after the Continuous Integration build has been completed. 


1. In your GitHub Codespace, open a PowerShell Terminal and run the starter solution. A Pull Request with a new `deploy-infrastructure.ps1` will be created

      ```
      Workshop-Step Start "CLOSELOOP-T002"
      ```

2. In your GitHub repository, navigate to the Tab Pull Requests and open the Pull Request with CLOSELOOP-T002 in the title

3. In the Pull Request, check the conversation, Commits, Checks and Files Changed Tabs, and got through the instructions and changes.

4. On the Conversation Tab, press the Merge Pull Request Button, to merge the files in to the main branch. Link the Pull Request to your Azure Boards Work item for Module 3 by typing AB#Module1WorkItemID in the title or description of the Pull Request Commit Message. 

      ![Shows the button for merging a Pull Request in GitHub](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/mergePullRequest.png)

Now your repository contains the new file.

6. In your GitHub Codespace, update your files to the latest version by pulling them.

      ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-12-10-11.png)

## Create a new GitHub Action Workflow that builds and pushes with Docker Compose

When we start to use docker-compose as our mechanism to build and push containers, we need to give docker compose instructions where to find the Docker files that can be used to build the images. We already have a `docker-compose.yml` file in our repository, but this contains the name of the images, and not the instructions to build the containers. 

Before performing the next steps, you will need to enable the Improved Container Support so as to use GitHub Container Registry.
      - In the upper-right corner of any page, click your profile photo, then click Feature preview.
      - On the left, select "Improved container support", then click Enable.
      
 ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/enable-container-support.gif)


1. Navigate to the codespace and add a `build.docker-compose.yml` file to the root of your repository and add the following contents. And then commit and push the file.

   ```YAML
   version: "3.4"
   services:
     api:
       build: ./content-api

     web:
       build: ./content-web
   ```

2. To use docker compose in our build, we are going to add a new GitHub Action workflow. In your GitHub repository, open the **Actions** Tab and create a new GitHub Action.

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/NewGHAction.png)

3. Click on **Setup a workflow yourself** and rename the new YAML file file to **docker-publish.yml**.

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/simplewf.png)

4. Delete the content present in your yaml file.

5. Navigate to this link https://raw.githubusercontent.com/CloudlabsAI-Git/code-to-cloud/main/docker-publish.yml to get the docker-publish.yml file content . Copy the content of the file and paste it in your newly created **docker-publish.yml** file in GitHub.

4. In the docker-publish.yml review the following lines of code, this step logs in to your GitHub Container Registry with the CR_PAT secret that you created earlier.

   ```YAML
   - name: Log into GitHub Container Registry
     run: echo "${{ secrets.CR_PAT }}" | docker login https://ghcr.io -u ${{ github.actor }} --password-stdin
   ```

5. Review the below lines of code, this step uses the docker-compose.yml and build.docker-compose.yml to build the containers with the Docker files and push it to the GitHub Container Registry

   ```YAML
   - name: Build and Push image
     run: |  
       docker-compose -f docker-compose.yml -f build.docker-compose.yml build
       docker-compose -f docker-compose.yml -f build.docker-compose.yml push
   ```
   
6. In the docker-compose.yml scroll down to the end and replace `your abbreviation` with **<inject key="UniqueID" />**.

7. Now that the containers have been built and pushed, the Azure Web Application needs to be updated. Before you can interact with Azure, you need to have access to the Azure API with the Azure CLI. Using the Azure Login Task, we can login securely in Azure using a GitHub secret.

8. Go to Environment details click on **Service principle Credentials** copy **Application id(clientId)** , **clientSecret** , **subscriptionId** and **tenantId** 

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/sp-creds-auth.png)

   Replace the values that you copied in below Json
   ```JSON
   {
    "clientId": "...",
    "clientSecret": "...",
    "subscriptionId": "...",
    "tenantId": "...",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

Copy the complete JSON output to your clipboard.

9. In your repository settings, navigate to **Secrets** and create a new secret called **AZURE_CREDENTIALS**. Paste the copied value from your clipboard to the value of the secret and save it.

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/secretAZCRED.png)
        

10. Commit the workflow file. The GitHub Action will trigger.

