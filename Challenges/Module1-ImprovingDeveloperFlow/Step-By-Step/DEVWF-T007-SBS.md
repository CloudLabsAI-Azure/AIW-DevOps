# Step by Step DEVWF-T007

If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/2FgK5SNVFCA/0.jpg)](https://www.youtube.com/watch?v=2FgK5SNVFCA)

In this task, you will use YAML to define 3 GitHub Actions workflows that builds your Docker images and pushes it to a GitHub Container Registry automatically.

1. In your GitHub repository, and select the [Settings] tab.

2. From the left menu, select [Secrets].

3. Select the [New repository secret] button.

    ![Settings link, Secrets link, and New secret button are highlighted.](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/2020-08-24-21-45-42.png)

4. In the [New secret] form, enter the name `CR_PAT` and for the value, paste in a GitHub Personal Access Token, with the following scopes.

    * repo
    * write:packages
    * read:packages

    > You can use the same GitHub PAT that you created in the prerequisite setup and that is now stored in your local settings.json file in the .workshop directory in your GitHub CodeSpace
    >
    > To generate a new GitHub Personal Access Token, please follow the steps described [on this webpage](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/creating-a-personal-access-token).

    ![A screen that show how to add a new secret](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/newsecret.png)

5. Navigate to the GitHub Actions in your repository and select [New Workflow]

    ![A screen that shows how to start a new Workflow for GitHub Actions](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/newworkflow.png)

6. Under the Continuous Integration Workflows, find the [Publish Docker Container] workflow and choose [Set up this workflow]

    ![A screenshot of the GitHub Action for Publishing Docker Files](/Assets/PublishDocker.png)


7. Rename the file to `fabrikam-web.yml`

8. Change the image name to fabrikam-web. This is the name of the container image that will be pushed to the GitHub Container Registry

    ```YAML
    env:
      # TODO: Change variable to your image's name.
      IMAGE_NAME: fabrikam-web
    ```

9. Add a working directory to the [Build Image] and [Push image to GitHub Container Registry] step. This ensure the Docker file can be found

    ```YAML
    - name: Build image
        working-directory: content-web
        run: docker build . --file Dockerfile --tag $IMAGE_NAME

    - name: Push image to GitHub Container Registry
        working-directory: content-web
    ```

10. The workflow for fabrikam-web should look as follows:
    ```yaml
    name: Fabrikam Web Build

    on:
    push:
        # Publish `main` as Docker `latest` image.
        branches:
        - main
        paths:
        - 'content-web/**'
        - '.github/workflows/fabrikam-web.yml'


        # Publish `v1.2.3` tags as releases.
        tags:
        - v*

    # Run tests for any PRs.
    pull_request:

    env:
    # TODO: Change variable to your image name.
    IMAGE_NAME: fabrikam-web

    jobs:
    # Push image to GitHub Packages.
    # See also https://docs.docker.com/docker-hub/builds/
    push:
        runs-on: ubuntu-latest
        if: github.event_name == 'push'

        steps:
        - uses: actions/checkout@v2

        - name: Build image
            working-directory: content-web
            run: docker build . --file Dockerfile --tag $IMAGE_NAME

        - name: Log into GitHub Container Registry
            run: echo "${{ secrets.CR_PAT }}" | docker login https://ghcr.io -u ${{ github.actor }} --password-stdin

        - name: Push image to GitHub Container Registry
            working-directory: content-web
            run: |
            IMAGE_ID=ghcr.io/${{ github.repository_owner }}/$IMAGE_NAME
            VERSION=${{ github.ref }}

            echo IMAGE_ID=$IMAGE_ID
            echo VERSION=$VERSION

            docker tag $IMAGE_NAME $IMAGE_ID:$VERSION
            docker push $IMAGE_ID:$VERSION
    ```

    where the last step can be optimized by putting the image id in lowerscore letters and removing the git ref prefix from version (but this is not mandatory):
    ```
    - name: Push image to GitHub Container Registry
            working-directory: content-web
            run: |
            IMAGE_ID=ghcr.io/${{ github.repository_owner }}/$IMAGE_NAME
            # Change all uppercase to lowercase
            IMAGE_ID=$(echo $IMAGE_ID | tr '[A-Z]' '[a-z]')
            # Strip git ref prefix from version
            VERSION=$(echo "${{ github.ref }}" | sed -e 's,.*/\(.*\),\1,')
            # Strip "v" prefix from tag name
            [[ "${{ github.ref }}" == "refs/tags/"* ]] && VERSION=$(echo $VERSION | sed -e 's/^v//')
            # Use Docker `latest` tag convention
            [ "$VERSION" == "main" ] && VERSION=latest
            echo IMAGE_ID=$IMAGE_ID
            echo VERSION=$VERSION
            docker tag $IMAGE_NAME $IMAGE_ID:$VERSION
            docker push $IMAGE_ID:$VERSION
    ```

11. Commit the file to the repository.

12. The GitHub Action is now running and automatically builds and pushes the container

    ![Screen that shows that the GitHub action build succeeded](/Assets/buildsucceed.png)

13. Next, setup the `content-api` workflow and the `content-init` workflow. Call the files `fabrikam-api.yml` and `fabrikam-init.yml` and change the container names also to `fabrikam-api` and `fabrikam-init`.
*These workflows are very similar to the one shown above, but `fabrikam-web` should be replaced by `fabrikam-api` et cetera.*

14. Navigate to the packages in your GitHub account and see if the container images are present.
    ![Overview of all packages of a GitHub account](/Assets/packages.png)

15. When you are done, pull the changes from your GitHub repository.

    ![](/Assets/2020-10-05-12-10-11.png)
    
 Now, you can move on to the next page.
