# Use case 10- Creating a webapp and power virtual agent bot with custom data using Azure OpenAI Service

**Introduction:**

Azure OpenAI on your data works with OpenAI's powerful ChatGPT
(gpt-35-turbo) and GPT-4 language models, enabling them to provide
responses based on your data. You can access Azure OpenAI on your data
using a REST API or the web-based interface in the Azure OpenAI
Studio to create a solution that connects to your data to enable an
enhanced chat experience.

One of the key features of Azure OpenAI on your data is its ability to
retrieve and utilize data in a way that enhances the model's output.
Azure OpenAI on your data together with Azure Cognitive Search
determines what data to retrieve from the designated data source based
on the user input and provided conversation history. This data is then
augmented and resubmitted as a prompt to the OpenAI model, with
retrieved information being appended to the original prompt. Although,
retrieved data is being appended to the prompt, the resulting input is
still processed by the model like any other prompt. Once the data has
been retrieved and the prompt has been submitted to the model, the model
uses this information to provide a completion.

**Objectives**

- To create a storage account, container, and Azure cognitive search
  service in the Azure portal.

- To deploy gpt-3-turbo and Embedded model in Azure AI Studio and to add
  data in Chat Playground.

- To test Assistant setup in Chat playground by sending queries in chat
  session.

- To launch a copilot and start a conversation with the bot

- To launch a new app and start a conversation with the copilot app.

- To delete gpt-3-turbo and embedded model, Azure storage account,
  cognitive search service, and the new web app.

## Exercise 1- Create an Azure Storage Account and Azure cognitive Search by using the portal

### Task 1: Create Azure OpenAI resource

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:+++<https://portal.azure.com/+++>, then press
    the **Enter** button.

![](./media/image1.png)

2.  In the **Microsoft Azure** window, use the **User Credentials** to
    login to Azure.

![](./media/image2.png)

3.  Then, enter the password and click on the **Sign in** button .

![](./media/image3.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

5.  From the Azure portal home page, click on **Azure portal
    menu** represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

![](./media/image4.png)

6.  Navigate and click on **+ Create a resource**.

![](./media/image5.png)

7.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press
    the **Enter** button.

![](./media/image6.png)

8.  In the **Marketplace** page, navigate to the **Azure
    OpenAI** section, click on the Create button dropdown, then
    select **Azure OpenAI** as shown in the image. (In case, you’ve
    already clicked on the **Azure** **OpenAI** tile, then click on
    the **Create** button on the **Azure OpenAI page**).

    ![](./media/image7.png)

9.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

      |    |   |
      |----|----|
      |Subscription	|Select the assigned subscription|
      |Resource group|	Select the assigned Resource group|
      |Region|	Select East US 2|
      |Name|	+++Azure-openai-testXXXXX+++ (XXXXX can be Lab instant ID)|
      |Pricing tier	|Select Standard S0|


     ![](./media/image8.png)

10. In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

      ![](./media/image9.png)

11. In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

      ![](./media/image10.png)

12. In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

      ![](./media/image11.png)

13. Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

14. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

      ![](./media/image12.png)

### Task 2: Create an Azure Storage Account by using the portal

1.  Sign in to the +++https://portal.azure.com/+++

2.  Click on the **Portal Menu**, then select **+ Create a resource**

     ![](./media/image13.png)

3.  In the **Create a resource** window search box, type **Storage
    account** and then click on the **storage account**.

    ![](./media/image14.png)

4.  In the **Marketplace** page, click on the **Storage
    account** section.

    ![](./media/image15.png)

5.  In the **Storage account** window, click on the **Create** button.

      ![](./media/image16.png)

6.  On **Create a storage account** window, under the **Basics** tab,
    enter the below details to create a storage account and then click
    on **Review**

      | |   |
      |---|---|
      |Subscription|	Select your Azure OpenAI subscription|
      Resource group|	Select your Resource group|
      |Storage account name|	+++azureopenaistorageXXXX+++( XXXX can be last 4 digits of Lab instant ID)|
      |Region|	Select the appropriate region for your storage account . In this lab East US is take|n
      |Performance|	Standard: Recommended for most scenarios (general-purpose v2 account)|
      |Redundancy	|Locally-redundant storage (LRS)|


      ![](./media/image17.png)

7.  On the **Review** tab, click on the **Create** button.

     ![](./media/image18.png)

8.  This new Azure Storage account is now set up to host data for an
    Azure Data Lake. Click on the **Go to resource** button.

     ![](./media/image19.png)

9.  After the account has been deployed, you will find options related
    to Azure Data Lake in the Overview page. In the left-side navigation
    pane, navigate to **Data storage** section, then click
    on **Containers**.

     ![](./media/image20.png)

10. On **azureopenaistorageXX | Containers** page, click
    on **+Container.**

     ![](./media/image21.png)

11. On the New container pane that appear on the right side, enter the
    container **Name** as **+++source+++** and click
    on **Create** button.

     ![](./media/image22.png)

12. On **azureopenaistorageXX | Containers** page,
    select **source** container\*\*.\*\*

      ![](./media/image23.png)

13. On **source** container page, click on **Upload** button.

      ![](./media/image24.png)

14. In the **Upload blob** pane, click on **Browse for file**, navigate
    to **C:\Labfiles** location and select **TF-AzureOpenAI.pdf**, then
    click on the **Open** button.

     ![](./media/image25.png)

     ![](./media/image50.png)

15. In **Upload blob** pane, click on the **Upload** button.

    ![](./media/image26.png)

16. You will see a notification – **Successfully uploaded blob** when
    the uploaded is succeeded.

      ![](./media/image27.png)
      
      ![](./media/image28.png)

### Task 3: Create an AzureAI Search service in the portal

1.  On the **azureopenaistorageXX | Containers** page, click
    on **Home** to go back to Azure portal home page.

      ![](./media/image29.png)

2.  In Azure portal home page, click on **+ Create Resource**.

      ![](./media/image30.png)

3.  In the **Create a resource** page search bar, type **Azure AI
    Search** and click on the appeared **azure ai search**.

      ![](./media/image31.png)

4.  Click on **azure ai search** section.

    ![](./media/image32.png)

5.  In the **Azure AI Search** page, click on the **Create** button.

     ![](./media/image58.png)

6.  On the **Create a search service** page, provide the following
    information and click on **Review+create** button.

    |Field	|Description|
    |----|----|
    |Subscription|	Select your Azure OpenAI subscription|
    |Resource group|	Select your Resource group|
    |Region|EastUS|
    |Name|	+++mysearchserviceXXXX+++ ( XXXX can be last 4 digits of Lab instant ID)|
    |Pricing Tier|	Click on change Price Tire>select Basic|


     ![](./media/image33.png)
   
     ![](./media/image34.png)

8.  Once the Validation is passed, click on the **Create** button.

    ![](./media/image35.png)

9.  After the deployment is completed, click on the **Go to
    resource** button.

    ![](./media/image36.png)

10. In the **mysearchserviceXX** Overview page. In the left-side
    navigation pane, under **Settings** section, select **Semantic
    ranker**.

    ![](./media/image37.png)

11. On the **Semantic ranker** tab, select **Standard** tile and click
    on the **Select plan.**

      ![](./media/image38.png)


## Exercise-2: Add your data using Azure OpenAI Studio

### Task 1: Deploy gpt-35-turbo and embedded models in Azure AI Studio

1.  Switch back to Azure portal and search for Azure OpenAI and select
    it.

     ![](./media/image39.png)

2.  Select your **Azure OpenAI** service .

      ![](./media/image40.png)
      
      ![](./media/image41.png)

3.  On the **AzureOpenAI** window, click on **Overview** in the left
    navigation menu, then click on the **Explore Azure AI Foundry
    portal** button to **Azure AI Foundry portal**  in a new browser

      ![](./media/image42.png)

4.  On the **Azure AI Foundry** |**Azure OpenAI Studio** homepage
    select **Deployment** from the left navigation menu .

      ![](./media/image43.png)

5.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

      ![](./media/image44.png)

6.  In the **Select a model** dialog box, navigate and carefully
    select **gpt-4**, then click on **Confirm** button.

      ![](./media/image45.png)

7.  In the **Deploy model dialog** box, enter the following details and
    click on the **Create** button.

    - Select Model: **gpt-4**

    - Deployment Name: enter **gpt-35-turbo**

    - Select select the **Standard** as **Deployment type**

      ![](./media/image46.png)
     
      ![](./media/image47.png)
     
      ![](./media/image48.png)

8.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

      ![](./media/image49.png)

9.  In the **Select a model** dialog box, navigate and carefully
    select **text-embedding-ada-002** then click on **Confirm** button.

     ![](./media/image50.png)

10. In the **Deploy model** dialog box, under **Deployment name** enter **+++text-embedding-ada-002+++**, select the **Standard** as **Deployment type** and Click on the **Deploy** button.

     ![](./media/image51.png)
  
     ![](./media/image52.png)

11. In **Azure AI Foundry |Azure OpenAI Service** Home page,
    under **Playgrounds** section, click on the **Chat**.

     ![](./media/image53.png)

12. In the **Chat playground** pane, drop down **Add your data** and
    select **+Add a data source**

     ![](./media/image54.png)

### Task 2: Add your data using Azure OpenAI Studio

1.  In the **Select or add data source** page, click on the dropdown
    under **Select or add data source**, then navigate and click
    on **Azure Blob Storage**.

2.  In the **Select or add data source** page, under **Select or add
    data source** enter the following details and select **Next.**

      |    |   |
      |----|---|
      |Subscription	|Select your Azure OpenAI subscription|
      |Select Azure Blob storage resource|	Select your Azure Blob storage that you have created in Exercise 1 Task 2|
      |Select storage container|	source|
      |Select Azure AI Search resource|	Select your Azure AI Search that you have created in Exercise 1 Task 3|
      |Enter the index name	|+++azure-index+++|
      |Indexer schedule|	Once|


3.  Select the check box – **Add vector search to this search
    resource**.

4.  Select an embedding model as **text-embedding-ada-002**, then click
    on the **Next** button.

      ![](./media/image55.png)

***Note**: In case, you encounter an error – **Can‘t manage CORS on this
resource. Please select another storage resource**, then syn your VM
time, as mentioned in Task \#1.*

5.  In the **Add data** page, on the **Data management** tab drop down
    the Search type and select **Hybrid+semantic.**

6.  Select the **chunk size** as **1024(default)** Then, click
    on **Next.**

    ![](./media/image56.png)

7.  In the **Data connection** pane, select **API key** and click
    on **Next** button.

      ![](./media/image57.png)

8.  In **Review and Finish** pane, review the details that you’ve
    entered, and click on **Save and close** button .

      ![](./media/image58.png)

9.  The data will be added in your Chat Playground. This will take
    approximately 4-5 minutes.

      ![](./media/image59.png)
      
      ![](./media/image60.png)

### Task 3: Explore text completion in the Chat Playground

1.  In the **Chat session** section, enter the following prompt in
    the **User message** text box and click on the **Send** icon
  
      +++What is Azure OpenAI Service?+++

      ![](./media/image61.png)
      
      ![](./media/image62.png)

2.  In the **Chat session** section, select the references link and
    observe the details of search document on right side of the page.

      ![](./media/image63.png)
      
      ![](./media/image64.png)

## Exercise 3: Deploy a web app with custom data

### Task 1: Deploy a web app

1.  In In **Azure AI Foundry |Azure OpenAI Service** Home page **,Chat
    playground pane**, drop down **Deploy**, then navigate and click
    on **as web app**.

      ![](./media/image65.png)

2.  On **Deploy to a web app** window, select **Create a new web
    app** radio button and enter the following details:

      |        |      |
      |------|-----|
      |Name|	+++AOAI-webappXXXXXX+++( XXXXX can be Lab instant ID|
      |Subscription|	Select the assigned subscription|
      |Resource Group|	Select the resource group |
      |Location|	East US|
      |Pricing plan|	Basic(B1)|


3.  Select the check box of **Enable chat history in the web app**

4.  Click on **Deploy** button.

    Note : Deployment takes 5-10 minutes

     ![](./media/image66.png)
 
5.  To check the deployment status, click on **Deployments** and
    select **App deployment**.

    ![](./media/image67.png)

    ![](./media/image68.png)

6.  Wait for the deployment to complete. The deployment will take
    around **10-15** minutes.

    ![](./media/image69.png)

7.  Click on the web application.

      ![](./media/image70.png)

8.  Wait for 10 minutes, so that authentication configuration can be
    successfully applied on the app.

9.  After 10 minutes, click on the **Refresh** button.

10. On **Permissions requested** dialog box, click on
    the **Accept** button

      ![](./media/image71.png)

11. Now, web app will open in a new browser.

      ![](./media/image72.png)

12. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

    **CodeCopy**
    
    How do I get access to Azure OpenAI?

      ![](./media/image73.png)
      
      ![](./media/image74.png) 
      ![](./media/image75.png)

13. Similarly, paste the following text in the text box and click on
    the **Send** icon.

    **CodeCopy**
    
    **+++What is the expiry date of GPT-35-Turbo version 0301 and GPT-4
    version 0314?+++**

    ![](./media/image76.png)
    
    ![](./media/image77.png)

14. Refresh the webapp page and click on the **Show chat history**.

      ![](./media/image78.png)
      
      ![](./media/image79.png)

15. Under the chat history click on **Accessing Azure OpenAI**.

      ![](./media/image80.png)
      
      ![](./media/image81.png)

## Exercise 4: Create a Copilot app with custom data

### Task 1: Create a chatbot with custom data

1.  In **Azure AI Foundry |Azure AI Studio** **Chat playground,** in the
    Add your data select the Remove data source.

      ![](./media/image82.png)

2.  In the **Chat playground** pane, drop down **Add your data** and
    select **+Add a data source**

      ![](./media/image54.png)

3.  In the **Add data** page, under **Select or add data source** enter
    the following details and select **Next.**

      |   |    |
      |----|----|
      |Subscription	|Select your Azure OpenAI subscription|
      |Select Azure Blob storage resource	|Select your Azure Blob storage that you have created in Exercise 1 Task 2|
      |Select storage container|	source|
      |Select Azure AI Search resource|	Select your Azure AI Search that you have created in Exercise 1 Task 3(mysearchserviceXX)|
      |Enter the index name	|+++copilot-index+++|
      |Indexer schedule	|Once|


     ![](./media/image83.png)
 
      ***Note**: In case, you encounter an error – **Can‘t manage CORS on
      this resource. Please select another storage resource**, then syn your
      VM time, as mentioned in Task \#1.*

4.  In the **Add data** page, on the **Data management** tab drop down
    the Search type and select **Keyword,** select the chunk size
    as **1024(default)** Then, click on **Next.**

      ![](./media/image84.png)

5.  In the **Data connection** pane, select **API key** and click
    on **Next** button.

      ![](./media/image57.png)

6.  In **Review and Finish** pane, review the details that you’ve
    entered, and click on **Save and close** button.

      ![](./media/image85.png)
      
      ![](./media/image86.png) 
      ![](./media/image87.png)

7.  The data will be added in your Chat Playground. This will take
    approximately 4-5 minutes.

### Task 2: Create a copilot with custom data from Azure OpenAI

1.  Login to +++https://copilotstudio.microsoft.com/+++ using your
    Azure login credentials.

2.  Once logged in, in the Welcome to Microsoft Copilot Studio page,
    select your Country and click on **Start free trial**.

    ![](./media/image88.png)

3.  The Copilot Home page opens.

   ![](./media/image89.png)

4.  Select **Agents** from the left pane. And then click on **+ New
    agent**.

    ![](./media/image90.png)

5.  Select **Skip to configure**.

      ![](./media/image91.png)

6.  On the Create a copilot page, enter the **name** as
    +++**CopilotforAOAI**+++ and click on **Create**.

      ![](./media/image92.png)

7.  Click on **Topics -\> System -\> Conversational boosting**.

     ![](./media/image93.png)

8.  Click on **Edit** under **Data sources** of the **Create generative
    answers** node. Select **Classic data** in the **Properties** pane
    that opens up. 

     ![](./media/image94.png)

9.  Under **Azure OpenAI Services on your data**, click on **Connection
    properties** 

     ![](./media/image95.png)

10. This adds the Azure OpenAI service connection and opens up the
    connection properties pane.

11. In the **Connection Properties** pane, under **General -\>
    Configuration**, fill in the below details

    Deployment – +++gpt-4+++
 
    Api version – Select latest version
 
     ![](./media/image96.png)

12. Under the **Model data** tab, click on **+ Add** under Data sources
    and then add the below details.

      Index name - +++copilot-index+++
      
      Content data – +++content+++

     ![](./media/image97.png)

13. Click on **Save**.

     ![](./media/image98.png)

**Task 3: Test your copilot**

1.  Click on **Test** to open the Test your Copilot pane.

      ![](./media/image99.png)

2.  Type in +++What is Azure OpenAI?+++ and click **Send**.

      ![](./media/image100.png)

3.  You will receive the response from the data uploaded in **Azure
    OpenAI resource**. Also, observe that the **Surfaced with Azure
    OpenAI** message below the reply.

     ![](./media/image101.png)

**Task 4: Delete resources**

1.  To delete the storage account, navigate to Azure portal home page,
    type **Resource groups** in the Azure portal search bar, navigate
    and click on **Resource groups** under **Services**.

      ![](./media/image102.png)

2.  Click on the assigned resource group.

      ![](./media/image103.png)

3.  Carefully select all resources that you’ve created.

      ![](./media/image104.png)

4.  In the Resource group page, navigate to the command bar and click
    on **Delete**.

    **Important Note**: Don’t click on **Delete resource group**. If you
    don’t see the **Delete** option in the command bar, then click on the
    horizontal ellipsis.

      ![](./media/image105.png)

5.  In the **Delete Resources** pane that appears on the right side,
    enter the **delete** and click on **Delete** button.

       ![](./media/image106.png)

6.  On **Delete confirmation** dialog box, click on D**elete** button.

      ![](./media/image107.png)
  
7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 4 selected items.**

**Summary**

You've created a storage account, container, and Azure cognitive service
in Azure portal, then you've deployed gpt-3-turbo model in Azure AI
Studio. You’ve added data in Chat Playground and tested the Assistant
setup by sending queries in a chat session. Then, you've launched a new
app and started conversation with the chatbot. You've deleted the
gpt-3-turbo model, Azure storage account, cognitive search service, and
the new web app to effectively and efficiently manage the Azure OpenAI
resources.
