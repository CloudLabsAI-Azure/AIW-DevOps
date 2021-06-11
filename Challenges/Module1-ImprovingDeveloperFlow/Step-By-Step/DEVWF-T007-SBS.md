# Step by Step DEVWF-T007

If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/2FgK5SNVFCA/0.jpg)](https://www.youtube.com/watch?v=2FgK5SNVFCA)

In this task, you will use YAML to define 3 GitHub Actions workflows that builds your Docker images and pushes it to a GitHub Container Registry automatically.

1. In your GitHub repository, and select the **Settings** tab.

2. From the left menu, select **Secrets**.

3. Select the **New repository secret** button.

    ![Settings link, Secrets link, and New secret button are highlighted.](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-08-24-21-45-42.png)

4. In the **New secret** form, enter the name `CR_PAT` and for the value, paste in a GitHub Personal Access Token, with the following scopes.

    * repo
    * write:packages
    * read:packages

    > You can use the same GitHub PAT that you created in the prerequisite setup and that is now stored in your local settings.json file in the .workshop directory in your GitHub CodeSpace
    >
    > To generate a new GitHub Personal Access Token, please follow the steps described [on this webpage](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/creating-a-personal-access-token).

    ![A screen that show how to add a new secret](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/newsecret.png)

5. Navigate to the GitHub Actions in your repository and select **New Workflow**

    ![A screen that shows how to start a new Workflow for GitHub Actions](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/newworkflow.png)

6. Click on Setup a workflow yourself

    ![A screenshot of the GitHub Action for Publishing Docker Files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/worksflow.png)

7. Rename the file to `fabrikam-web.yml`.

8. Delete the content present in your yaml file.

9. Navigate to this link ```https://github.com/CloudlabsAI-Git/code-to-cloud/blob/main/fabrikam-web``` to get the fabrikam-web.yml file content . Copy the content of the file and paste it in your newly created `fabrikam-web.yml` file in GitHub.

10. Change the name and image name to fabrikam-web. This is the name of the container image that will be pushed to the GitHub Container Registry.
   
    ```YAML
    env:
      # TODO: Change variable to your image's name.
      IMAGE_NAME: fabrikam-web
    ```
    
    ![A screenshot of the GitHub Action for Publishing Docker Files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/worksflow.png)


10. Add a working directory in the **Build Image** and **Push image to GitHub Container Registry** step should be added as below.

    ```YAML
            - name: Build image
                working-directory: ./content-web
                run: docker build . --file Dockerfile --tag $IMAGE_NAME

            - name: Push image to GitHub Container Registry
                working-directory: ./content-web
     ```

     ![A screenshot of the GitHub Action for Publishing Docker Files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/worksflow.png)
     

11. Commit the file to the repository.

12. The GitHub Action is now running and automatically builds and pushes the container

    ![Screen that shows that the GitHub action build succeeded](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/buildsucceed.png)

13. Next, setup the `content-api` workflow and the `content-init` workflow the same way you setup for fabrikam-web.yml , copy the content from ```https://github.com/CloudlabsAI-Git/code-to-cloud/blob/main/fabrikam-web``` and replace the container name and working directory

14. Navigate to the packages in your GitHub account and see if the container images are present.
    ![Overview of all packages of a GitHub account](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/packages.png)

15. When you are done, pull the changes from your GitHub repository.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-10-05-12-10-11.png)
    
 Now, you can move on to the next page.
