# Getting Started for the Code To Cloud Workshop

This workshop is targeted at students in instructor-led training. To make it challenging for the students, the workshop contains challenges that can also be done individually. To make sure students do not get stuck, there are scripts available with instructions to "automatically" fix a challenge, so students can continue. The workshop also contains extensive Step-By-Step videos and written instructions. There are also videos that explain the concepts that are used in the exercises.

# Video
If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/STzJSPvtim4/0.jpg)](https://www.youtube.com/watch?v=STzJSPvtim4)

## Codebase

The workshop builds upon an existing codebase. Before you start the workshop, this codebase needs to be forked or cloned. 

1.  On the Virtual Machine provided on the left of the screen, click on Microsoft Edge and complete the initial getting started prompts. Then, sign in to the Github ``https://github.com/login`` using the **Outlook/GitHub Credential** provided under the **Environment details** tab

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/env-creds.png)
   
2. If prompted with the **Device Verification** dialog box, open Microsoft edge Browser in **incognito mode** ( you can open incognito mode by clicking on the three dots "..." icon  at the top right of the browser within the virtual machine and then select New InPrivate window)

3. Now, sign in to Outlook by navigating to https://outlook.com using the **Outlook/GitHub Credential** provided under the **Environment details** tab 

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/code.png)

4. From the Outlook Inbox, you can find the verfication code and then click on **Verify** in the **Device Verification** dialog box that is opened in the different browser window. After providing the code you will be successfully logged in to Github.

5. After Login, open a new tab in the browser window where you are already logged in to GitHub and navigate to ``https://github.com/xpiritbv/CodeToCloud-Source``

6. Then, click on Fork at the top right, select your account with the name **github-cloudlabuser-UniqueID**

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/forked-repo.png)

UniqueID value is provided under the Environment details-> Azure Credentials tab.
       

## GitHub Codespace

The workshop is built with and targeted at development with GitHub Codespace, a full-featured IDE in the cloud. To start working, you need to create a Codespace.

1. Navigate to your forked repository on GitHub. The name of the forked repository will be in the following format - **github-cloudlabuser-UniqueID/CodeToCloud-Source**

2. Now, click on the **Code** dropdown, then click on **Open with Codespaces** and then on **+New Codespace**  to create a Code Space in your forked repo.

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/CodeSpaces.png)

3. Preparation and Configuration of the Codespace takes around 3 minutes.

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/codespace-build.png)

4. Once your GitHub Codespace is created, you should be able to see the files and a welcome message under the Terminal.

   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/Codespace-files.png)

   Visual Studio Code doesn't pass a couple of specific keystrokes to the terminal, this may make it harder to quit docker once you've started a container interactively. You can add the custom keybindings  [your Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/keybindings#_advanced-customization). This remaps `ctrl-q` and `ctrl-p` when the terminal has focus.

## Set up workshop scripts

Furthermore, the workshop provides starter and solution scripts. These scripts are served as a Pull Request with instructions in your Git Repository. To make this work, and to make the scripts work we have set up a container and some helper scripts, that you can execute in the workshop.

To set this up, you need to perform these steps

* Setup your settings file and PowerShell Profile
* Create GitHub Personal Access Token
* Create Azure DevOps Personal Access Token

#### Create GitHub Personal Access Token

1. Ensure you are logged in to your GitHub account.

2. Create a Personal Access Token as described below:

- In the upper-right corner of any page, click your profile photo, then click **Settings** and in the left sidebar click **Developer settings**.

  ![Permissions GH](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/Settings_pat.png)

- Then in the left sidebar, click **Personal access tokens** and select Generate new token button on the right. Provide the GitHub password if prompted. 

3. Select the scopes or permissions you would like to grant this token

    - Note: Provide the following text in the note field, UniquedId-token. Rreplace UniqueID with the value given in Environment Details -> Azure Credentials tab.
    - Select worklow, write:packages, delete:packages, read:org
  
  ![Permissions GH](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/PAT.png)

- Click **Generate token**.

  ![Permissions GH](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/gentoken.png)

4. Click on the Copy icon to copy the token to your clipboard and save it on your notepad. For security reasons, after you navigate off the page, you will not be able to see the token again. **DO NOT COMMIT THIS TO YOUR REPO!**

  ![Permissions GH](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/copytoken.png)

#### Create Azure DevOps Personal Access Token

1. log in to `https://dev.azure.com/` using the Azure credentials provided in Environment details.

   ![Azure creds](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/azure-creds.png)
   
3. Create project named **CodeToCloudWorkshop-UniqueID** 

   ![create project](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/azuredevops-project.png)
   
>Get the UniqueID value from the **Environment details-> Azure Credentials** tab, Suppose the UniqueID is 296566 the name of the forked repository should be CodeToCloud-Source-296566

3. Go to **User settings** and then select Personal Access Tokens
   
   ![select pat](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/azuredevops-pat.png)
   
4. Click on **+ New Token**   
   
   ![new token](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/azuredevops-newtoken.png)
   
5. Create token named **UniqueID-Token** and provide the following permissions
   * Work Items: Read & Write
   * Build: Read & Execute
   * Project & Team: Read, Write & Manage  ( To view Project & Team, click on **Show all scopes** just above Create button )

   ![create token](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/azuredevops-createtoken.png)
   
6. Copy the value of the generated token and save it in the notepad where you have stored the GitHub Personal Access Token.

   ![copy token](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/azuredevops-copypat.png)
   
7. Keep this Personal Access token safe for later use. **DO NOT COMMIT THIS TO YOUR REPO!**

### Setup your settings file and PowerShell Profile

1. Now, Open your GitHub Codespace 
2. In the terminal type `pwsh`
3. Then run `.workshop/setup.ps1` which will ask for:
    1. The location of your repository
    2. Your GitHub Personal Access Token with the following scopes (see instructions below):
       * repo
       * read:packages
       * write:packages
       * read:org
       * workflow
    3. The name of your Azure DevOps organization
    4. Your Azure DevOps Personal Access Token with the following scopes:
       * Work Items: Read & Write
       * Build: Read & Execute
       * Project & Team: Read, Write & Manage
    5. The name of the Project in Azure DevOps. The project will be automatically created if it doesn't exist yet. If the students must use pre-created projects, make sure they are using the Basic Process for Azure Boards.
    6. Your unique suffix (short, only lower case letters). This will be used to create the name of the resource group and resources in Azure.
    7. Whether to create/recreate work items in Azure Boards to which the commits and pull-requests will be linked.

4. A local `settings.json` file has been created in the `.workshop` folder and is automatically ignored by git. **DO NOT COMMIT THIS TO YOUR REPO!**
5. This file is automatically loaded by the containers PowerShell Profile and pre-populates several global variables.


## Variables

The following instructions are for addtional informational purpose. There is nothing to be performed as part of the lab.

In some scripts, we use variables like `$resourceGroupName` and `$webappName`. Based on the settings.json file, that is stored in your `.workshop` folder, we generated a PowerShell Profile for you. The values stored in `settings.json` are automatically loaded into your PowerShell console.

Available variables (loaded into `$global:` and `$env` scopes):

```powershell
$studentsuffix         # short lowercase string of letters unique to you.
$resourcegroupName     # the name of the resource group that will be created for you
$cosmosDBName          # the name of the cosmosdb used by the webapp
$webappName            # web app service name
$planName              # web app service plan
$location1             # azure datacenter region
$location2             # azure datacenter region
$appInsights           # app insights instance name
$CR_PAT                # GitHub container registry accerr token
```

If you ever manually change the values in the `settings.json`, opening a fresh PowerShell console should load the new values automatically. Alternatively, run:

```powershell
Invoke-expression $profile
```

Now, you can move to the next page.
