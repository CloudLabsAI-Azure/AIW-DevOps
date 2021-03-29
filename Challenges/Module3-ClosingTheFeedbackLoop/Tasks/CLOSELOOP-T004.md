# Deploy latest validated version with automated approvals

Everything is looking great. The Azure DevOps pipeline is running, and is building and pushing the latest version to the Azure WebApp. However, there is some confusion about the tag "latest". What is the latest version? Since the container images are also tagged with a build number, the team wants to make it explicit that the deployment uses the version instead of the latest version.

Furthermore, it happens that developers update the docker-compose file locally, to use their own container images, and sometimes this slips into the committed source code. The team wants to fix this to make the pipeline even more robust.

## Challenge

In this challenge you are going to replace the `:latest` tag in the docker-compose file with the build number from the pipeline. You will also add an automated check to the pipeline to validate if images are only coming from your own GitHub repository using an automated policy. 

## Validation

* Pipeline contains script to deploy versioned containers
* Production environment contains an [Evaluate Artifact] automated approval that checks if the container registry is on a whitelist

> Tips:
> Use the PowerShell task in the Azure Pipeline to replace the :latest tag in the docker-compose file with the version of the build
>
> ```YAML
> - powershell: (gc .\docker-compose.yml) -replace ':latest',':$(Build.BuildNumber)' | set-content .\docker-compose.yml
> ```



