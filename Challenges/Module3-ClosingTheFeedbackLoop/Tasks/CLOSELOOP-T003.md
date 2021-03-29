# Increase control with Azure DevOps CI/CD

Now that the Continuous Delivery pipeline has been set up, the product owner notices that changes, that she wants to announce all at once, are ending up straight into production. Even worse, some customers complain about these new features and unknown behavior. One of the developers mentions to start using feature flags to hide certain functionality. That is a great idea, but for now this is too much work and too complicated to set up. The team decides wants to set up a manual approval workflow to allow the product owner to approve changes before they end up in production. 

After some research they find that GitHub Actions is very good at automation and is more then sufficient for the developer workflow. But a more enterprise requirement, like adding approvals, is very hard with GitHub. You and your team advise to look at Azure DevOps again. Since all work is already registered there, it makes sense to build the build and release pipeline within Azure DevOps, and implement the manual approval. Furthermore, the integration between GitHub and Azure DevOps is great with the Azure Pipelines extension

## Challenge

In this challenge you are going to setup a CI/CD pipeline in Azure DevOps that gets the sources from GitHub. The pipeline will have 1 deployment stage that deploys to the production environment. This has an manual approval gate. 

## Validation

* GitHub Actions are disabled
* Azure DevOps YAML Pipeline created with a build stage, that uses docker compose to build and publish images to the GitHub Container Registry
* Azure DevOps pipeline build sources from the GitHub repository
* DeployProd stage added that deploys the infrastructure with the `deploy-infrastructure.ps1` file
* WebApp deployed from the pipeline using the docker-compose file
* Secret added for GitHub Container Registry
* Environment production added to the pipeline with a manual approval


