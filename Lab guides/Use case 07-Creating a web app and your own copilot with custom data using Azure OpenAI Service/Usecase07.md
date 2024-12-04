  # Use case 7- Creating a webapp and power virtual agent bot with custom data using Azure OpenAI Service

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

# Exercise 1- Create an Azure Storage Account and Azure cognitive Search by using the portal

## Task 1: Create Azure OpenAI resource

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:+++https://portal.azure.com/+++, then press
    the **Enter** button.

      ![](./media/image1.png)

2.  In the **Microsoft Azure** window, use the **User Credentials** to
    login to Azure.

     ![](./media/image2.png)

3.  Then, enter the password and click on the **Sign in** button . 

    ![](./media/image3.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

      ![](./media/image4.png)
5.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

     ![](./media/image5.png)

6.  Navigate and click on **+ Create a resource**.

      ![](./media/image6.png)

7.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

     ![](./media/image7.png)

8.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

    ![](./media/image8.png)

9.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

      |   |   |
      |---|----|
      |Subscription	|Select the assigned subscription|
      |Resource group|	Click on Create new> enter +++AOAI-RGXXX+++(XXX can be a unique number)|
      |Region	|Select East US 2|
      |Name	|+++Azure-openai-testXX+++ (XX can be a unique number, you can add more digits after XX to make the name unique)|
      |Pricing tier	|Select Standard S0|


      ![](./media/image9.png)
      ![](./media/image10.png)

10. In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

      ![](./media/image11.png)

11. In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

      ![](./media/image12.png)

12. In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

      ![](./media/image13.png)

13. Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

14. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

      ![](./media/image14.png)

## Task 2: Cognitive Services Usages Reader for the Azure OpenAI resource

1.  Type in **Subscriptions** in the search bar and select
    **Subscriptions**.

      ![](./media/image15.png)
2.  Click on your assigned **subscription**.

      ![](./media/image16.png)

3.  From the left menu, click on the **Access control(IAM).**

      ![](./media/image17.png)

4.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

      ![](./media/image18.png)

5.  Type the **Cognitive Services Usages Reader** in the search box and
    select it. Click **Next**

      ![](./media/image19.png)

6.  In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

      ![](./media/image20.png)

7.  On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

      ![](./media/image21.png)

8.  In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

      ![](./media/image22.png)
      ![](./media/image23.png)

9.  You will see a notification – added as Cognitive Services Usage
    Reader for Azure Pass-Sponsorship.

      ![](./media/image24.png)

10. In Azure subscription page from the left menu, click on the **Access
    control(IAM).**

      ![](./media/image17.png)

11. On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

      ![](./media/image18.png)

12. Type the !!Cognitive Services Contributor!! in the search box and select it. Click **Next**

      ![](./media/image25.png)

13. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

      ![](./media/image26.png)

14. On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

      ![](./media/image21.png)

15. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

      ![](./media/image27.png)
      
      ![](./media/image28.png)

16. You will see a notification – added as Cognitive Services Usage
    Reader for Azure Pass-Sponsorship.

      ![](./media/image29.png)

17. Go back to **Azure portal** home page, type in **Azure OpenAI** in
    the search bar and select **Azure OpenAI** created in **Lab 1**

      ![](./media/image30.png)

18. Click on your **Azure OpenAI** service.

      ![](./media/image31.png)

19. From the left menu, click on the **Access control(IAM).**

      ![](./media/image32.png)

20. On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

      ![](./media/image33.png)

21. Type the +++Cognitive Services Contributor+++ in the search box and select it. Click **Next**

      ![](./media/image34.png))

22. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

      ![](./media/image35.png)
23. On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

      ![](./media/image21.png)

24. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

      ![](./media/image27.png)
      ![](./media/image28.png)

25. You will see a notification – added as Cognitive Services Usage
    Reader for Azure Pass-Sponsorship.

      ![](./media/image35.png)

## Task 3: Create an Azure Storage Account by using the portal

1.  Sign in to the +++https://portal.azure.com/+++

2.  Click on the **Portal Menu**, then select **+ Create a resource**

       ![](./media/image36.png)

3.  In the **Create a resource** window search box, type **Storage
    account** and then click on the **storage account**.

       ![](./media/image37.png)

4.  In the **Marketplace** page, click on the **Storage account**
    section.

       ![](./media/image38.png)

5.  In the **Storage account** window, click on the **Create** button.

       ![](./media/image39.png)

6.  On **Create a storage account** window, under the **Basics** tab,
    enter the below details to create a storage account and then click
    on **Review**

      |   |   |
      |---|----|
      |Subscription	|Select your Azure OpenAI subscription|
      |Resource group|	Select your Resource group(that you have created in Task 1)|
      |Storage account name|	+++azureopenaistorageXX+++(XX can be a unique number) (here, we entered azureopenaistorage39)|
      |Region	|Select the appropriate region for your storage account . In this lab East US is taken|
      |Performance|	Standard: Recommended for most scenarios (general-purpose v2 account)|
      |Redundancy	|Locally-redundant storage (LRS)|

      ![](./media/image40.png)

      ![](./media/image41.png)

7.  On the **Review** tab, click on the **Create** button.

      ![](./media/image42.png)

8.  This new Azure Storage account is now set up to host data for an
    Azure Data Lake. Click on the **Go to resource** button.

      ![](./media/image43.png)

9.  After the account has been deployed, you will find options related
    to Azure Data Lake in the Overview page. In the left-side navigation
    pane, navigate to **Data storage** section, then click on
    **Containers**.

      ![](./media/image44.png)

10. On **azureopenaistorageXX | Containers** page, click on
    **+Container.**

      ![](./media/image45.png)

11. On the New container pane that appear on the right side, enter the
    container **Name** as **source** and click on **Create** button.

      ![](./media/image46.png)

12. On **azureopenaistorageXX | Containers** page, select **source**
    container**.**

      ![](./media/image47.png)

13. On **source** container page, click on **Upload** button.

       ![](./media/image48.png)

14. In the **Upload blob** pane, click on **Browse for file**, navigate
    to **C:\Labfiles** location and select **TF-AzureOpenAI.pdf**, then
    click on the **Open** button.

       ![](./media/image49.png)
       
        ![](./media/image50.png)

15. In **Upload blob** pane, click on the **Upload** button.

      ![](./media/image51.png)

16. You will see a notification – **Successfully uploaded blob** when
    the uploaded is succeeded.

      ![](./media/image52.png)
     
      ![](./media/image53.png)

## Task 4: Create an Azure Cognitive Search service in the portal

1.  On the **azureopenaistorageXX | Containers** page, click on **Home**
    to go back to Azure portal home page.

      ![](./media/image54.png)

2.  In Azure portal home page, click on **+ Create Resource**.

      ![](./media/image55.png)

3.  In the **Create a resource** page search bar, type **Azure AI
    Search** and click on the appeared **azure ai search**.

      ![](./media/image56.png)

4.  Click on **azure ai search** section.

      ![](./media/image57.png)

5.  In the **Azure AI Search** page, click on the **Create** button.

        ![](./media/image58.png)

6.  On the **Create a search service** page, provide the following
    information and click on **Review+create** button.

      |Field|	Description|
      |----|----|
      |Subscription|	Select your Azure OpenAI subscription|
      |Resource group|	Select your Resource group(that you have created in Task 1)|
      |Region|	EastUS|
      |Name	|+++mysearchserviceXX+++ (XXcan be unique number)|
      |Pricing Tier|	Click on change Price Tire>select Basic|


      ![](./media/image59.png)
      
      ![](./media/image60.png)
      
      ![](./media/image61.png)

7.  Once the Validation is passed, click on the **Create** button.

      ![](./media/image62.png)

       ![](./media/image63.png)
8.  After the deployment is completed, click on the **Go to resource**
    button.

      ![](./media/image64.png)

9.  In the **mysearchserviceXX** Overview page. In the left-side
    navigation pane, under **Settings** section, select **Semantic
    ranker**.

      ![](./media/image65.png)

10. On the **Semantic ranker** tab,  select **Standard** tile and
    click on the **Select plan.**

      ![](./media/image66.png)

11. You will see a notification -**Successfully updated semantic ranker
    to free plan**

# Exercise-2: Add your data using Azure OpenAI Studio

## Task 1: Deploy gpt-35-turbo and embedded models in Azure AI Studio

1.  Switch back to Azure portal and search for Azure OpenAI and select
    it.

    ![](./media/image67.png)

2.  Select your **Azure OpenAI** service .

      ![](./media/image68.png)

      ![](./media/image69.png)

3.  On the **AzureOpenAI** window, click on **Overview** in the left
    navigation menu, then under the **Get Started** tab, click on the
    **Go to Azure OpenAI Studio** button to open **Azure OpenAI Studio**
    in a new browser

       ![](./media/image70.png)

4.  On the **Azure AI Foundry** |**Azure OpenAI Studio** homepage select
    **Deployment** from the left navigation menu . 

      ![](./media/image71.png)

5.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

      ![](./media/image72.png)

6.  In the **Select a model** dialog box, navigate and carefully select
    **gpt-35-turbo**, then click on **Confirm** button.

        ![](./media/image73.png)

7.  In the **Deploy model dialog** box, enter the following details and
    click on the **Create** button.

      - Select Model: **gpt-35-turbo**
      
      - Deployment Name: enter **gpt-35-turbo**
      
      - Select select the **Standard** as **Deployment type**

        ![](./media/image74.png)
 
      ![](./media/image75.png)

8.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

        ![](./media/image76.png)

9.  In the **Select a model** dialog box, navigate and carefully select
    **text-embedding-ada-002** then click on **Confirm** button.

     ![](./media/image77.png)

10. In the **Deploy model** dialog box, under **Deployment name** enter
    +++text-embedding-ada-002+++, select the **Standard** as
    **Deployment type** and Click on the **Deploy** button.

      ![](./media/image78.png)

       ![](./media/image79.png)
11. In **Azure AI Foundry |Azure OpenAI Service** Home page, under
    **Playgrounds** section, click on the **Chat**.

      ![](./media/image80.png)

12. In the **Chat playground** pane, drop down **Add your data** and
    select **+Add a data source**

      ![](./media/image81.png)

## Task 2: Add your data using Azure OpenAI Studio

1.  In the **Select or add data source** page, click on the dropdown
    under **Select or add data source**, then navigate and click on
    **Azure Blob Storage**.

2.  In the **Select or add data source** page, under **Select or add
    data source** enter the following details and select **Next.**

      |    |   |
      |----|----|
      |Subscription	|Select your Azure OpenAI subscription|
      |Select Azure Blob storage resource	|Select your Azure Blob storage that you have created in Exercise 1 Task 2(azureopenaistorageXX)|
      |Select storage container|	source|
      |Select Azure AI Search resource|Select your Azure AI Search that you have created in Exercise 1 Task 3(mysearchserviceXX)|
      |Enter the index name|+++azure-index+++| 
      |Indexer schedule |	Once|

3.  Select the check box – **Add vector search to this search
    resource**.

4.  Select an embedding model as **text-embedding-ada-002**, then click
    on the **Next** button.

      ![](./media/image82.png)
      
      ***Note**: In case, you encounter an error – **Can‘t manage CORS on this
      resource. Please select another storage resource**, then syn your VM
      time, as mentioned in Task \#1.*

5.  In the **Add data** page, on the **Data management** tab drop down
    the Search type and select **Hybrid+semantic.**

6.  Select the **chunk size** as **1024(default)** Then, click on
    **Next.**

      ![](./media/image83.png)

7.  In the **Data connection** pane, select **API key** and click on
    **Next** button.

      ![](./media/image84.png)

8.  In **Review and Finish** pane, review the details that you’ve
    entered, and click on **Save and close** button . 

      ![](./media/image85.png)

9.  The data will be added in your Chat Playground. This will take
    approximately 4-5 minutes.

       ![](./media/image86.png)
      
      ![](./media/image87.png)

## Task 3: Explore text completion in the Chat Playground

1.  In the **Chat session** section, enter the following prompt in the
    **User message** text box and click on the **Send** icon

      CodeCopy
      ```
      What is Azure OpenAI Service?
      ```
      ![](./media/image88.png)
      
      ![](./media/image89.png)

2.  In the **Chat session** section, select the references link and
    observe the details of search document on right side of the page.

      ![](./media/image90.png)
      
      ![](./media/image91.png)

# Exercise 3: Deploy a web app with custom data

## Task 1: Deploy a web app

1.  In In **Azure AI Foundry |Azure OpenAI Service** Home page **,Chat
    playground pane**, drop down **Deploy**, then navigate and click on
    **as web app**.

     ![](./media/image92.png)

2.  On **Deploy to a web app** window, select **Create a new web app**
    radio button and enter the following details:

      |    |   |
      |---|----|
      |Name |	+++AOAI-webappXXX+++(XXX can be a unique number) (here, we entered AOAI-webapp129)|
      |Subscription|	Select the assigned subscription|
      |Resource Group	|Select the resource group created in Lab 1|
      |Location|	East US|
      |Pricing plan|	Basic(B1)|

3.  Select the check box of **Enable chat history in the web app**

4.  Click on **Deploy** button.

      Note : Deployment takes 5-10 minutes

      ![](./media/image93.png)

5.  To check the deployment status, click on **Deployments** and
    select **App deployment**.

     ![](./media/image94.png)

     ![](./media/image95.png)

6.  Wait for the deployment to complete. The deployment will take around
    **10-15** minutes.

      ![](./media/image96.png)

7.  Click on the web application.

      ![](./media/image97.png)

8.  Wait for 10 minutes, so that authentication configuration can be
    successfully applied on the app.

9.  After 10 minutes, click on the **Refresh** button.

    ![](./media/image98.png)

10. On **Permissions requested** dialog box, click on the **Accept**
    button

    ![](./media/image99.png)

11. Now, web app will open in a new browser.

     ![](./media/image100.png)

12. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

    **CodeCopy**
    ```
     How do I get access to Azure OpenAI? 
    ```
      ![](./media/image101.png)

      ![](./media/image102.png)
      ![](./media/image103.png)

5.  Similarly, paste the following text in the text box and click on the
    **Send** icon.

      **CodeCopy**
      
      **+++What is the expiry date of GPT-35-Turbo version 0301 and GPT-4 version
      0314?+++**
      
      ![](./media/image104.png)
      
      ![](./media/image105.png)

6.  Refresh the webapp page and click on the **Show chat history**.

      ![](./media/image106.png)
      
      ![](./media/image107.png)

7.  Under the chat history click on **Accessing Azure OpenAI**.

      ![](./media/image108.png)
      
      ![](./media/image109.png)

# Exercise 4: Create a Copilot app with custom data

## Task 1: Create a chatbot with custom data

1.  In **Azure AI Foundry |Azure AI Studio** **Chat playground,** in the
    Add your data select the Remove data source.

      ![](./media/image110.png)

2.  In the **Chat playground** pane, drop down **Add your data** and
    select **+Add a data source**

     ![](./media/image81.png)

3.  In the **Add data** page, under **Select or add data source** enter
    the following details and select **Next.**

      |   |   |
      |-----|----|
      |Subscription	|Select your Azure OpenAI subscription|
      |Select Azure Blob storage resource|	Select your Azure Blob storage that you have created in Exercise 1 Task 2(azureopenaistorageXX)|
      |Select storage container|	source|
      |Select Azure AI Search resource|Select your Azure AI Search that you have created in Exercise 1 Task 3(mysearchserviceXX)|
      |Enter the index name	|+++copilot-index+++|
      |Indexer schedule|Once|

      ![](./media/image111.png)

      ***Note**: In case, you encounter an error – **Can‘t manage CORS on this
      resource. Please select another storage resource**, then syn your VM
      time, as mentioned in Task \#1.*

4.  In the **Add data** page, on the **Data management** tab drop down
    the Search type and select **Keyword,** select the chunk size as
    **1024(default)** Then, click on **Next.**

      ![](./media/image112.png)

5.  In the **Data connection** pane, select **API key** and click on
    **Next** button.

      ![](./media/image84.png)

6.  In **Review and Finish** pane, review the details that you’ve
    entered, and click on **Save and close** button.

      ![](./media/image113.png)
      
      ![](./media/image114.png)
      ![](./media/image115.png)

7.  The data will be added in your Chat Playground. This will take
    approximately 4-5 minutes.

## Task 2: Create a copilot with custom data from Azure OpenAI

1.  Login to !!https://copilotstudio.microsoft.com/!! using your
    Azure login credentials.

      ![](./media/image116.png)

2.  Once logged in, in the Welcome to Microsoft Copilot Studio page,
    select your Country and click on **Start free trial**.

      ![](./media/image117.png)

3.  The Copilot Home page opens.

      ![](./media/image118.png)

4.  Select Copilots from the left pane. And then click on **+ New
    copilot**.

      ![](./media/image119.png)

5.  Select **Skip to configure**.

      ![](./media/image120.png)

6.  On the Create a copilot page, enter the **name** as
    +++CopilotforAOAI+++ and click on **Create**.

      ![](./media/image121.png)

7.  Click on **Topics -\> System -\> Conversational boosting**.

      ![](./media/image122.png)

8.  Click on **Edit** under **Data sources** of the **Create generative
    answers** node. Select **Classic data** in the **Properties** pane
    that opens up.
      ![](./media/image123.png)

9.  Under **Azure OpenAI Services on your data**, click on **+ Add
    connection** and then select **Azure OpenAI**.

      ![](./media/image124.png)

10. This adds the Azure OpenAI service connection and opens up the
    connection properties pane.

11. In the **Connection Properties** pane, under **General -\>
    Configuration**, fill in the below details

        Deployment – +++gpt-35-turbo+++
        
        Api version – +++0301+++

      ![](./media/image125.png)

12. Under the **Model data** tab, click on **+ Add** under Data sources
    and then add the below details.

      Index name - +++copilot-index+++
      
      Content data – +++content+++

      ![](./media/image126.png)

13. Click on **Save**.

      ![](./media/image127.png)

## Task 3: Test your copilot

1.  Click on **Test** to open the Test your Copilot pane.

      ![](./media/image128.png)

2.  Type in !!What is Azure OpenAI?!! and click **Send**.

      ![](./media/image129.png)

3.  You will receive the response from the data uploaded in **Azure
    OpenAI resource**. Also, observe that the **Surfaced with Azure
    OpenAI** message below the reply.

      ![](./media/image130.png)

## Task 4: Delete resources

1.  To delete the storage account, navigate to Azure portal home page,
    type **Resource groups** in the Azure portal search bar, navigate
    and click on **Resource groups** under **Services**.

      ![](./media/image131.png)

2.  Click on the assigned resource group.

      ![](./media/image132.png)

3.  Carefully select storage account, Azure Cognitive Search, Azure web
    app, CosmosDB that you’ve created.

    **Note**: Don’t select Azure OpenAI service.

     ![](./media/image133.png)

4.  In the Resource group page, navigate to the command bar and click on
    **Delete**.

    **Important Note**: Don’t click on **Delete resource group**. If you
    don’t see the **Delete** option in the command bar, then click on the
    horizontal ellipsis.

      ![](./media/image134.png)

5.  In the **Delete Resources** pane that appears on the right side,
    enter the **delete** and click on **Delete** button.

      ![](./media/image135.png)

6.  On **Delete confirmation** dialog box, click on D**elete** button.

      ![](./media/image136.png)

7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 4 selected items.**

      ![](./media/image137.png)
 
  **Summary**
 
 You've created a storage account, container, and Azure cognitive
 service in Azure portal, then you've deployed gpt-3-turbo model in
 Azure AI Studio. You’ve added data in Chat Playground and tested the
 Assistant setup by sending queries in a chat session. Then, you've
 launched a new app and started conversation with the chatbot. You've
 deleted the gpt-3-turbo model, Azure storage account, cognitive search
 service, and the new web app to effectively and efficiently manage the
 Azure OpenAI resources.

