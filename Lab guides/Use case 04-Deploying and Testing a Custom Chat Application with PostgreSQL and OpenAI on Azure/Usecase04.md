# **Use case 04-Deploying and Testing a Custom Chat Application with PostgreSQL and OpenAI on Azure**

**Introduction**

This scenario creates a web-based chat application with an API backend
that can use OpenAI chat models to answer questions about the items in a
PostgreSQL database table. The frontend is built with React and
FluentUI, while the backend is written with Python and FastAPI.

This scenario provides the following features:

- Hybrid search on the PostgreSQL database table, using [the pgvector
  extension](https://github.com/pgvector/pgvector) for the vector search
  plus [full text
  search](https://www.postgresql.org/docs/current/textsearch-intro.html),
  combining the results using RRF (Reciprocal Rank Fusion).

- OpenAI function calling to optionally convert user queries into query
  filter conditions, such as turning "Climbing gear cheaper than $30?"
  into "WHERE price \< 30".

- Conversion of user queries into vectors using the OpenAI embedding
  API.

     ![](./media/image1.png)

In this use case, you will set up a comprehensive development
environment, deploy a chat application integrated with PostgreSQL, and
verify its deployment on Azure. This involves installing essential tools
like Azure CLI, Node.js, Docker, and Visual Studio Code, configuring
user roles in Azure, deploying the application using Azure Developer
CLI, and interacting with the deployed resources to ensure
functionality.

**Objective:**

- To configure the development environment on Windows by installing
  Azure CLI, Node.js, assigning Azure subscription roles, starting
  Docker Desktop, and enabling Visual Studio Code with Dev Containers
  extension.

- To deploy and test Custom Chat Application with PostgreSQL and OpenAI
  on Azure.

## Exercise 1: set up environment

## Task 1: Install Azure Cli and set the policy scope to Local machine

1.  In your windows search bar, type **PowerShell**. In the
    **PowerShell** dialog box, navigate and click on **Run as
    administrator**. If you see the dialog box - **Do you want to allow
    this app to make changes to your device?** then click on the **Yes**
    button.

      ![](./media/image2.png)

2.  Run the following command to install Azure Cli on the PowerShell

PowerShell copy

+++winget install microsoft.azd+++
      ![](./media/image3.png)

3.  Run the below command to set the policy to **Unrestricted** and
    enter **A** when asked to change the execution policy.

+++Set-ExecutionPolicy Unrestricted+++
      ![](./media/image4.png)

## Task 2: Install Node.js

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:+++https://nodejs.org/en/download/+++ then press the
    **Enter** button.

     ![](./media/image5.png)

2.  Select and click on **Windows Installer**.

      ![](./media/image6.png)

3.  **Node-V** file will be downloaded. Click on the downloaded file to
    set up **Node.js**

      ![](./media/image7.png)

4.  In the **Welcome to the Node.js Setup Wizard** window, click on the
    **Next button**.
 
      ![](./media/image8.png)

5.  In the **End-User License Agreement** window, select **I accept the
    terms in the License agreement** radio button and click on the
    **Next** button.

      ![](./media/image9.png)

6.  In the **Destination Folder** window, click on the **Next** button.

      ![](./media/image10.png)

7.  In the **Custom Setup** window, click on the **Next** button.

      ![](./media/image10.png)
      ![](./media/image11.png)

8.  In Ready to install Node.js window, click on **Install.**

      ![](./media/image13.png)

9.  In **Completing the Node.js Setup Wizard window**, click on the
    **Finish** button to complete the installation process.

       ![](./media/image13.png)

## Task 3: Assign a user as an owner of an Azure subscription

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL: +++https://portal.azure.com/+++, then press the
    **Enter** button.

      ![](./media/image15.png)

2.  In the **Microsoft Azure** window, use the **User Credentials** to
    login to Azure.

      ![](./media/image16.png)

3.  Then, enter the password and click on the **Sign in** button**.**

       ![](./media/image17.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

      ![](./media/image18.png)
5.  Type in **Subscriptions** in the search bar and select
    **Subscriptions**.

      ![](./media/image19.png)

6.  Click on your assigned **subscription**.

      ![](./media/image20.png)

7.  From the left menu, click on the **Access control(IAM).**

      ![](./media/image21.png)

8.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

      ![](./media/image22.png)

9.  In the Role tab, select the **Privileged administrator roles** and
    select **Owner** . Click **Next**

      ![](./media/image23.png)
      ![](./media/image24.png)

10. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

      ![](./media/image25.png)

11. On the Select members tab , select your Azure OpenAI credentials and
    click **Select.**

       ![](./media/image26.png)

12. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

      ![](./media/image27.png)
      ![](./media/image28.png)

13. You will see a notification – added as Owner for Azure
    Pass-Sponsorship.

      ![](./media/image29.png)

## Task 4: Run the Docker

1.  In your Windows search box, type Docker , then click on **Docker
    Desktop**.

      ![](./media/image30.png)

2.  Run the Docker Desktop.

     ![](./media/image31.png)

## **Task 5:** **Install Dev Containers extension**

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

       ![](./media/image32.png)

2.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    +++https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers+++
    then press the **Enter** button.

      ![](./media/image33.png)

3.  On Dev Containers page, select on Install button.

     ![](./media/image34.png)

4.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

      ![](./media/image35.png)

5.  Open the Visual Studio Code.

     ![](./media/image36.png)

      ![](./media/image37.png)

## Exercise 2: Deploy the application and test it from the browser

## Task 1: Open development environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    +++https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/rag-postgres-openai-python+++ then press the **Enter** button.

      ![](./media/image38.png)

2.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

      ![](./media/image39.png)

3.  In case, **Allow an extension to open this URI?** dialog box
    appears, then click on the **Open** button.

     ![](./media/image40.png)

4.  In case, **Cloning a repository in a Dev Container may execute
    arbitrary code** dialog box appears, then click on the **Got it**
    button.

     ![](./media/image41.png)

5.  To Staring Dev container will take 13-15 min

       ![](./media/image42.png)

       ![](./media/image43.png)

6.  After cloning the repo press any key

     ![](./media/image44.png)

## Task 2: Deploy chat app to Azure

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

     ![](./media/image45.png)

2.  Sign in to Azure with the Azure Developer CLI. Run the following
    command on the Terminal
    ```
    azd auth login
    ```
      ![](./media/image46.png)

3.  Default browser opens to sign in. Sign in with your Azure
    subscription account.

     ![](./media/image47.png)
     ![](./media/image48.png)

4.  Close the browser

      ![](./media/image49.png)

5.  To create an environment for Azure resources, run the following
    Azure Developer CLI command.
    ```
    azd env new
    ```
      ![](./media/image50.png)

6.  prompted to enter an environment name, enter the **ragsqlXX**(XX can
    be a unique number, you can add more digits after XX to make the
    name unique)

  **Note:** When creating an environment, ensure that the name consists of
  lowercase letters.
     ![](./media/image51.png)

7.  Run the following Azure Developer CLI command to provision the Azure
    resources and deploy the source code.

     +++azd up+++

       ![](./media/image52.png)

8.  When prompted, select a **subscription** to create the resources and
    select the region closest to your location; in this lab, we have
    chosen the East US2 region.
      ![](./media/image53.png)

      ![](./media/image54.png)

9.  When prompted, **enter a value for the ‘openAILocation’
    infrastructure parameter** select the region closest to your
    location; in this lab, we have chosen the **North Central US**
    region
     ![](./media/image55.png)

     ![](./media/image56.png)
     ![](./media/image57.png)

10. Deployment will take around 19-20 min

     ![](./media/image58.png)

11. Deployment completed and front end hosted successfully. Copy the URL
    and paste it into a browser and save URL in notepad

URL look likes-

https://ragpsql-3vlvcq6uzuk-ca.wonderfulcliff-01f39f01.eastus2.azurecontainerapps.io/
    ![](./media/image59.png)
    ![](./media/image60.png)

## Task 3: Verify deployed resources in the Azure portal

1.  Open a browser go to !!https://portal.azure.com!! and sign in with
    your Azure subscription account.

2.  On the Home page, click on **Resource Groups**.

     ![](./media/image61.png)

3.  Click on your resource group name

      ![](./media/image62.png)

4.  Make sure the below resource got deployed successfully

      - Container App
      
      - Application Insights
      
      - Container Apps Environment
      
      - Log Analytics workspace
      
      - Azure OpenAI
      
      - Azure Database for PostgreSQL flexible server
      
      - Container registry
      ![](./media/image63.png)

5.  On the resource group and click on **Azure OpenAI** resource name.

      ![](./media/image64.png)

6.  On the **Azure OpenAI** window, click on **Overview** in the left
    navigation menu, then under the **Get Started** tab, click on the
    **Go to Azure OpenAI Studio** button to open **Azure OpenAI Studio**
    in a new browser.

      ![](./media/image65.png)

7.  Make sure **gpt-35-turbo**, **text-embedding-ada-002** should be
    deployed successfully

      ![](./media/image66.png)

## Task 4: Use chat app to get answers from files

1.  Now open the URL (**(**The URL that you have saved in your notepad
    in the **Exercise 2> Task 2>Step 11)** it into a browser.

2.  In the **RAG on database |OpenAI+PoastgreSQL** web app page, **click
    on Best shoe for hiking?** button and observe the output

      ![](./media/image67.png)

      ![](./media/image68.png)

       ![](./media/image1.png)

3.  Click on the **clear chat.**

      ![](./media/image69.png)

4.  In the **RAG on database |OpenAI+PoastgreSQL** web app page, click
    on **Climbing gear cheaper than $30** button and observe the output

     ![](./media/image70.png)

     ![](./media/image71.png)

5.  Click on the **clear chat.**

     ![](./media/image69.png)

6.  In the **RAG on database |OpenAI+PoastgreSQL** web app page, click
    on **Waterproof camping gear?** button and observe the output

     ![](./media/image72.png)

     ![](./media/image73.png)

## Task 5: Delete the Resources

1.  To delete Resource group , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

      ![](./media/image74.png)

2.  Click on the sample web app resource group.

      ![](./media/image75.png)

3.  In the resource group home page , select **Delete resource group**
    button.

     ![](./media/image76.png)

4.  On the Delete a resource group tab, enter the resource group and
    click on the **Delete** button.

     ![](./media/image77.png)

Summary:

This use case walks users through deploying a custom chat application
with PostgreSQL and OpenAI on Azure, focusing on cloud-based application
deployment and management.. In this lab, you’ve set up the development
environment, installed necessary tools like Azure CLI and Node.js,
configured Azure resources using Azure Developer CLI, and deployed the
application to Azure Container Apps. In this lab, you’ve gained
proficiency in managing Azure resources, integrating OpenAI for advanced
chat functionalities, and ensuring proper deployment and verification
through Azure Portal. You’ve acquired hands-on experience in deploying
scalable, cloud-native applications with integrated AI capabilities on
Microsoft Azure.
