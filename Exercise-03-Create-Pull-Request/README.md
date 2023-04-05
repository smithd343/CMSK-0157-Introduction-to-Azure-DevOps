# Exercise 3 - Create a Pull Request

Create a pull request on a repository.


## Part 1 - Set up Remote Repository in Azure DevOps

1. Access your [Azure DevOps](https://dev.azure.com/) organisation

2. Create a new project called `AmazingConsoleProject`

![image](https://user-images.githubusercontent.com/121144260/228673893-0af42f10-6ef8-4404-a1ef-d65ae4f15427.png)

3. Select Repos and scroll to the bottom, unselect "Add a README", then select **VisualStudio**

![image](https://user-images.githubusercontent.com/121144260/228674536-a2976b0f-410c-4054-b2cd-324f8d9f3755.png)

4. Click **Initialize** to set up your repository

5. Select Repos then Branches

6. Click **New branch**

7. Enter the branch name as feature1, ensure it is based on main

![image](https://user-images.githubusercontent.com/121144260/228674801-00440e3b-504c-4591-83f0-4f3fbfe00ed7.png)

8. Click **Create** to create your new branch

9. Select Repos then Files

10. Click **Clone** and copy the URL to the clipboard

![image](https://user-images.githubusercontent.com/121144260/228675321-fe661f21-bb1a-42e7-9dd5-b3c660e51eef.png)



## Part 2 - Clone the Repository in Visual Studio 2022

1. Open [Visual Studio](https://visualstudio.microsoft.com/vs/) and select **Clone a Repository**

![image](https://user-images.githubusercontent.com/121144260/228675750-d9dae3af-e69b-47d2-826d-2cd387723458.png)

2. Paste the URL from your clipboard into the **Repository location** field:

![image](https://user-images.githubusercontent.com/121144260/228675868-7099b995-12e5-4b74-bb7d-18ab3571e167.png)

3. If the git credentials appears, sign in with your MacEwan account

4. In Visual Studio under Solution Explorer click Folder View

![image](https://user-images.githubusercontent.com/121144260/228676302-ea9887f0-f74d-40ac-9c89-e5347457c90d.png)


## Part 3 - Set up Git in Visual Studio

1. In Visual Studio, select the **Git Changes** panel on the right side

2. Click on **main** and set the local branch to **feature1**

![image](https://user-images.githubusercontent.com/121144260/228682369-b7c14c55-85c6-4746-ba52-b6eedf75cb72.png)

3. Click on **feature1** and set the remote branch also to **feature1**

4. Select Git then Settings and make sure your **User name** and **Email** are correct

![image](https://user-images.githubusercontent.com/121144260/228682678-3d14fb36-8487-468c-b435-948840faac6b.png)



## Part 4 - Add a Console Project

1. In Visual Studio select File, then New, then **Project**

![image](https://user-images.githubusercontent.com/121144260/228677021-6a01e22e-bd1c-47b0-9a00-aeee7f7cc276.png)

2. Search for **Console App** and select the C# version then click **Next**

![image](https://user-images.githubusercontent.com/121144260/228677293-67c81705-118e-4180-856f-12e0c1bea1bc.png)

3. Use **Project name** AmazingConsoleProject and under Solution select **Add to solution** then click **Next**

![image](https://user-images.githubusercontent.com/121144260/228677540-1c82f583-c344-4907-b06f-b45e139358ec.png)

4. Select Frameworkd **.NET 7.0** or **.NET 6.0** depending on what is on your local workstation and click **Create**

![image](https://user-images.githubusercontent.com/121144260/228677677-935ea0d1-578b-40e8-80d5-fc2963395a22.png)

5. Change the `Console.WriteLine` details to say **This is an Amazing Console Project!**

![image](https://user-images.githubusercontent.com/121144260/228677998-8879a4b9-4470-4922-9a8f-4eb3183acb82.png)



## Part 5 - Review and Commit your Changes to Local Repository

1. In Visual Studio, select the **Git Changes** panel on the right side

![image](https://user-images.githubusercontent.com/121144260/228678232-ca4bf770-72c1-4403-8c5d-89c86b9ee8d7.png)

2. There should be two items that have been Added to the Staging Area

![image](https://user-images.githubusercontent.com/121144260/228678528-48daf460-5ea5-4f45-a027-ba1dc0e14476.png)

3. In the Commit Message box, enter "Added Console App and changed initial output" and click **Commit All**

![image](https://user-images.githubusercontent.com/121144260/228678769-940dd65e-169b-4d97-9ae9-4f5e9728e078.png)

4. At this point, your local repository **feature1** contains the new console app

![image](https://user-images.githubusercontent.com/121144260/228682957-2bc2aeed-985a-4c00-9432-7e72bcc470a7.png)



## Part 6 - Push Changes to Remote Repository

1. Under the **Git Changes** panel, click the **Push** icon (or select Git then Push)

![image](https://user-images.githubusercontent.com/121144260/228683108-0b1ad297-ebec-4177-afa0-2a28225f7041.png)

2. Check for confirmation in the Visual Studio **Git Changes** panel

![image](https://user-images.githubusercontent.com/121144260/228683328-c41042d7-978d-41a9-b27d-82e82d1921a8.png)

3. Access your Azure DevOps project and confirm that the **main** branch has no changes

![image](https://user-images.githubusercontent.com/121144260/228683389-027c43f8-99d4-4442-a4a1-ddc239102448.png)

4. Switch to the **feature1** branch and confirm the two new files are present

![image](https://user-images.githubusercontent.com/121144260/228683582-60fb92be-cff0-4716-9536-3a13cbb86526.png)



## Part 7 - Create Pull Request

1. Access your Azure DevOps **AmazingConsoleProject** project and select Repos then Pull Requests

![image](https://user-images.githubusercontent.com/121144260/228683910-cb93656d-ccf0-4d7f-ab9b-69044e123e0c.png)

2. Your DevOps site will suggest that **feature1** was updated and that a pull request should be raised - click on **Create a pull request**

3. Review the pull request details, confirming this is a pull from **feature1** into **main**, check the files affected, check the commits included

![image](https://user-images.githubusercontent.com/121144260/228684242-905cc48d-2884-43fd-8bbd-66c4df057ce7.png)

4. Click Create when you have reviewed the **Pull Request** content

5. The **Pull Request** will be displayed for you to Complete - at this point you have the option to reject, request feedback, or create comments for others to review

![image](https://user-images.githubusercontent.com/121144260/228684590-e74fd92a-8cff-4dcc-875d-fe28cd9a2553.png)

6. Click **Complete** and confirm the merge type of merge, and make sure **feature1** is deleted after merging

![image](https://user-images.githubusercontent.com/121144260/228684900-978491da-9841-4d7d-8ad0-df0e9d016eb5.png)

7. The Azure DevOps site will process the merge and set the status to **Completed**

![image](https://user-images.githubusercontent.com/121144260/228685000-3322fad8-be40-49f5-b883-efb0f7387211.png)

8. Select **Repos** then **Files** and confirm that branch **main** now contains the content from branch **feature1**

![image](https://user-images.githubusercontent.com/121144260/228685140-fd91498d-f625-4c26-94b2-81804f9f4570.png)



## Conclusion

These steps show how to:

* Create an Azure DevOps Project
* Clone the Repository into Visual Studio 2022
* Set up your Git environment in VS 2022 to use the **feature1** branch
* Add a Console App project to the cloned repository
* **Commit** your changes to the local repository
* **Push** the changes to the remote repository
* Create a **Pull Request** to merge the changes from the **feature1** branch into the **main** branch
