# Exercise 4 - Create DevOps Pipeline

Create an Azure DevOps Pipeline for a web based application. Make sure you have installed all the [prerequisites](#Prerequisites).


## Step 1 - Prepare a Solution

1. Open a command prompt or a terminal window


2. Create an ASP.NET MVC application with these command:

       cd %userprofile%\Source
       dotnet new mvc --language C# --name AmazingWebApp --output AmazingWebApp --auth None
       cd AmazingWebApp
       dotnet new sln
       dotnet sln add AmazingWebApp.csproj
       dotnet new gitignore


3. Open this folder in Visual Studio Code with this command:

       code .


4. Click on the Git icon on the left side of the VS [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) then click on "Initialize Repository"

   ![image](https://user-images.githubusercontent.com/121144260/229326591-11ac2033-b0b0-4c66-a7d5-17150fa76f03.png)


5. Open a terminal with View then Terminal

   ![image](https://user-images.githubusercontent.com/121144260/229326915-60ee5ac3-41de-4c2d-8f4f-c81c034d9fa7.png)


6. Enter the following commands:

       git config --global user.email "[macewan profile]@macewan.ca"
       git config --global user.name "Your Name"

    This will allow you to commit files using Git

   ![image](https://user-images.githubusercontent.com/121144260/229326986-94957474-ede9-42ea-a005-0446b52666d7.png)


7. Add all files in the folder to the staging area by clicking the **+** plus sign on the **Changes** line

   ![image](https://user-images.githubusercontent.com/121144260/229331008-0d010c9f-de3c-4c7c-a32a-a980069d169b.png)


8. Commit the code to the local repository by entering an appropriate message then clicking **Commit**

   ![image](https://user-images.githubusercontent.com/121144260/229326822-c264e621-598e-4b7a-8ae8-563fa7d553f9.png)


9. Open a browser window to your Azure DevOps Organisation, usually `https://dev.azure.com/[Your_Organization]` and select **+ New project**

   ![image](https://user-images.githubusercontent.com/121144260/229327070-31a8d8c9-c70f-4dbd-b482-a85df07735d3.png)


10. Set the **Project name** to `AmazingWebProject` and enter a description then click **Create** to launch

    ![image](https://user-images.githubusercontent.com/121144260/229327097-70db8a81-49ec-46bb-bbb5-678a5114d9e2.png)


11. Copy the URL for the remote repository

    ![image](https://user-images.githubusercontent.com/121144260/229327174-69f9cdc0-b223-4f39-9039-e4e050bce22d.png)


12. Go back to Visual Studio Code and access the Source Control panel


13. Click the three dots `...` and select `Remote` then `Add remote`

    ![image](https://user-images.githubusercontent.com/121144260/229331471-1aa34d70-1e62-48e0-a304-503d4d11b5a3.png)


14. Paste the URL from the clipboard and hit enter

    ![image](https://user-images.githubusercontent.com/121144260/229331521-7e38406b-7e5f-4563-8abf-1330bb903f30.png)


15. Enter `main` as the Remote Name then hit Enter

    ![image](https://user-images.githubusercontent.com/121144260/229331856-d1d76f94-6117-4756-99ba-b2261b4329d7.png)


16. If the Git Credentials Manager pops up, enter your MacEwan account details

    ![image](https://user-images.githubusercontent.com/121144260/229331618-a39133cf-b627-416f-a77d-5e0a0d097cd1.png)


17. Use the three dots `...` and select **Push**

    ![image](https://user-images.githubusercontent.com/121144260/229331771-5b902de9-31b9-4a63-a6e9-69bcff4e1e94.png)


18. If asked to push to the remote branch `main` select OK

    ![image](https://user-images.githubusercontent.com/121144260/229331882-b40afde5-440f-491b-b145-5ad13c2caf90.png)




## Step 2 - Create the Pipeline

1. Access your Azure DevOps Project `AmazingWebProject` and check the Repos | Files section to confirm your code has been **push**ed to the remote repository

   ![image](https://user-images.githubusercontent.com/121144260/229331948-6418f667-d8c9-4bf3-a522-cd734d43d7d5.png)


2. Click "Set up build" to start configuring your Pipeline

   ![image](https://user-images.githubusercontent.com/121144260/229332054-56d21af8-ddcb-487a-af64-28ec11f386be.png)


3. Click **Show More** and scroll until you find **ASP.NET Core**

   ![image](https://user-images.githubusercontent.com/121144260/229332118-3d23693a-6a75-4568-b492-80f1a5f1c838.png)


4. Review the generated YAML file and if everything looks correct click **Save and run**

   ![image](https://user-images.githubusercontent.com/121144260/229332167-6683f721-33aa-43d5-b196-afd48215de01.png)


5. Enter a commit message, as the pipeline itself is stored in your repository, then click **Save and run** again

   ![image](https://user-images.githubusercontent.com/121144260/229332183-cfce253b-437a-4af1-8f88-6df080f9b064.png)


6. Click on **Pipelines** to see the status of Pipeline jobs

   ![image](https://user-images.githubusercontent.com/121144260/229332243-92c4cc1e-d6b8-4dbf-b7aa-1ec150aa46d2.png)


7. Review your recently run job to confirm everything build successfully

   ![image](https://user-images.githubusercontent.com/121144260/229332274-b933445b-32a4-4a85-a11c-1a0ea3ef332a.png)


8. Select the last run and review the summary

   ![image](https://user-images.githubusercontent.com/121144260/229332290-f3d4c31c-0b90-4adb-86fb-81e986cf67e5.png)


9. Scroll down to the **Job** section and click to expand

   ![image](https://user-images.githubusercontent.com/121144260/229332331-d9bfb2ac-f9d5-4426-9b09-afa291af6349.png)


10. Review the steps of the build pipeline job

    ![image](https://user-images.githubusercontent.com/121144260/229332584-33d9aa84-d232-4b4b-bee0-a138e2503431.png)




## Prerequisites

1. Download and install [Git CLI](https://git-scm.com/download/)


2. Download and install [Visual Studio Code](https://code.visualstudio.com/Download)


3. Download and install the latest stable [.NET SDK](https://dotnet.microsoft.com/en-us/download)


4. Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) for Visual Studio Code


5. Install the [Azure Repos extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-repos) for Visual Studio Code 


6. Consider also the following extensions:

  * [GitHub Repositories](https://marketplace.visualstudio.com/items?itemName=GitHub.remotehub)
  * [Remote Repositories](https://marketplace.visualstudio.com/items?itemName=ms-vscode.remote-repositories)
