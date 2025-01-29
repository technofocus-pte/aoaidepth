**Lab 07: Implementing Q&A using semantic answering**

**Introduction**

A simple web application for an OpenAI-enabled document search. This
repo uses Azure OpenAI Service for creating embeddings vectors from
documents. For answering the question of a user, it retrieves the most
relevant document and then uses GPT-3 to extract the matching answer for
the question.

![Architecture](./media/image1.png)

**Objectives**

- To deploy chat and embedding models in Azure AI Studio.

- To use a custom template for deploying the required resources such as
  App Service, Search Service, Form recognizer, etc.

- To deploy aoaichatsearch-site Web App and perform Azure OpenAI-enabled
  document search, text summarization, and conversation data extraction.

- To delete the deployed resources and models.

## **Task 1: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)

2.  Navigate and click on **+ Create a resource**.

> ![A screenshot of a computer Description automatically
> generated](./media/image3.png)

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image4.png)

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

> ![A screenshot of a computer Description automatically
> generated](./media/image5.png)

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

[TABLE]

> ![A screenshot of a computer Description automatically
> generated](./media/image6.png)

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image7.png)

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image8.png)

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image9.png)

9.  Wait for the deployment to complete. The deployment will take around
    **2-3** minutes.

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

![A screenshot of a computer Description automatically
generated](./media/image10.png)

11. In your **Azure-open-testXX | Model deployments** window, navigate
    to the **Resource Management** section, and click on **Keys and
    Endpoints**.

![A screenshot of a computer Description automatically
generated](./media/image11.png)

12. In **Keys and Endpoints** page, copy **KEY1, KEY 2,** and
    **Endpoint** values and paste them in a notepad as shown in the
    below image, then **Save** the notepad to use the information in the
    upcoming lab.

![A screenshot of a computer Description automatically
generated](./media/image12.png)

## **Task 2: Deploy the Chat model and Embedding model**

1.  In **Azure-openai-testXX** page, click on **Overview** in the
    left-sided navigation menu, scroll down and click on **Go to Azure
    OpenAI Studio** button as shown in the below image.

![](./media/image13.png)

2.  Wait for the Azure OpenAI studio to launch.

> ![A screenshot of a computer Description automatically
> generated](./media/image14.png)

3.  On the **Azure AI Foundry** |**Azure OpenAI Studio** homepage select
    **Deployment** from the left navigation menu**.**

![A screenshot of a computer Description automatically
generated](./media/image15.png)

4.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

> ![A screenshot of a computer Description automatically
> generated](./media/image16.png)

5.  In the **Select a model** dialog box, navigate and carefully select
    **gpt-4**, then click on **Confirm** button.

![](./media/image17.png)

6.  Select the **Model version** as **0125-Preview,** in the
    **Deployment type** as **Standard, Deployment name field**, enter
    **gpt-4**, and click on the **Create** button.

> ![](./media/image18.png)

![A screenshot of a computer Description automatically
generated](./media/image19.png)

7.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

> ![](./media/image20.png)

8.  In the **Select a model** dialog box, navigate and carefully select
    **text-embedding-ada-002** then click on **Confirm** button.

![](./media/image21.png)

9.  In the **Deploy model** dialog box, under **Deployment name** enter
    +++**text-embedding-ada-002+++,** select the **Standard** as
    **Deployment type** and Click on the **Deploy** button.

![](./media/image22.png)

![A screenshot of a computer Description automatically
generated](./media/image23.png)

## **Task 3: Deploy on Azure (WebApp + Batch Processing) with Azure Cognitive Search**

1.  Open your edge browser, navigate to the address bar, and type or
    paste the following URL:
    <https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fruoccofabrizio%2Fazure-open-ai-embeddings-qna%2Fmain%2Finfrastructure%2Fdeployment_ACS.json>
    then press the **Enter** button.

![](./media/image24.png)

2.  On **Custom deployment** window, under the **Basics** tab, enter the
    following details to deploy the custom template and then click on
    **Review + create.**

[TABLE]

![](./media/image25.png)

![](./media/image26.png)

3.  On **Review + create** tab, once the Validation is Passed, click on
    the **Create** button.

![](./media/image27.png)

4.  Wait for the deployment to complete. The deployment will take around
    15-17 minutes.

> ![A screenshot of a computer Description automatically
> generated](./media/image28.png)

5.  Click on the **Go to resource group** button.

> ![](./media/image29.png)

## **Task 4: Azure OpenAI-enabled document search through web application**

1.  On the **aoaiXXX-RG** resource group window, under **Resources**
    tab, navigate to the **App Service** - **aoaaichatsearch-site** and
    click on it.

![](./media/image30.png)

2.  On **aoaichatsearch-site** Web App **Overview** page, navigate to
    the command bar and click on **Browse**, it will navigate you to the
    web application.

![](./media/image31.png)

3.  Wait for the web application deployment to complete. The deployment
    will take approximately **10-15** minutes.

![A screenshot of a computer Description automatically
generated](./media/image32.png)

4.  On the web application home page, to verify the deployments status
    click on the **Check deployments** button under Microsoft.

![](./media/image33.png)

5.  To check the deployment status, it may take around 5-6 min.

![A screenshot of a computer Description automatically
generated](./media/image34.png)

![](./media/image35.png)

6.  On Web App home page, navigate and click on **Add Document** on the
    left-hand side to add the data.

![](./media/image36.png)

7.  On **Add Document** pane, click on the **Browse files** button to
    upload documents that needs to be added to the knowledge base.

![](./media/image37.png)

8.  Navigate to **C:\Labfiles\Contoso Electronics** location in the VM
    and select **Benefit_Options.pdf,** then click on **Open** button.

![](./media/image38.png)

9.  Click again on the **Browse files,** navigate to
    **C:\Labfiles\Contoso Electronics** location in the VM and select
    **employee_handbook.pdf**, then click on **Open** button.

![](./media/image39.png)

![](./media/image40.png)

10. Similarly, add **Northwind_Health_Plus_Benefits_Details.pdf** and
    **Northwind_Standard_Benefits_Details.pdf**

![](./media/image41.png)

![](./media/image42.png)

11. The uploaded data will be added to the knowledge base and it’ll take
    approximately 5-7 minutes.

12. Click on **Document Management** to verify whether the files are
    successfully uploaded or not.

![](./media/image43.png)

![](./media/image44.png)

13. Click on **Index Management** to verify the files, keys, and source.

![](./media/image45.png)

14. Then, click on **Chat.**

![](./media/image46.png)

15. In the **Chat session** section, enter the following prompt, then
    press the **Enter** button and view the response.

**You**: **what is the employee's portion of the healthcare cost from
each paycheck in Contoso Electronics**

![](./media/image47.png)

![](./media/image48.png)

16. In the **Chat session** section, click on the **Clear chat** button.

![](./media/image49.png)

17. In the **Chat session** section, enter the following prompt, then
    press the **Enter** button and view the response.

**You**: **How do I file a complaint or appeal with Northwind Health
Plus?**

![](./media/image50.png)

18. In the **Chat session** section, click on the **Clear chat** button.

![](./media/image51.png)

19. In the **Chat session** section, enter the following prompt. then
    press the **Enter** button and view the response.

**You**: **Does my plan covers my eye exams?**

![](./media/image52.png)

20. Click on **Utils-Document Summary** on the left-hand side.

![](./media/image53.png)

21. In the **Summarization** section, select the **Basic Summary** radio
    button**.**

![](./media/image54.png)

22. In the **Summarization** window, under **Enter some text to
    summarize** section, in the message box, replace the current text
    with the following, then click on the **Summarize** button.

It’s been six months since we reinvented search with [the new AI-powered
Bing and
Edge](https://blogs.microsoft.com/blog/2023/02/07/reinventing-search-with-a-new-ai-powered-microsoft-bing-and-edge-your-copilot-for-the-web/).
In that short time, you’ve engaged in so many unique and creative ways;
to date we’ve seen over 1 billion chats and over 750 million images fill
the world of Bing! We’ve also seen nine consecutive quarters of growth
on Edge, meaning we’re more able than ever to bring our best-in-class AI
experiences to users across the web.

![](./media/image55.png)

23. Check the summary of the text that you’ve entered.

![](./media/image56.png)

24. After reviewing the Summary result, click on the **Clear summary**
    button.

![](./media/image57.png)

25. Now, scroll up and select the **Bullet Points** radio button.
    Under **Enter some text to summarize** section, in the message box,
    replace the current text with the following and then click on the
    **Summarize** button.

Microsoft has made its Azure OpenAI Service generally available,
bringing the enterprise generative AI tools out of its invite-only
program. Now any customers who meet Microsoft’s standards can access the
professional versions of OpenAI’s large language model GPT-3.5 and the
related text-to-image tool DALL-E 2, computer programming assistant
Codex, and the popular ChatGPT chatbot interface for the LLM.

Microsoft launched the Azure OpenAI Service with an eye toward offering
businesses a way to develop apps without coding, write reports, and put
together marketing content. The scope has grown since then to encompass
new facets of the OpenAI’s models, including chat and visuals. Those
interested in the tools have to explain how they will use the AI tools
and agree to Microsoft’s ethical guidelines in their application for
access. The decision to widen the Azure OpenAI Service’s availability
arrives in tandem with Microsoft’s plans to integrate ChatGPT and DALL-E
into its Office suite, Bing search engine, and other consumer products.
Azure OpenAI Service followed earlier experiments to integrate GPT-3
into Microsoft projects like the low-code Power Apps programming tool
and the GitHub Copilot programming assistant.

![](./media/image58.png)

26. You’ll see the summary results in the form of bullet points.

![](./media/image59.png)

27. Click on **Utils-Conversation Data Extraction** on the left side.

![](./media/image60.png)

28. On the **Conversation data extraction** pane, click on the **Execute
    tasks** and view the response under **OpenAI result**.

![](./media/image61.png)

29. Review the data extracted from the conversation between the Agent
    and the User.

![](./media/image62.png)

## Task 5: Deleting the deployed resources and models

1.  To delete the deployed resources, navigate to **Azure portal home**
    page, click on **Resource groups**.

> ![A screenshot of a computer Description automatically
> generated](./media/image63.png)

2.  In the Resource groups page, select your resource group.

> ![A screenshot of a computer Description automatically
> generated](./media/image64.png)

3.  In the **Resource group** home page, select all resources and click
    on **delete**

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “delete” to confirm deletion** field, then click
    on the **Delete** button.

5.  On **Delete confirmation** dialog box, click on **Delete** button.

> ![A screenshot of a computer error Description automatically
> generated](./media/image65.png)

6.  Click on the bell icon, you’ll see the notification

**Summary**

You've deployed gpt-4 chat model and text-embedding-ada-002 embedding
model in your Azure AI Studio, then you’ve deployed the necessary
resources using a custom template. You've uploaded unstructured
documents in aoaichatsearch-site Web App and extracted the precise
information in a chat session. You've generated basic as well as bullet
points summary from sample texts, then you've extracted the data from a
conversation. At the end of the lab, you've deleted the resources and
models to efficiently manage your Azure OpenAI resources.

**Important Note: Please do not delete the Resource Group. If deleted,
you’ll not be able to proceed with the next lab or create a new Resource
Group.**

**Please do not delete the Azure OpenAI Service (Azure-openai-testXX).
The same service will be used throughout all the labs.**
