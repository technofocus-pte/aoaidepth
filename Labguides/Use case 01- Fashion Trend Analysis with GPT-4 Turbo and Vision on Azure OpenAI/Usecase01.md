**Use Case 01- Developing Multimodal AI Applications for Image
Classification Using Azure OpenAI GPT-4o**

**Introduction**

This use case demonstrates how to utilize Azure OpenAI's GPT-4o
model for image classification by combining its multimodal capabilities
with a user-friendly web interface. It highlights the power of GPT-4o in
interpreting visual content and generating meaningful natural language
descriptions, making it ideal for applications in AI-driven image
understanding.

**Objective:**

- Showcase the integration of GPT-4o with Azure services for image
  classification.

- Enable users to upload images and receive intelligent, descriptive
  outputs from GPT-4o.

- Provide a working example of how to build multimodal AI applications
  using Python and Streamlit.

- Inspire developers to explore GPT-4o’s potential in real-world
  scenarios involving vision and language.

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

   ![](./media/image1.png)

3.  **Help** tab holds the Support information. The **ID** value here is
    the **Lab instance ID** which will be used during the lab execution.

    ![](./media/image2.png)

##  Task 1 : Register Service provider

1.  Open a browser go to +++https://portal.azure.com+++ and sign in with
    your cloud slice account below.

    Username: <+++@lab.CloudPortalCredential>(User1).Username+++
 
    Password: <+++@lab.CloudPortalCredential(User1).Password>+++
 
   ![](./media/image3.png)
 
   ![](./media/image4.png)

2.  Click on **Subscriptions** tile.

    ![](./media/image5.png)

3.  Click on the subscription name.

     ![](./media/image6.png)

4.  Expand Settings from the left navigation menu. Click on **Resource
    providers**, enter **+++Microsoft.AlertsManagement+++** and select
    i,t, and then click **Register**.

     ![](./media/image7.png)

     ![](./media/image8.png)

5.  Click on **Resource providers**,
    enter +++**Microsoft.DBforPostgreSQL+++** and select i,t, and then
    click **Register**.

      ![](./media/image9.png)
      
      ![](./media/image10.png)
      
      ![](./media/image11.png)
      
      ![](./media/image12.png)
6.  Repeat the steps \#10 and \#11 to register the following Resource
    providers.

    - Microsoft.Search
    
    - Microsoft.Web
    
    - Microsoft.ManagedIdentity
      
    - Microsoft.AlertsManagement

## **Task 2: Create Azure OpenAI resource**

1.  In Azure portal, click on **portal menu** represented by three
    horizontal bars on the top left corner of page, as shown in the
    below image.

    ![](./media/image13.png)

2.  Navigate and click on **+ Create a resource**.

     ![](./media/image14.png)

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type +++**Azure OpenAI+++**, then press
    the **Enter** button.

     ![](./media/image15.png)

4.  In the **Marketplace** page, navigate to the **Azure OpenAI** tile,
    click on the V chevron button beside **Create**, then navigate and
    click on the **Azure OpenAI** as shown in the below image.

     ![](./media/image16.png)

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

    a.  **Subscription**: Select the assigned subscription

    b.  **Resource group:** : Select the assigned Resource group

    c.  **Region**: For this lab, you will use a  **gpt-4o**
        model. This model is currently only available in [certain
        regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models).
        Please select a region from this list, In this lab **Sweden
        Central** is using for this resource.

    d.  **Name**: **aoai-gpt4o-visionXXXXX** (XXXXX can be Lab instant
        ID)

    e.  **Pricing tier**: Select **Standard S0**

    **Note**: To find your lab instant ID, select 'Help' and copy the
  instant ID.
 
    ![](./media/image17.png)
   
    ![](./media/image18.png)
   
    ![](./media/image19.png)

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

    ![](./media/image20.png)

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

     ![](./media/image21.png)

8.  In the **Review + submit** tab, once the Validation is Passed, click
    on the **Create** button.

     ![](./media/image22.png)

9.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on **Go to resource** button.

     ![](./media/image23.png)

11. In the Overview section of the Azure OpenAI home page, copy the
    Azure OpenAI resource name, resource group, and subscription ID, and
    save them in a notepad.

     ![](./media/image24.png)

12. Click on **Keys and Endpoints** from the left navigation menu and
    then copy the endpoint value in a notepad to **AzureAI ENDPOINT**
    and key to a variable **AzureAIKey**.

     ![](./media/image25.png)

13. On the **aoai-gpt4o-visionXX** window, click on **Overview** in the
    left-sided navigation menu, scroll down to **Get Started** tile and
    click on **Go to AzureOpenAI Studio** button as shown in the below
    image to open **Azure AI Foundry portal** in a new browser.

    ![](./media/image26.png)

## **Task 3: Deploying an Azure OpenAI model gpt-4o**

1.  On the **Azure AI Foundry | Azure Open AI Service** homepage,
    navigate to **Components** section and click on **Deployments**.

    ![](./media/image27.png)

2.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

     ![](./media/image28.png)

3.  In the **Select a model** dialog box, navigate and carefully select
    **gpt-4o**, then click on **Confirm** button.

     ![](./media/image29.png)

4.  In the **Deploy model gpt-4o** dialog box, under the **Deployment
    name** field, ensure that **gpt-4o**, select the Deployment type as
    **Standard** and select Model ersion as Vision- preview. Then click
    on the **Deploy** button.

    ![](./media/image30.png)
    
    ![](./media/image31.png)

## Task 4: GPT-4o with Vision demo

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

     ![](./media/image32.png)

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open Folder**.

    ![](./media/image33.png)

3.  Navigate and select **gpt-4o-image-classification** folder from
    **C:\LabFiles** and click on the **Select Folder** button.

    ![](./media/image34.png)

4.  If you see a dialog box - **Do you trust the authors of the files in
    this folder?**, then click on **Yes, I trust the author**.

     ![](./media/image35.png)

5.  In Visual Studio Code dropdown the **GPT-4O-IMAGE-CLASSIFICATION**,
    click on **azure.env** file.

     ![](./media/image36.png)

6.  Update the parameters ,replace **Azure OpenAI resource name,
    Subscription, Resource group name,** **Azure OpenAI Endpoint, Azure
    OpenAI Key(**The values that you have saved in your notepad in the
    **Task 2)** and Save the file.

    ![](./media/image37.png)
    ![](./media/image38.png)

7.  In Visual Studio Code dropdown the **GPT-4O-IMAGE-CLASSIFICATION**
    and select **Image classification with Azure OpenAI gpt-4o - Flowers
    example.ipynb** notebook.

      ![](./media/image39.png)

8.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1^(st) cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

    ![](./media/image40.png)
   
    ![](./media/image41.png)

9.  If prompted to select the path, then select the **Python version
    3.11.5** path as shown in the image.

     ![](./media/image42.png)

10. If you see an windows security alert dialog box - then click on
    **Allow access**.

     ![](./media/image43.png)
  
      ![](./media/image44.png)
      ![](./media/image45.png)
      
       ![](./media/image46.png)
      
      ![](./media/image47.png)

11. To restart Jupyter kernel, click on **Restart** button.

      ![](./media/image48.png)
     
      ![](./media/image49.png)

12. To import the libraries, select cell. Then, execute the cell by
    clicking on the **start icon**.

     ![](./media/image50.png)

13. Select **4^(th)** cell. Then, execute the cell by clicking on the
    **start icon**.

     ![](./media/image51.png)

14. To check the OpenAI, system versions, select **5^(th)**,6^(th) and
    7^(th) cells. Then, execute the cell by clicking on the **start
    icon**.

    ![](./media/image52.png)
   
    ![](./media/image53.png)

15. Define a helper function to create embeddings, select and execute
    the 8^(th) ,9^(th) , 10^(th) and 11^(th) cells by clicking on the
    **Play** button.

    ![](./media/image54.png)
   
    ![](./media/image55.png)
   
    ![](./media/image56.png)
   
    ![](./media/image57.png)

16. To Image classification, select and execute the 12^(th) , 13^(th)
    ,14^(th) and 15^(th) cells by clicking on the **Play** button.

    ![](./media/image58.png)
   
    ![](./media/image59.png)
   
    ![](./media/image60.png)

17. To test, select and execute the **16^(th) ,17^(th)** ,**18^(th)**
    and **19^(th)** cells by clicking on the **Play** button.

    ![](./media/image61.png)
    
    ![](./media/image62.png)
    
    ![](./media/image63.png)
    
    ![](./media/image64.png)
    
    ![](./media/image65.png)
    
    ![](./media/image66.png)
    
    ![](./media/image67.png)

     ![](./media/image68.png)

18. Select and execute the **20^(th) ,21^(st) 22^(nd) ,23^(rd) ,24^(th)
    and 25^(th)** cells by clicking on the **Play** button.

      ![](./media/image69.png)
     
     ![](./media/image70.png)
     
      ![](./media/image71.png)
     
       ![](./media/image72.png)
     
      ![](./media/image73.png)
     
      ![](./media/image74.png)
     
     ![](./media/image75.png)
     
     ![](./media/image76.png)
     
      ![](./media/image77.png)
    ![](./media/image78.png)

## Task 5: Delete the resources

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

     ![](./media/image79.png)

2.  Click on the **ResourceGroup1** resource group.

     ![](./media/image80.png)

3.  In the **Resource group** home page, select the **delete resource
    group**

     ![](./media/image81.png)

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “resource group name” to confirm deletion**
    field, then click on the **Delete** button.

     ![](./media/image82.png)

5.  On **Delete confirmation** dialog box, click on **Delete** button.

     ![](./media/image83.png)

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

     ![](./media/image84.png)

**Summary**

This usecase presents a Streamlit-based web application that allows
users to upload images and receive descriptive classifications powered
by Azure OpenAI's GPT-4o model. It highlights the model’s ability to
interpret visual content and generate natural language responses.

