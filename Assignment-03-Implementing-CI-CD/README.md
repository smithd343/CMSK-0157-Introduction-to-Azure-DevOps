# Assignment 3 - Implementing CI/CD


## Step 1 - Azure Resources

1. Sign into the [Azure Portal](https://portal.azure.com/) with your MacEwan profile


2. Create a Resource Group called `AmazingWebApp` in region **Canada Central**

    ![image](https://user-images.githubusercontent.com/121144260/229623245-2e4a6a1d-0323-4a34-8828-22ee6c7d43cb.png)


3. Create an App Service Plan called `AmazingWebPlan` in the `AmazingWebProject` resource group using region **Canada Central**

    ![image](https://user-images.githubusercontent.com/121144260/229623836-213c76a8-28e1-4aec-ba66-e14b6eaad30d.png)

    Use **Linux** for the Operating System and chose the **Free** Pricing Plan


4. Create a Web App called `AmazingWebApp-[macewanprofile]` in the `AmazingWebProject` resource group that publishes **Code** and uses **.NET 7** with the **Linux** Operating System

    ![image](https://user-images.githubusercontent.com/121144260/229624370-f15c2c26-4597-4ede-b967-5e679973fd89.png)

    Use the **AmazingWebPlan(F1)** created in the previous step for the Pricing Plan

    ![image](https://user-images.githubusercontent.com/121144260/229625030-e1a0c48d-df7d-4cc9-98f9-e24d760f51bd.png)

    For the other pages:
    * Under **Deployment**, Disable GitHub actions
    * Under **Networking**, Enable Public Access 
    * Under **Monitoring**, Enable Application Insights


5. Access the `AmazingWebProject` Resource Group to confirm all resources are present

    ![image](https://user-images.githubusercontent.com/121144260/229625624-91aab926-7b24-4d46-8dcb-058d7fdbcaf8.png)




## Step 2 - Configure Azure DevOps connection to Azure

1. Sign into  [Azure DevOps](https://dev.azure.com/) and access your organisation, then select the `AmazingWebProject` created in [Exercise 4](../Exercise-04-Create-Azure-DevOps-Pipeline/README.md)

    ![image](https://user-images.githubusercontent.com/121144260/229626922-40ce9b06-236e-44c9-9ac7-77ebd8fcf715.png)


2. Access the Project Settings, scroll down to Pipelines, and select **Service connections**

    ![image](https://user-images.githubusercontent.com/121144260/229627128-4a54df6b-3ed8-41bb-b97b-0eaed06e46a8.png)


3. Click **Create Service Connection** and pick **Azure Resource Manager** then click **Next**

    ![image](https://user-images.githubusercontent.com/121144260/229627347-404cd96f-3c81-4a49-8e22-295d1bf80bc8.png)


4. Use the Authentication Method of **Service Principal (automatic)**

    ![image](https://user-images.githubusercontent.com/121144260/229627462-4551d94e-db5c-4d74-84a2-4dd685a04539.png)


5. Pick your Subscription then the `AmazingWebProject` Resource Group and give your service connection the name of `Azure-AmazingWebApp`

    ![image](https://user-images.githubusercontent.com/121144260/229632453-cf464605-4fce-448b-9a34-a7a71a7e06e1.png)

    Make sure to check **Grant access to all pipelines** and click Save




## Step 3 - Update the Build Pipeline

1. Select Pipelines to review the available pipelines

    ![image](https://user-images.githubusercontent.com/121144260/229633071-64a67a17-f92b-4cf6-8721-865d2f1b40f2.png)


2. Click on the three dots on the right side of the available pipeline and select **Edit**

    ![image](https://user-images.githubusercontent.com/121144260/229633223-877c6bb5-c593-4ded-984d-f266fcf11108.png)


3. Update the build pipeline to:

  * Follow [deployment best practices](https://learn.microsoft.com/en-us/azure/app-service/deploy-best-practices)
  * Use the [.NET Core](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/dotnet-core-cli-v2?view=azure-pipelines) task to build the solution
  * Use the [.NET Core](https://learn.microsoft.com/en-us/azure/devops/pipelines/ecosystems/dotnet-core?view=azure-devops&tabs=dotnetfive) task to publish the pipleline artifact

<details>
<summary>This isn't an example build file</summary>
  
```yaml
# Build-AmazingWebProject

trigger:
- master

pool:
  vmImage: ubuntu-latest

variables:
  buildConfiguration: 'Release'

steps:
- task: DotNetCoreCLI@2
  displayName: 'Build AmazingWebProject'
  inputs:
    command: 'build'
    projects: '**/*.sln'
    arguments: '--configuration $(buildConfiguration)'

- task: DotNetCoreCLI@2
  displayName: 'Publish AmazingWebProject'
  inputs:
    command: 'publish'
    publishWebProjects: true
    zipAfterPublish: true
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'

- task: PublishBuildArtifacts@1
  displayName: 'Publish Build Artifacts'
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'AmazingWebProject'
    publishLocation: 'Container'
```
  
</details>


4. Review the Build and Publish tasks to make sure they completed successfully

    ![image](https://user-images.githubusercontent.com/121144260/229635682-90843cf4-e7af-4c69-816c-ee409ba575fa.png)




## Step 4 - Create the Deploy Pipeline

1. Select Pipelines | Release

    ![image](https://user-images.githubusercontent.com/121144260/229635920-9c874180-6dc7-4539-bc07-9ea7606838c2.png)


2. Select **New pipeline** and pick or search for `Azure App Service deployment`

    ![image](https://user-images.githubusercontent.com/121144260/229636057-2d510112-9c8e-4e32-9e1e-ece9888e4afc.png)


3. Change the **Stage name** to `Deploy`

    ![image](https://user-images.githubusercontent.com/121144260/229636449-83bd9d51-e7a3-432f-9501-c002de5af58f.png)


4. Add an Artifact

    ![image](https://user-images.githubusercontent.com/121144260/229636595-513c807f-25f7-4f14-b8d4-ff7645c03aee.png)


5. Use the Build Artifact created by the Build Pipeline

    ![image](https://user-images.githubusercontent.com/121144260/229636783-193144d0-bab0-4e44-9365-573c6f0fbeb8.png)


6. Configure the deployment tasks

     ![image](https://user-images.githubusercontent.com/121144260/229636840-d617a805-16a0-44e9-96b0-dad1b9e93c9b.png)


7. Change the **Agent job** details to use the **Agent pool** of ``Azure Pipelines`` and the **Agent Specificatin** of `ubuntu latest`

    ![image](https://user-images.githubusercontent.com/121144260/229637243-1dc1e016-ca17-405c-8bc6-9ac0573684d3.png)


8. Change the **Deploy Azure App Service** details to use the Connection you created

    ![image](https://user-images.githubusercontent.com/121144260/229637466-90930452-a870-4c5c-8f29-224b18ba645a.png)

    For the other settings:
    * Make sure the **App Service type** is set to `Web App on Linux`
    * Set the **App Service name** to `AmazingWebApp-[macewan profile]`
    * Pick `7.0 (DOTNETCORE|7.0)` as the **Runtime Stack**


9. Click the pencil icon next to the pipeline name and change the name to `Deploy-AmazingWebApp`

    ![image](https://user-images.githubusercontent.com/121144260/229638397-fdd0243c-4141-45f5-893f-2141ff5c0949.png)


10. Click the **lightning bolt** and enable the **Continuous deployment trigger**

    ![image](https://user-images.githubusercontent.com/121144260/229638736-6dcec603-3b22-4e89-9ec5-219d08dcdeb4.png)


11. Click **Save** and pick the default folder

     ![image](https://user-images.githubusercontent.com/121144260/229638107-1db44daa-6322-4482-9179-b84d00ddfb3a.png)




## Step 5 - Update the Repository

1. Under Pipelines, select `Build-AmazingWebProject` then click the three dots and select **Status Badge**

    ![image](https://user-images.githubusercontent.com/121144260/229640083-694b8e76-d83c-4c31-bba7-ce9317db5d2b.png)


2. Copy the generated markdown code to your clipboard

    ![image](https://user-images.githubusercontent.com/121144260/229640174-355930d1-adec-4a0f-ae06-a5d5bb27dea7.png)


3. Access our Repos | Files for the `master` branch

    ![image](https://user-images.githubusercontent.com/121144260/229639308-83060a43-d6cd-43ee-aff7-61f73cd14771.png)


4. Use the three dots to access the New File selection

    ![image](https://user-images.githubusercontent.com/121144260/229639402-4150017c-dfba-41fa-a531-a2d73d5c7776.png)


5. Create a README.md file

    Add in various sections and paste in the copied markdown code

<details>
<summary>This isn't an example readme file</summary>
  
```md
# Amazing Web Project


## Getting started

TODO: List steps on how to set up their development environments and clone this repository


## Build and Test

TODO: Describe how the code is automatically build and deployed
TODO: Add some code tests

## Contributors

Yourname (Owner)

  
## Current Status

[![Build Status](https://dev.azure.com/deanwsmith/AmazingWebProject/_apis/build/status%2FBuild-AmazingWebProject?branchName=master)](https://dev.azure.com/deanwsmith/AmazingWebProject/_build/latest?definitionId=1&branchName=master)
```
  
</details>


6. Commit the new README.md file directly to the `master` branch

    ![image](https://user-images.githubusercontent.com/121144260/229640371-5082a1f3-3d4e-4aa5-9753-5f72655bb8e1.png)


7. A push to the `master` branch will trigger the build pipline - review the status of the job

    ![image](https://user-images.githubusercontent.com/121144260/229640662-f16519ff-04fe-43a1-a98e-b4d49f13f01a.png)


9. If the build task was successful it should trigger the deploy pipleine - review their status of the job

    ![image](https://user-images.githubusercontent.com/121144260/229648664-380d6724-f072-4ce1-b3c4-3ff5e16dc754.png)


10. In Azure access your **Web App** `AmazingWebApp-[macewanprofile]` and in the **Overview** section copy the **Default domain** to your clipboard

    ![image](https://user-images.githubusercontent.com/121144260/229648737-6b5d1acb-bf64-4196-81d4-06f870ee2753.png)


11. Access your AmazingWebApp hosted on Azure

    ![image](https://user-images.githubusercontent.com/121144260/229648824-f7c079f7-e11e-4c39-9c16-96053adec345.png)
