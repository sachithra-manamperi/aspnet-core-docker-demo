# ASP.NET Demo App with YAML CI/CD Pipeline Configuration Edited

# Azure DevOps Pipeline Explanation

This Azure DevOps pipeline is used to build and deploy a .NET Core web application as a Docker container to an Azure App Service.

## Trigger

The pipeline is triggered whenever a change is pushed to the `master` branch.

## Variables

- `buildConfiguration`: Specifies the build configuration (Release in this case).
- `location`: Specifies the Azure region to deploy the resources to (West US 2 in this case).
- `acrHostName`: Specifies the hostname of the Azure Container Registry (ACR) to store the Docker images.
- `acrName`: Specifies the name of the ACR.
- `rgName`: Specifies the name of the Azure Resource Group.
- `imageName`: Specifies the name of the Docker image to be built and deployed.
- `webAppName`: Specifies the name of the Azure App Service to deploy the Docker container to.

## Stages

### Build and Test

This stage has the following jobs:

- `BuildAndTest`: This job is responsible for building, testing, and publishing the web application as a Docker container.

#### Steps

1. **Create or update the ACR resource:** This task creates or updates the Azure Container Registry.
2. **Use .NET Core SDK:** This task installs the .NET Core SDK.
3. **Restore dependencies:** This task restores the NuGet packages required for the web application.
4. **Build app:** This task builds the web application.
5. **Run unit tests:** This task runs the unit tests for the web application.
6. **Publish the app:** This task publishes the web application as a Docker container.
7. **Build container image:** This task builds the Docker image for the web application.
8. **Push container image:** This task pushes the Docker image to the Azure Container Registry.
9. **Copy ARM templates:** This task copies the ARM templates required for deployment.
10. **Publish the app as an artifact:** This task publishes the web application as an artifact.

### Staging Release

This stage has the following job:

- `Release`: This job is responsible for deploying the Docker container to the Azure App Service.

#### Steps

1. **Don't clone the repo:** This step skips cloning the repository.
2. **Download the published application artifact:** This step downloads the artifact published in the previous stage.
3. **Create or update Azure App Service:** This task creates or updates the Azure App Service.
4. **Deploy App Service:** This task deploys the Docker container to the Azure App Service.
