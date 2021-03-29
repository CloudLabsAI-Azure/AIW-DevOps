# Step by Step DEVWF-T003

If you rather watch a video with step by step instructions, you can do that here
[![Step by Step Video](https://img.youtube.com/vi/dHYOyyfUhNQ/0.jpg)](https://www.youtube.com/watch?v=dHYOyyfUhNQ)

In this task, you will create 3 Dockerfiles that will be used to build and run the WEB, API and INIT application as a containerized application.

1. From your GitHub repository open your Codespace if it is not already

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/OpenCodeSpace.png)

2. In the Terminal window, open a PowerShell Terminal by typing `pwsh`

3. In your explorer on the GitHub Codespace, navigate to the `content-api` folder and create a new file called `Dockerfile`.

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/create-dockerfile.gif)
    
   We can also create Docker file by using command ```vi Dockerfile``` after this **i** to insert the content then **Esc** and then **:wq**

4. Open the Gist (containing the example definition of the API Dockerfile), from the location given below and paste the contents in to your newly created Dockerfile.

    ```
    https://gist.github.com/renevanosnabrugge/b2390f11c45671f6d0a9c6c9bb2c01ca
    ```

5. In your Terminal window, navigate to the **content-api** directory and then execute the next command.

    ```
    cd /workspaces/CodeToCloud-Source/content-api
    ```

    ```bash
    pushd
    ```
``` Note : Every time you use the pushd command, a single directory is stored for your use. However, you can store multiple directories by using the pushd command multiple times. The directories are stored sequentially in a virtual stack, so if you use the pushd command once, the directory in which you use the command is placed at the bottom of the stack. If you use the command again, the second directory is placed on top of the first one. The process repeats every time you use the pushd command.```

6. From the content-api folder containing the API application files and the new Dockerfile you created, type the following command to create a Docker image for the API application. This command does the following:

   - Executes the Docker build command to produce the image
   - Tags the resulting image with the name `fabrikam-api` (-t)
   - The final dot (`.`) indicates to use the Dockerfile in this current directory context. By default, this file is expected to have the name "Dockerfile" (case sensitive).

   ```bash
   docker build -t fabrikam-api .
   ```

7. Once the image is successfully built, run the Docker images listing command. You will see several new images: the node images and your container image [fabrikam-api].

   ```bash
   docker images
   ```

8. Repeat steps 3-7 but store the Dockerfile in the folder **content-web**, call the Docker image **fabrikam-web** and use the below Gist to get the contents of the Dockerfile

    ```
    https://gist.github.com/renevanosnabrugge/251e01fa380c10c8282ffc7f11ff0526
    ```

     > Note: Ensure to change the directory to **content-web** in step 3 and Step 5.
    
9. Repeat steps 3-7 but store the Dockerfile in the folder **content-init**, call the Docker image **fabrikam-init** and use the below Gist to get the contents of the Dockerfile

    ```
    https://gist.github.com/renevanosnabrugge/5178c88a09e8c6cdd66a2eb0dc6dcba2
    ```

     > Note: Ensure to change the directory to **content-init** in step 3 and Step 5.

10. Now that the images have been successfully built, you should be able to see them in your terminal window, when executing the `docker images` command.

    ![In this screenshot of the terminal window, docker images has been typed and it shows the 3 containers that were built.](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/DockerImages-Fabrikam.png)

Now that you have created 3 Docker images for your application, it is time to run the application.

11. Make sure you remove all running images to avoid conflict with ports in use. When you run `docker ps -a` you see all containers that are running or are stopped. Remove all containers, except the `cloudenvimage`. The `cloudenvimage` contains you GitHub Codespace. 

    ```
    docker ps -a
    ```
    
    ```bash
    docker rm -f <containername or id>
    ```

12. Check if your `fabrikam` network is still around by running the command 

    ```
    docker network ls
    ````

13. Start the MongoDB container and the `fabrikam-init` container you just created and run them on the `fabrikam network` to prepare the database. The command does the following.

    - Starts a Mongo container with a name mongo (--name) in the background (-d) running on port 27017 (-p) and connected to the network `fabrikam` (--net)
    - Starts the `fabrikam-init` container in an interactive terminal (-ti) and connected to the network `fabrikam` (--net)

    ```bash
    docker run -d --name mongo --net fabrikam -p 27017:27017 mongo

    docker run -ti --name init --net fabrikam fabrikam-init
    ```

14. Now start the `fabrikam-api` container running on port 3001 and the `fabrikam-web` container running on port 3000

    ```bash
    docker run -d --name api -p 3001:3001 --net fabrikam fabrikam-api
    docker run -d --name web -p 3000:80 --net fabrikam fabrikam-web
    ```

Note : If you face error as Port 3000 or Port 3001 is already in use. please follow the steps below:

* Run command **lsof -i : portnumber** , replace portnumber with the port in which you are facing issue

* After running the command you will get process id 
 
* run the command **kill -9 processid**

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/port-issue.gif)

15. In your GitHub Codespace, navigate to the Remote Explorer and forward the ports `3000` and `3001` to make them available on the web. Click the Globe Icon to navigate to the Web Application (port 3000).

    ![](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/port-forward.gif)

    ![![Screen showing the remote explorer where ports 3000 and 3001 are forwarded.]](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/OpenBrowser.png)

16. In the web application, click the Speakers Menu items, to validate if data is loaded from the API and the Database, both running in a container.

    ![Screen showing data in the Neuro Web application](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/neuroconf-screen.png)

17. When you are done, **commit** and **push** your changes to your GitHub repository.

    ![Commit and purh your container to the registry](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-DevOps/main/Assets/commitandpush.png)
