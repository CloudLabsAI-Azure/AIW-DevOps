# Step by Step DEVWF-T001

If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/mrY42ZK6IoM/0.jpg)](https://www.youtube.com/watch?v=mrY42ZK6IoM)

In this task you are going to setup an integration between GitHub and Azure Boards, to be able to link work items and code commits.

There are 2 possible scenarios for this Step by Step

1. You have never used the Azure Boards integration before
2. You previously set up Azure Boards for another GitHub repository.

## You have never used the Azure Boards integration before

1. On the GitHub Marketplace, navigate to 

    ``` 
    https://github.com/marketplace/azure-boards
    ```

2. On the bottom of the page, select **Install it for free**.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/newABIntegration.png)

3. On the next page, Click **Complete order and begin installation**

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/CompleteOrder.png)

4. Select the [CodeToCloud-Source] repository and click **Install & Authorize**.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/ABSelectrepo.png)

    **Note**: If prompted for GitHub password enter password from the Outlook/GitHub Credential provided under the Environment details tab

5. Login to your Azure DevOps Organization, and select the Team Project that you created in the Prerequisite setup, then click on **Continue**.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-11-24-19.png)

6. When the integration succeeded, you will be taken to the Azure Board. 4 Work items are present and you see a "Success" message

## You previously set up Azure Boards for another GitHub repository.

When you already used the Azure Boards integration, you need to manually link the GitHub repository and the Azure DevOps Project.

1. Navigate back to your GitHub Repository, then go to your profile and choose [Settings]. In the Settings page, navigate to the [Applications] tab on the left and choose the [Configure] Button for the Azure Boards application.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-11-42-34.png)

2. In the [Repository Access] section, choose your repository and hit Save. If it's already saved, you can skip to Test Integration Section.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-11-43-21.png)

3. Login to your Azure DevOps Organization, and select the Team Project that you created in the Prerequisite setup.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-11-24-19.png)

4. When the integration succeeded, you will be taken to the Azure Board. 4 Work items are present and you see a "Success" message

## Test Integration
1. In the Azure Board, create an Issue called [Test]. Remember the Work Item ID that was assigned when you save the work item.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-11-28-12.png)

2. In your GitHub Repository, open the Readme.md file and choose Edit.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-11-30-12.png)

3. Make a textual change, and commit the change with a message that contains the Azure Boards Work Item ID, in the following format 

    ```
    AB#WorkItemID
    ```
    
    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/boards-commit-integration.png)

4. In Azure Boards, find the work item, and see that the code commit has been linked to the work item

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-11-33-26.png)
    
    
Now you can move on to the next page.
