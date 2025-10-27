# Usecase 05 - Deploying chat app on Azure Container Apps with PostgreSQL Flexible Server

**Objective:**

- To configure the development environment on Windows by installing
  Azure CLI, Node.js, assigning Azure subscription roles, starting
  Docker Desktop, and enabling Visual Studio Code with Dev Containers
  extension.

- To deploy and test Custom Chat Application with PostgreSQL and OpenAI
  on Azure.

  ![](./media/lab6.png)

In this use case, you will set up a comprehensive development
environment, deploy a chat application integrated with PostgreSQL, and
verify its deployment on Azure. This involves installing essential tools
like Azure CLI, Docker, and Visual Studio Code ( we have already done it
for you on host env ), configuring user roles in Azure, deploying the
application using Azure Developer CLI, and interacting with the deployed
resources to ensure functionality.

**Key technologies used** -- Python, FastAPI, Azure OpenAI models, Azure
Database for PostgreSQL and azure-container-apps,ai-azd-templates.

**Estimated duration** -- 45 minutes

**Lab Type:** Instructor Led

**Pre-requisites:**

GitHub account -- You are expected to have your own GitHub login
credentials. If you do not have, please create one from here
- +++https://github.com/signup?user_email=&source=form-home-signupobjectives+++

## Exercise 1 : Provision , deploy the application and test it from the browser
## Task 0: Understand the VM and the credentials

In this task, we will identify and understand the credentials that we
will be using throughout the lab.

1.  **Instructions** tab hold the lab guide with the instructions to be
    followed throughout the lab.

2.  **Resources** tab has got the credentials that will be needed for
    executing the lab.

    - **URL** – URL to the Azure portal

    - **Subscription** – This is the ID of the subscription assigned to
      you

    - **Username** – The user id with which you need to login to the
      Azure services.

    - **Password** – Password to the Azure login. Let us call this
      Username and password as Azure login credentials. We will use
      these creds wherever we mention Azure login credentials.

    - **Resource Group** – The **Resource group** assigned to you.

    \[!Alert\] **Important:** Make sure you create all your resources under
    this Resource group

    ![](./media/b1.png)

3.  **Help** tab holds the Support information. The **ID** value here is
    the **Lab instance ID** which will be used during the lab execution.

    ![](./media/b2.png)

##  Task 1 : Register Service provider

1.  Open a browser go to +++https://portal.azure.com+++ and sign in with
    your cloud slice account below.

> Username: <+++@lab.CloudPortalCredential>(User1).Username+++
>
> Password: <+++@lab.CloudPortalCredential(User1).Password>+++
>
   ![](./media/b3.png)
   ![](./media/b4.png)

2.  Click on **Subscriptions** tile.

    ![](./media/b5.png)

3.  Click on the subscription name.

     ![](./media/b6.png)

4.  Expand Settings from the left navigation menu. Click on **Resource
    providers**, enter +++**Microsoft.AlertsManagement+++** and select
    i,t, and then click **Register**.

     ![](./media/b7.png)
     ![](./media/b8.png)

5.  Click on **Resource providers**,
    enter +++**Microsoft.DBforPostgreSQL+++** and select i,t, and then
    click **Register**.
      ![](./media/b9.png)
      ![](./media/b10.png)
      ![](./media/b11.png)
      ![](./media/b12.png)

7.  Repeat the steps \#10 and \#11 to register the following Resource
    providers.

    - **+++Microsoft.Search+++**
    
    - **+++Microsoft.Web+++**
    
    - **+++Microsoft.ManagedIdentity+++**
    
    - **+++Microsoft.Management+++**
    - **+++Microsoft.operationalinsights+++**


### Task 2: Copy the existing resource group name

1.  On Home page, click on **Resource groups**  tile.

      ![](./media/image3.png)

2.  Make sure you already have a resource group created for you to work.
    Never delete this resource group. Instead, you can delete resources
    within the resource group, but not the resource group itself.

3.  Click on resource group name

      ![](./media/image4.png)

4.  Copy the resource group name and save it in Notepad to use for
    deploying all resources into this resource group

     ![](./media/image5.png)


### Task 3 : Open development environment

1.  Open your browser, navigate to the address bar, type or paste the
    following
    URL: +++https://github.com/technofocus-pte/rag-postgres-openai-python2/tree/main+++ tab
    opens and ask you to open in Visual studio code. Select **Open
    Visual Studio Code.**

      ![](./media/image13.jpeg)

2.  Click on **fork** to fork the repo. Give unique name to the repo and
    click on **Create repo** button.

      ![](./media/aa3.png)
      ![](./media/iaa4.png)

3.  Click on **Code -> Codespaces -> Codespaces+**

       ![](./media/aa5.png)

4.  Wait for the Codespaces environment to setup .It takes few minutes
    to setup completely

      ![](./media/img1.png)
      ![](./media/img2.png)

### Task 4: Provision Services and deploy application to Azure

1. In the infra folder, select the main.bicep file to open it.
    ![](./media/img4.png)

2 Navigate to the C:\LabFiles\LabFiles directory, select the main.bicep file, and open it.
   ![](./media/img5.png)

3. Copy the code and replace the contents of the main.bicep file in the Codespace.
    ![](./media/img6.png)
   ![](./media/img7.png)
4. Save the main.bicep file to apply the changes.

5.  Run the following command on the Terminal. It generates the code to
    copy. Copy the code and press Enter.

      +++azd auth login+++

      ![](./media/image19.png)

2.  Default browser opens to enter the generated code to verify. Enter
    the code and click **Next**.

      ![](./media/image20.png)

3.  Sign in with your Azure credentials.

      ![](./media/image21.png)

4.  To create an environment for Azure resources, run the following
    Azure Developer CLI command.It asks you to enter environment name
    .Enter any name of your choice and press enter (eg :+++ragpgpy@lab.LabInstance.Id+++)

    **Note:** When creating an environment, ensure that the name consists of
    lowercase letters.

      +++azd env new+++

      ![](./media/image22.png)
5. Run below command to set resource group

   +++azd env set AZURE_RESOURCE_GROUP {your resource group name}+++
     ![](./media/image29.png)

6.  Run the following Azure Developer CLI command to provision the Azure
    resources and deploy the code.

      +++azd up+++

    
7.  When prompted, select a **subscription** to create the resources and
    select the region closest to your location; in this lab, we have
    chosen the **Sweden Central** region.

      ![](./media/img3.png)

8.  When prompted, **enter a value for the 'openAILocation'
    infrastructure parameter** select the region closest to your
    location; in this lab, we have chosen the **North Central
    US** region

      ![](./media/image26.png)

9.  Provisioning resource will take around 15-16 min. Click **Yes** if
    prompted.

       ![](./media/image27.png)

10. Wait for the template to provision all resource successfully.

     ![](./media/image28.png)

   
13. Wait for the deployment to complete. Deployment takes \<5

      ![](./media/image31.png)

14. Click on the deployed web app endpoint link.

     ![](./media/image32.png)

15. Click on **Open**. It opens new tab with app

     ![](./media/image33.png)

16. The app opens.

      ![](./media/image34.png)

    >[!Alert] Important: If you face any issue launching the app, please redeploy it by following step 12, i.e azd deploy

### Task 5: Use chat app to get answers from files

1.  In the **RAG on database |OpenAI+PoastgreSQL** web app page, **click
    on Best shoe for hiking?** button and observe the output

    ![](./media/image35.png)

     ![](./media/image36.png)

2.  Click on the **clear chat.**

     ![](./media/image37.png)

3.  In the **RAG on database |OpenAI+PoastgreSQL** web app page, click
    on **Climbing gear cheaper than \\$30** button and observe the
    output

      ![](./media/image38.png)

      ![](./media/image39.png)

4.  Click on the **clear chat.**

### Task 6: Verify deployed resources in the Azure portal

1.  On Home page of Azure portal, click on **Resource Groups**.

      ![](./media/image40.png)

2.  Click on your resource group name

      ![](./media/image41.png)

3.  Make sure the below resource got deployed successfully

    - Container App

    - Application Insights

    - Container Apps Environment

    - Log Analytics workspace

    - Azure OpenAI

    - Azure Database for PostgreSQL flexible server

    - Container registry

    ![](./media/image42.png)

4.  Click on **Azure OpenAI** resource name.

    ![](./media/image43.png)

5.  On **Overview** in the left navigation menu, click **Go to Azure AI
    Foundry portal** and select to open a new tab.

      ![](./media/image44.png)

6.  Click on **Shared resources -\>** **Deployments** from left
    navigation menu and make
    sure **gpt-35-turbo**, **text-embedding-ada-002** should be deployed
    successfully

    ![](./media/image45.png)

### Task 7 : Clean up all the resources

To clean up all the resources created by this sample:

1.  Switch back to **Azure portal -\> Resource group- \> Resource group
    name.**

     ![](./media/image46.png)

2.  Select all the resource and then click on Delete as shown in below
    image. (**DO NOT DELETE** resource group)

     ![](./media/image47.png)

3.  Type ``delete`` on the text box and then click on **Delete**.

     ![](./media/image48.png)

4.  Confirm the deletion by clicking on **Delete**.

      ![](./media/image49.png)

5.  Switch back to Github portal tab and refresh the page.

      ![](./media/image50.png)

6.  Click on Code , select the branch created for this lab and click on
    **Delete**.

      ![](./media/image51.png)

7.  Confirm the branch deletion by clicking on **Delete** button.

      ![](./media/image52.png)

>**Summary:**:This use case walks you through deploying a chat application with PostgreSQL and OpenAI on Azure, focusing on cloud-based application
deployment and management. you’ve set up the development environment,
installed necessary tools like Azure CLI, configured Azure resources
using Azure Developer CLI, and deployed the application to Azure
Container Apps.
