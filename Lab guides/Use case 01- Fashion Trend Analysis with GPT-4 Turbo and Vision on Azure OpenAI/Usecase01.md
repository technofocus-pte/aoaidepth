**Use Case 01- Fashion Trend Analysis with GPT-4 Turbo and Vision on
Azure OpenAI**

**Introduction:**

GPT-4 Turbo with Vision on Azure OpenAI service is now in public
preview. GPT-4 Turbo with Vision is a large multimodal model (LMM)
developed by OpenAI that can analyze images and provide textual
responses to questions about them. It incorporates both natural language
processing and visual understanding. With enhanced mode, you can use the
Azure AI Vision features to generate additional insights from the images

**Objective:**

- To deploy Azure OpenAI resources and configure them.

- To deploy specific Azure OpenAI model like GPT-4 Vision.

- Set up your development environment with Python, Jupyter Notebook, and
  required libraries.

- This usecase related to fashion use cases. These might involve image
  analysis, text generation, or other AI tasks.

## **Task 1: Register the required Resource providers**

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:+++https://portal.azure.com/+++, then press
    the **Enter** button.

    ![](./media/b1.png)

2.  In the **Sign in** window, enter the **Username** and click on the
    **Next** button.

     ![](./media/b2.png)

3.  Then, enter the password and click on the **Sign in** button**.**

      ![](./media/b3.png)
4.  In **Stay signed in?** window, click on the **Yes** button.

      ![](./media/b4.png)

5.  On **Welcome to Microsoft Azure** dialog box, click on **Maybe
    later** button.

      ![](./media/b5.png)

6.  In the Azure portal search box, type **Subscriptions**, then click
    on **Subscriptions** under **Services**.

      ![](./media/b6.png)

7.  In the **Subscriptions** page, navigate and click on **Azure Pass –
    Sponsorship**.

      ![](./media/b7.png)

8.  In the **Azure Pass – Sponsorship** page left-sided navigation menu,
    navigate to the **Settings** section, then click on the **Resource
    Providers**.

      ![](./media/b8.png)

9.  In the **Azure Pass – Sponsorship | Resource providers** page,
    navigate to the search box and type **Microsoft.Storage**. Select
    the **Microsoft.Storage** under **Provider**, then click on the
    **Register** as shown in the below image.

      ![](./media/b9.png)

10. You’ll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

      ![](./media/b10.png)

11. In the **Azure Pass – Sponsorship | Resource providers** page,
    navigate to the search box and type **Microsoft.Security**. Select
    the **Microsoft.Security** under **Provider**, then click on the
    **Register** as shown in the below image.

    ![](./media/b11.png)

12. You’ll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

      ![](./media/b12.png)

13. Repeat the steps \#10 and \#11 to register the following Resource
    providers.

      - **Microsoft.CognitiveServices**
  
      - **Microsoft.Search**
  
      - **Microsoft.Sql**
  
      - **Microsoft.Web**
  
      - **Microsoft.ManagedIdentity**
        
      - **Microsoft.AlertsManagement**
      - **Microsoft.DBforPostgreSQL**

## **Task 2: Create Azure OpenAI resource**

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL: +++https://portal.azure.com/+++, then press the
    **Enter** button.

     ![](./media/image1.png)

2.  In the **Microsoft Azure** window, use the **User Credentials** to
    login to Azure.

      ![](./media/image2.png)

3.  Then, enter the password and click on the **Sign in** button**.**

     ![](./media/image3.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

     ![](./media/image4.png)

5.  In Azure portal, click on **portal menu** represented by three
    horizontal bars on the top left corner of page, as shown in the
    below image.

    ![](./media/image5.png)

6.  Navigate and click on **+ Create a resource**.

      ![](./media/image6.png)

7.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

      ![](./media/image7.png)

8.  In the **Marketplace** page, navigate to the **Azure OpenAI** tile,
    click on the V chevron button beside **Create**, then navigate and
    click on the **Azure OpenAI** as shown in the below image.

      ![](./media/image8.png)

9.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

    a.  **Subscription**: Select the assigned subscription

    b.  **Resource group:** Click on **Create new**\> enter
        **AOAI-RGXX**(XX can be a unique number, you can add more digits
        after XX to make the name unique)

    c.  **Region**: For this lab, you will use a  **gpt-4-vision**
        model. This model is currently only available in [certain
        regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models).
        Please select a region from this list, In this lab **Sweden
        Central** is using for this resource.

    d.  **Name**: **aoai-gpt4-visionXXXXX** (XXXXX can be Lab instant
        ID)

    e.  **Pricing tier**: Select **Standard S0**

      ![](./media/image9.png)

10. In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

     ![](./media/image10.png)

11. In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

     ![](./media/image11.png)

12. In the **Review + submit** tab, once the Validation is Passed, click
    on the **Create** button.

     ![](./media/image12.png)

13. Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

14. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on **Go to resource** button.

     ![](./media/image13.png)

15. Click on **Keys and Endpoints** from the left navigation menu and
    then copy the endpoint value in a notepad to **AzureAI ENDPOINT**
    and key to a variable **AzureAIKey**.

     ![](./media/image14.png)

16. On the **aoai-gpt4-visionXX** window, click on **Overview** in the
    left-sided navigation menu, scroll down to **Get Started** tile and
    click on **Go to AzureOpenAI Studio** button as shown in the below
    image to open **Azure OpenAI Studio** in a new browser.

     ![](./media/image15.png)

## **Task 3: Deploying an Azure OpenAI model gpt-4-vision**

1.  On the **Azure AI Foundry | Azure Open AI Service** homepage,
    navigate to **Components** section and click on **Deployments**.

2.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

      ![](./media/image16.png)

3.  In the **Select a model** dialog box, navigate and carefully select
    **gpt-4**, then click on **Confirm** button.

      ![](./media/image17.png)

4.  In the **Deploy model gpt-4** dialog box, under the **Deployment
    name** field, ensure that **gpt-4**, select the Deployment type as
    **Standard** and select Model ersion as Vision- preview. Then click
    on the **Deploy** button.

    ![](./media/image18.png)
    
    ![](./media/image19.png)

## Task 4: GPT-4 Turbo with Vision demo

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

    ![](./media/image20.png)

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open Folder**.

    ![](./media/image21.png)

3.  Navigate and select **GPT4V-Fashion** folder from **C:\LabFiles**
    and click on the **Select Folder** button.

    ![](./media/image22.png)

4.  If you see a dialog box - **Do you trust the authors of the files in
    this folder?**, then click on **Yes, I trust the author**.

      ![](./media/image23.png)

5.  In Visual Studio Code dropdown the **Gpt 4V-FASHION**, click on
    **azure.env** file.

     ![](./media/image24.png)

6.  Update the parameters ,replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    1)** and Save the file.

    ![](./media/image25.png)

7.  In Visual Studio Code dropdown the **GPT 4V-FASHION** and select
    **GPT-4 with Vision demo with Azure Open AI - Fashion
    usecase.ipynb** notebook.

     ![](./media/image26.png)

8.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1^(st) cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

     ![](./media/image27.png)
    
     ![](./media/image28.png)

9.  If prompted to select the path, then select the **Python version
    3.11.5** path as shown in the image.

  ![](./media/image29.png)

10.  If you see an windows security alert dialog box - then click on
    **Allow access**.

     ![](./media/image30.png)
    
     ![](./media/image31.png)
    
     ![](./media/image32.png)
    
     ![](./media/image33.png)

11.  To restart Jupyter kernel, click on **Restart** button.

     ![](./media/image34.png)

12.  To import the libraries, select **4^(th)** cell. Then, execute the
    cell by clicking on the **start icon**.

     ![](./media/image35.png)

13.  Select **5^(th)** cell. Then, execute the cell by clicking on the
    **start icon**.

     ![](./media/image36.png)

14.  To check the OpenAI, system versions, select **6^(th)**,7^(th) ,
    8^(th) and 9^(th) cells. Then, execute the cell by clicking on the
    **start icon**.

     ![](./media/image37.png)

15. To load the configuration values, select and execute the **10^(th)**
    ,11^(th) and 12^(th) cells by clicking on the **Play** button.

     ![](./media/image38.png)

16. Define a helper function to create embeddings, select and execute
    the 13^(th) .14^(th) cells by clicking on the **Play** button.

      ![](./media/image39.png)
     
      ![](./media/image40.png)

12. To run the example, select and execute the 15^(th) , 16^(th) cells
    by clicking on the **Play** button.

      ![](./media/image41.png)
     
      ![](./media/image42.png)

13. To run the example, select and execute the **17^(th) ,18^(th)**
    cells by clicking on the **Play** button.

      ![](./media/image43.png)
     
      ![](./media/image44.png)

14. To run the example, select and execute the **19^(th) ,20^(th)**
    cells by clicking on the **Play** button.
     ![](./media/image45.png)
 
    ![](./media/image46.png)

15. To run the example, select and execute the **21^(st) ,22^(nd)**
    cells by clicking on the **Play** button.

    ![](./media/image47.png)
   
    ![](./media/image48.png)

16. To run the example, select and execute the **23^(st) ,24^(nd)**
    cells by clicking on the **Play** button.

     ![](./media/image49.png)

     ![](./media/image50.png)

17. To run the example, select and execute the **25^(th) ,26^(th)**
    cells by clicking on the **Play** button.

      ![](./media/image51.png)
     
      ![](./media/image52.png)

18. To run the example, select and execute the **27^(th) ,28^(th)**
    cells by clicking on the **Play** button.

     ![](./media/image53.png)
 
    ![](./media/image54.png)

19. To run the example, select and execute the **27^(th) ,28^(th)**
    cells by clicking on the **Play** button.

      ![](./media/image55.png)
 
     ![](./media/image56.png)

20. To generate WebApp, select and execute the **29^(th)** cells by
    clicking on the **Play** button.

     ![](./media/image57.png)

21. To generate WebApp, select and execute the **30^(th)** cell by
    clicking on the **Play** button.

      ![](./media/image58.png)

22. After the application has been successfully deployed, you see a URL
    displayed in the terminal. Copy the **URL**

      ![](./media/image59.png)

23. Open your browser, navigate to the address bar, paste the Publick
    URL link.
    ![](./media/image60.png)

25. Open your browser, navigate to the address bar, paste the local URL
    link. Select any item

     ![](./media/image61.png)

25. Click on the **Submit** button.

    ![](./media/image62.png)

    ![](./media/image63.png)

## Task 5: Delete the resources

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

     ![](./media/image64.png)

2.  Click on the AOAI-RGXXX resource group.

     ![](./media/image65.png)

3.  In the **Resource group** home page, select the **delete resource
    group**

     ![](./media/image663.png)

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “resource group name” to confirm deletion**
    field, then click on the **Delete** button.

     ![](./media/image67.png)

5.  On **Delete confirmation** dialog box, click on **Delete** button.

      ![](./media/image68.png)

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

      ![](./media/image69.png)

**Summary**

In this hands-on lab, participants delve into advanced AI capabilities
using Azure OpenAI. Starting with the setup of essential Azure
resources, they deploy AI models like GPT-4-vision. The lab specifically
explores how GPT-4, equipped with vision capabilities, can revolutionize
fashion-related tasks—think image recognition, personalized style
recommendations, and trend analysis.
