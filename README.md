# Azure_Deployment_on_ACA
This Azure Task allows users to easily deploy their application source to an Azure Container App by providing a previously built image, a Dockerfile that an image can be built from 

## Pipeline Requirements

This task requires the following parameters to be defined:

Parameters:

| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | :-------------: | :-------------: | ------------- |
| dockerImage | Docker image to build | String |  |  | Required | Specify the Docker image to build |
| dockerImageTag | Docker image tag | String |  |  | Required |  |
| azureSubscription | Azure Resource Manager connection | String |  |  | Required | Specify an Azure Resource Manager service connection for the deployment. This service connection must be linked to the user's Azure Subscription where the Container App will be created/updated. |
| resourceGroup | Azure resource group name | String |  |  | Optional | The existing resource group that the Azure Container App will be created in (or currently exists in). If not provided, this value will be in the form of <container-app-name>-rg |
| containerAppName | Azure Container App name | String |  |  | Required | The name of the Azure Container App that will be created or updated. If not provided, this value will be in the form of ado-task-app-<build-id>-<build-number> |


These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/Azure_Deployment_on_ACA
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: ContainerAppDeployment.yaml
    parameters:
      azureSubscription: ${{ parameters.azureSubscription }}
      containerAppName: ${{ parameters.containerAppName }}
      resourceGroup: ${{ parameters.resourceGroup }}
      dockerImage: ${{ parameters.dockerImage }}
      dockerImageTag: ${{ parameters.dockerImageTag }}
        
  
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```
