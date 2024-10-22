# Lab 01: Provisioning Azure OpenAI resource and exploring Azure AI Studio Playground

**Introduction**

Azure OpenAI Service brings the generative AI models developed by OpenAI
to the Azure platform, enabling you to develop powerful AI solutions
that benefit from the security, scalability, and integration of services
provided by the Azure cloud platform. The first step to use an Azure
Open AI model is to provision an Azure OpenAI resource. In this lab,
you’ll learn how to get started with Azure OpenAI service by
provisioning Azure OpenAI resource in the Azure portal.

**Objectives**

- To configure VM settings and register necessary Azure resource
  providers.

- To create an Azure OpenAI resource and retrieve key and endpoint.

- To install the required Python libraries.

## **Task 0: Sync Host environment time**

1.  In your VM, navigate and click in the **Search bar**, type
    **Settings** and then click on **Settings** under **Best match**.

     ![](./media/image1.png)

2.  On Settings window, navigate and click on **Time & language**.

      ![](./media/image2.png)

3.  On **Time & language** page, navigate and click on **Date & time**.

      ![](./media/image3.png)

4.  Scroll down and navigate to **Additional settings** section, then
    click on **Syn now** button. It will take 3-5 minutes to syn.

     ![](./media/image4.png)

5.  Close the **Settings** window.

      ![](./media/image5.png)

## **Task 1: Register the required Resource providers**

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:+++https://portal.azure.com/+++, then press
    the **Enter** button.

      ![](./media/image6.png)

2.  In the **Sign in** window, enter the **Username** and click on the
    **Next** button.

      ![](./media/image7.png)

3.  Then, enter the password and click on the **Sign in** button.

       ![](./media/image8.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

       ![](./media/image9.png)

5.  On **Welcome to Microsoft Azure** dialog box, click on **Maybe
    later** button.

     ![](./media/image10.png)

6.  In the Azure portal search box, type **Subscriptions**, then click
    on **Subscriptions** under **Services**.

       ![](./media/image11.png)

7.  In the **Subscriptions** page, navigate and click on **Azure Pass –
    Sponsorship**.

       ![](./media/image12.png)

8.  In the **Azure Pass – Sponsorship** page left-sided navigation menu,
    navigate to the **Settings** section, then click on the **Resource
    Providers**.

      ![](./media/image13.png)

9.  In the **Azure Pass – Sponsorship | Resource providers** page,
    navigate to the search box and type **+++Microsoft.Storage+++**. Select
    the **Microsoft.Storage** under **Provider**, then click on the
    **Register** as shown in the below image.

      ![](./media/image14.png)

10. You’ll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

      ![](./media/image15.png)

11. In the **Azure Pass – Sponsorship | Resource providers** page,
    navigate to the search box and type **+++Microsoft.Security+++**. Select
    the **Microsoft.Security** under **Provider**, then click on the
    **Register** as shown in the below image.

      ![](./media/image16.png)

12. You’ll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

     ![](./media/image17.png)

13. Repeat the steps \#10 and \#11 to register the following Resource
    providers.

    - **+++Microsoft.CognitiveServices+++**

    - **+++Microsoft.Search+++**

    - **+++Microsoft.Sql+++**

    - **+++Microsoft.Web+++**

    - **+++Microsoft.ManagedIdentity+++**

## **Task 2: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

     ![](./media/image18.png)

2.  Navigate and click on **+ Create a resource**.

     ![](./media/image19.png)

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

      ![](./media/image20.png)

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

       ![](./media/image21.png)

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.
    |  |  |
    |-----|-----|
    |Subscription	|Select the assigned subscription|
    |Resource group	|Click on Create new> enter +++AOAI-RGXX+++(XX can be a unique number, you can add more digits after XX to make the name unique)|
    |Region	|East US 2 |
    |Name|+++Azure-openai-testXX+++ (XX can be a unique number, you can add more digits after XX to make the name unique) (here, we entered Azure-open-test39)|
    |Pricing tier|	Select Standard S0|
 **Note**:For this lab, you will use a GPT-4O model. This model is currently only available in [certain regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models). Please select a region from this list, In this lab East US 2 is using for this resource.
     ![](./media/image22.png)
     ![](./media/image23.png)

7.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

      ![](./media/image24.png)

8.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

      ![](./media/image25.png)

9.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

     ![](./media/image26.png)

10.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

     ![](./media/image27.png)

11. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

     ![](./media/image28.png)

## Task 3: Create a Speech resource in the Azure portal

1.  Open your browser, navigate to the address bar, and paste the
    following URL:
    +++https://portal.azure.com/#create/Microsoft.CognitiveServicesSpeechServices+++
    then press the **Enter** button.

      ![](./media/image29.png)

2.  On the **Create Speech Services** page, enter the following
    information, then click on **Review+create** button.

    |Field	|Description|
    |-----|----|
    |Subscription	|Select your Azure OpenAI subscription|
    |Resource group|	Select your Resource group (that you have created in Task 2)|
    |Region|	East US|
    |Name|SpeechChat-testXX (XX can be unique number)|
    |Pricing Tier|	Standard S0|

     ![](./media/image30.png)

3.  Once the Validation is passed, click on the **Create** button.

      ![](./media/image31.png)

4.  Wait for few minutes until the deployment is completed.

     ![](./media/image32.png)

## **Task 4: Create the project using Azure AI Studio**

1.  After the deployment is completed, click on **Home** at the top left
    corner of the page to go back to Azure portal. In the Azure portal,
    navigate and click on **Resource groups** under **Azure services**.

     ![](./media/image33.png)
     ![](./media/image34.png)

2.  Select the resource group that you’ve created in **Lab \#1**.

     ![](./media/image35.png)

3.  In the **AOAI-RGXX Resource group** page, navigate and click on
    **Azure-openai-testXX** as shown in the below image.

    ![](./media/image36.png)

4.  In **Azure-openai-testXX** page, click on **Overview** in the
    left-sided navigation menu, scroll down and click on **Explore Azure
    AI Studio** button as shown in the below image.

     ![](./media/image37.png)

     ![](./media/image38.png)

5.  On **Azure AI Studio** window, click on **Create now** button.

     ![](./media/image39.png)

6.  On Create an AI project tab, click on **Create a new project and
    continue**

     ![](./media/image40.png)

7.  On Create an AI project tab, click on **Create a new project** .

    ![](./media/image41.png)

8.  On Create an AI project tab, click on **Next** button.

     ![](./media/image42.png)

9.  On Create an AI project tab, click on **Next** button.

     ![](./media/image43.png)

10. On Create an AI project tab, click on **Create Project** button.

     ![](./media/image44.png)

     ![](./media/image45.png)

11. Now, you’re directed to the **Azure AI Studio** home page,

     ![](./media/image46.png)

## **Task 5: Hear and speak with chat models in the Azure AI Studio playground**

Give your app the ability to hear and speak by pairing Azure OpenAI
Service with Azure AI Speech to enable richer interactions.

The speech to text and text to speech features can be used together or
separately in the Azure AI Studio playground. You can use the playground
to test your chat model before deploying it.

In this chat session, you use both speech to text and text to speech.
You use the speech to text feature to speak to the assistant, and the
text to speech feature to hear the assistant's response.

1.  In the **Azure AI Studio Preview** page, navigate to **Components**
    section and click on **Deployments**.

     ![](./media/image47.png)

2.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

     ![](./media/image48.png)

3.  In the **Select a model** dialog box, navigate and carefully select
    **gpt-4o**, then click on **Confirm** button.

     ![](./media/image49.png)

4.  In the **Deploy model gpt-4o** dialog box, under the **Deployment
    name** field, ensure that **gpt-4o**, then click on the **Deploy**
    button.

     ![](./media/image50.png)

5.  **gpt-4o** deployment is successful.

      ![](./media/image51.png)

6.  In **gpt-4o** pane, click on **Open in Playground** button.

     ![](./media/image52.png)

7.  Ensure that **gpt-4o** is selected under **Deployment**.

     ![](./media/image53.png)

8.  Now, navigate to the Chat session section and click on **Chat
    capabilities**.

     ![](./media/image54.png)

** Note:** You should also see the options to select the microphone or
speaker buttons. If you select either of these buttons but haven't yet
enabled speech to text or text to speech, you are prompted to enable
them in **Playground Settings**.

9.  On the **Playground Settings** page, provide the following
    information and then click on the **Save** button.
    
    |  |   |
    |----|---|
    |Language	|Select the language locale and voice you want to use for speaking and hearing. (In this lab, we are selecting English).|
    |Subscription|Select your Azure OpenAI subscription|
    |Speech resource |Select your speech resource group that you’ve created in Task #1.|
    |Voice configuration|	Emma|


    - **Select the check box**-I acknowledge that spoken chat will incur
      usage to my subscription.
    
    - Select **Enable speech to text** and **Enable text to speech**.
    
    **Note**: Optionally, you can enter some sample text and
    select **Play** to try the voice.

     ![](./media/image55.png)

10. Select the microphone button and speak to the assistant. For
    example, you can say "**Do you know where I can get an Xbox**".

     ![](./media/image56.png)

12. In case, use your microphone dialog box appears, then click on the
    **Allow** button.

     ![](./media/image57.png)

13. Click on the **Send** button (represented by right arrow) to send
    your message to the assistant. The assistant's response is displayed
    in the chat session pane.

      ![](./media/image58.png)

     ![](./media/image59.png)

** Note:** If the speaker button is turned on, you'll hear the
assistant's response. If the speaker button is turned off, you won't
hear the assistant's response, but the response will still be displayed
in the chat session pane.

14. Select the microphone button and speak to the assistant. You can say
    " **How do the capabilities of Azure OpenAI compare to OpenAI?”**

15. Click on the **Send** button (represented by right arrow) to send
    your message to the assistant. The assistant's response is displayed
    in the chat session pane.

     ![](./media/image60.png)

     ![](./media/image61.png)

16. Navigate to **Assistant setup** section. You can change the system
    prompt to change the assistant's response format or style. Paste the
    following content under **System message** box, then click on
    **Apply changes** as shown in the below image.

     Copy
      ```
     "You're an AI assistant that helps people find information. Answers
     shouldn't be longer than 20 words because you are on a phone. You
     could use 'um' or 'let me see' to make it more natural and add some
     disfluency."
     ```
     ![](./media/image62.png)

17. In the **Update system message?** dialog box, click on the
    **Continue button.**

     ![](./media/image63.png)

18. Select the microphone button and speak to the assistant. You can say
    "**Do you know where I can get an Xbox?”**

19. Click on the Send button (represented by right arrow) to send your
    message to the assistant. The assistant's response is displayed in
    the chat session pane.

      ![](./media/image64.png)

      ![](./media/image65.png)

20. Select the **View Code** button to view and copy the sample code,
    which includes configuration for Azure OpenAI and Speech services.
    You can use the sample code to enable speech to text and text to
    speech in your application.

      ![](./media/image66.png)

      ![](./media/image67.png)

## Task 6: Install Python libraries and pip updating 

1.  In your windows search bar, type **Command Prompt**. In the
    **Command Prompt App** dialog box, navigate and click on **Run as
    administrator**. If you see the dialog box - **Do you want to allow
    this app to make changes to your device?** then click on the **Yes**
    button.
   
     ![](./media/image68.png)

2.  Move into the folder where the Python was installed and run the
    **pip** command. i.e., **C:\Users\Admin**
    ```
    python -m pip install --upgrade pip
    ```
    ![](./media/image69.png)

3.  Run the following command to install Python libraries - openai,
    num2words, matplotlib, plotly, scipy, scikit-learn, pandas, tiktoken
    ```
    pip install openai num2words matplotlib plotly scipy scikit-learn pandas
    tiktoken
    ``` 
     ![](./media/image70.png)
     ![](./media/image71.png)
4.  Run the below command to install the Transformers package:

    ```
    pip install transformers
    ```
   ![](./media/image72.png)

## **Task 7: Clean up resources**

To avoid incurring unnecessary Azure costs, you should delete the
resources you created in this quick start if they're no longer needed.
To manage resources, you can use the [Azure
portal](https://portal.azure.com/?azure-portal=true).

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

     ![](./media/image34.png)

2.  Click on the resource group that you’ve created.
    ![](./media/image73png)

3.  In the **Resource group** home page, select the **delete resource
    group** .

     ![](./media/image74.png)

4.  In the Delete a resource group tab, enter your resource group name
    and click on **Delete button**.
     ![](./media/image75.png)

5.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “delete” to confirm deletion** field, type
    **delete**, then click on the **Delete** button.

      ![](./media/image76.png)

6.  On **Delete confirmation** dialog box, click on **Delete** button.

     ![](./media/image77.png)

7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 4 selected items.**

**Summary**

In this lab, you’ve set the VM time, registered the necessary Azure
resource providers, then provisioned Azure OpenAI resource. You’ve
learned how to retrieve keys and endpoint information that will be used
for deploying Azure OpenAI models in the upcoming labs. Finally, you’ve
successfully installed Python libraries.

This lab focuses on hands-on exploration of Azure AI Studio and Azure
Cognitive Services for Speech and OpenAI integration. In this lab,
you’ve created and deployed resources, developed and tested text
completions, and engaged in chat sessions with AI models. At the end of
the lab, you’ve deleted the resources to avoid incurring unnecessary
Azure costs. In this lab, you’ve acquired practical skills in AI model
deployment, customization, and integration with speech capabilities,
making it a comprehensive learning experience in Azure AI technologies.
