# Step by Step DEVWF-T005

If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/rjdF-JjZm6Q/0.jpg)](https://www.youtube.com/watch?v=rjdF-JjZm6Q)

In this task, you will enable the GitHub security features for your repository we can do that by navigating to security tab .

1. In your GitHub repository, navigate to the **Security** Tab. Press the **Enable Dependabot alerts** button and the **Set up Code Scanning** button

    ![Enable Dependabot and Code Scanning Alerts](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/securityfeatures.png)

2. In the Dependabot features, enable Dependabot Alerts and Dependabot security updates

3. In the Code Scanning features, select the CodeQL Analysis workflow. This workflow is a GitHub Action that runs every time you check in some code to the main branch

    ![Setup this Workflow in CodeQL](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/CodeQLAction.png)

4. Save the workflow by pressing the **Start Commit** button

5. To solve a Dependabot issue, navigate to the Security Tab and press View Dependabot Alerts. when there is nothing to see, the Dependabot engine is still running. Wait a few minutes and refresh the screen

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-12-51-55.png)

6. Find the **handlebars** vulnerability and open this by clicking on the title.
   
   **Note** : If you don't see **handlebars** vulnerability this means a pullrequest was automatically created and merged, you can skip step 6-8 and continue from step 9.
   
   ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/handlebars.png)

7. Press the Create Dependabot Security update button. This may take a couple of seconds.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-13-03-26.png)

8. In the Pull Requests, find the the Dependabot Security patch, and merge the Pull Request to your main branch

9. To solve a Code Scanning issue, navigate to the Security Tab and press **View Alerts** next to Code Scanning alerts.

10. Select an issue and then from the details select "Won't Fix"

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-13-10-25.png)

11. When you are done, pull the changes from your GitHub repository.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-12-10-11.png)
    
    
 Now, you can move on to the next page.
