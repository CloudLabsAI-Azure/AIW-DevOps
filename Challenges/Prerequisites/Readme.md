# Prerequisites for the Code To Cloud Workshop

This workshop is targeted for students in a instructor-led training. To make it challenging for the students, the workshop contains challenges that can also be done individually. To make sure students do not get stuck, there are scripts available with instructions to "automatically" fix a challenge, so students can continue. The workshop also contains extensive Step-By-Step videos and written instructions. There are also videos that explain the concepts that are used in the exercises.

# Video
If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/STzJSPvtim4/0.jpg)](https://www.youtube.com/watch?v=STzJSPvtim4)

## Code base

The workshop builds upon an existing code base. Before you start the workshop, this code base needs to be forked or cloned. 

1. Sign in to the [Github](https://github.com/login) using the **GitHub Credential** provided under the **Environment details->Licenses** tab.

   ![](/Assets/Licensestab.png)

2. Navigate to [CodeToCloud-Source](https://github.com/xpiritbv/CodeToCloud-Source) repository to fork it into a account you logged in the previous step.

3. Click on **Fork** from the top right corner
   
   ![](/Assets/fork.png)
   
4. Then from your forked repository under the **Settings** tab rename the forked repository to **CodeToCloud-Source-UniqueID**, Click on **Rename**.
   
   ![](/Assets/renamerepo.png)

>Get the UniqueID value from the **Environment details-> Azure Credentials** tab, Suppose the UniqueID is 296566 the name of the forked repository should be CodeToCloud-Source-296566

## GitHub Codespace

The workshop is built with and targeted at development with GitHub Codespace. A full featured IDE in the cloud. In order to start working you need to create a Codespace.

1. Navigate to your forked repository on GitHub

2. Under the **Code** dropdown click on **Open with Codespaces** then **+New Codespace**  to create a Code Space in your forked repo.

   ![](/Assets/CodeSpaces.png)

3. Preparation and Configuration of the Codespace takes around 3 minutes.

   ![](/Assets/Codespace-initiation.png)

4. Once your GitHub Codespace is created you should be able to see the files and a welcome message under the Terminal.

   ![](/Assets/Codespace-files.png)

   Visual Studio Code doesn't pass a couple of specific of keystrokes to the terminal, this may make it harder to quit docker once you've started a container interactively. You can add the [custom keybindings specified here](/.devcontainer/keybindings.json) to [your Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/keybindings#_advanced-customization). This remaps `ctrl-q` and `ctrl-p` when the terminal has focus.

## Set up workshop scripts

Furthermore, the workshop provides starter and solution scripts. These scripts are served as a Pull Request with instructions in your Git Repository. In order to make this work, and to make the scripts work we have set up a container and some helper scripts, that you can execute in the workshop.

To set this up, you need to perform these steps

* Setup your settings file and PowerShell Profile
* Create GitHub Personal Access Token
* Create Azure DevOps Personal Access Token

### Setup your settings file and PowerShell Profile

1. Open your GitHub Codespace 
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
5. This file is automatically loaded by the containers PowerShell Profile and pre-populates a number of global variables.

#### Create GitHub Personal Access Token

1. Ensure you are logged in to your GitHub Account.

2. Create a Personal Access Token as described below:

- In the upper-right corner of any page, click your profile photo, then click **Settings** and in the left sidebar click **Developer settings**.

  ![Permissions GH](/Assets/Settings_pat.png)

- Then in the left sidebar, click **Personal access tokens** to select the scopes or permissions you would like to grant this token.
  
  ![Permissions GH](/Assets/PAT.png)

- Click **Generate new token**.

  ![Permissions GH](/Assets/gentoken.png)

3. Click on Copy icon to copy the token to your clipboard and save it on your notepad. For security reasons, after you navigate off the page, you will not be able to see the token again. **DO NOT COMMIT THIS TO YOUR REPO!**

  ![Permissions GH](/Assets/copytoken.png)

#### Create Azure DevOps Personal Access Token

1. Login to `https://dev.azure.com/youraccount` using the lab credentials.
1. Create a Personal Access Token as [described here](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=preview-page)
1. Keep this Personal Access token somewhere safe for later use. **DO NOT COMMIT THIS TO YOUR REPO!**

## Variables

In some scripts we use variables like `$resourceGroupName` and `$webappName`. Based on the settings.json file, that is stored in your `.workshop` folder, we generated a PowerShell Profile for you. The values stored in `settings.json` are automatically loaded into your PowerShell console.

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

### Next Step

When you are done, move to the [first challenge](/Challenges/Module1-ImprovingDeveloperFlow/ImprovingDeveloperWorkflow.md)
