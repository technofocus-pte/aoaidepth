# **Use case 08- Build and deploy a question and answer copilot with prompt flow in Azure AI Studio**

**Introduction**

In this [Azure AI Studio](https://ai.azure.com/) use case, you use
generative AI and prompt flow to build, configure, and deploy a copilot
for your retail company called Contoso. Your retail company specializes
in outdoor camping gear and clothing.

The copilot should answer questions about your products and services. It
should also answer questions about your customers. For example, the
copilot can answer questions such as "How much do the TrailWalker hiking
shoes cost?" and "How many TrailWalker hiking shoes did Daniel Wilson
buy?".

In this use case, you’ll learn how to create and deploy your own AI
copilot using Azure AI Studio's prompt flow capabilities. This lab is
designed to equip you with practical skills in setting up Azure AI
resources, designing sophisticated prompt flows, managing diverse data
sources, and optimizing AI models for enhanced performance.

By the end of this use case, you will have acquired essential skills in
leveraging Azure AI Studio’s capabilities to build and deploy a
versatile AI copilot, ready to assist in a range of interactive and
data-driven applications.

**Objectives**

- To provision and configure Azure AI resources, including Cognitive
  Search and role-based access control, to ensure secure deployment and
  management of AI applications.

- To deploy and configure an Azure AI project in Azure AI Studio,
  integrating Azure AI Search for seamless data connections, deploying a
  GPT-4 chat model, and enhancing model capabilities through rigorous
  testing of local data sources in the Azure AI Studio playground.

- To configure and deploy compute instances and runtime environments in
  Azure AI Studio tailored for prompt flow operations, ensuring optimal
  performance and scalability for the copilot's chat model.

- To enhance the Azure AI Studio prompt flow by seamlessly integrating
  multiple data sources, such as product and customer information
  indexes, to enable comprehensive and accurate responses for complex
  queries in the copilot application.

- To delete the deployed resources in order to avoid incurring
  unnecessary Azure costs.

# Exercise 1- Create an Azure AI resource and Azure cognitive Search by using the portal

## **Task 1: Create a secure Azure AI resource in the Azure portal**

If your organization is using [Azure
Policy](https://learn.microsoft.com/en-us/azure/governance/policy/overview),
setup a resource that meets your organization's requirements instead of
using AI Studio for resource creation.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:+++https://portal.azure.com/+++ , then press
    the **Enter** button.

      ![](./media/image1.png)

2.  In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

     ![](./media/image2.png)

3.  Then, enter the password and click on the **Sign in** button**.**

     ![](./media/image3.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

     ![](./media/image4.png)

5.  From the Azure portal, search for **Azure AI Studio** and click on
    **Azure AI Studio.** 

     ![](./media/image5.png)

6.  Select create a new resource by selecting **+ New Azure AI hub**

      ![](./media/image6.png)


7.  On the **Azure AI** Create a search service page, provide the
    following information and click on **Next: Storage** button.

    |   |   |
    |---|---|
    |Field|	Description|
    |Subscription	|Select your Azure OpenAI subscription|
    |Resource group|	Click on Create new> enter +++AOAI-RGXX+++(XX can be a unique number, you can add more digits after XX to make the name unique)|
    |Region|	For this lab, you will use a GPT-4 model. This model is currently only available in certain regions. Please select a region from this list, In this lab East US 2 is using for this resource.|
    |Name	|+++Copilot-AzureAIXX+++ (XXcan be unique number)|

     ![](./media/image7.png)

9.  In the **Storage** tab, leave all in the default state, and click on
    the **Next: Networking** button.

      ![](./media/image8.png)

10.  In the **Networking** tab, select the Public radio buttons, and
    click on the **Next: Encryption** button.

      ![](./media/image9.png)

11. In the **Encryption** tab, click the check box on
    **Microsoft-managed keys** , and click on the **Next: Identity**
    button.

      ![](./media/image10.png)

12. In the **Identity** tab, leave all the fields in the default state,
    and click on the **Review+create** button.

      ![](./media/image11.png)

13. In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

      ![](./media/image12.png)

14. After the deployment is completed, click on the **Go to resource**
    button.

     ![](./media/image13.png)

## **Task 2:Role-based access control in Azure AI Studio**

1.  In your **Copilot-AzureAI** window, from the left menu, click on the
    **Access control(IAM).**

    ![](./media/image14.png)

2.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

     ![](./media/image15.png)

3.  In **Privileged administrator** **role,** type the **contributor**
    in the search box and select it. Click **Next**

      ![](./media/image16.png)

4.  In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

      ![](./media/image17.png)

5.  On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

     ![](./media/image18.png)

6.  In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

      ![](./media/image19.png)

      ![](./media/image20.png)

7.  In your **Copilot-AzureAI** window, from the left menu, click on the
    **Access control(IAM).**

      ![](./media/image14.png)

8.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

     ![](./media/image15.png)

9.  Type the **Azure AI Developer** in the search box and select it.
    Click **Next**

     ![](./media/image21.png)

10. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

     ![](./media/image22.png)

11. On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

     ![](./media/image23.png)

12. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

     ![](./media/image24.png)

     ![](./media/image25.png)

13. You will see a notification – added as Azure AI Developer for
    Azure-openai-testXX

     ![](./media/image26.png)

## **Task 3: Create an Azure AI Search service in the portal**

1.  In Azure portal home page, click on **+ Create Resource**.

      ![](./media/image27.png)

2.  In the **Create a resource** page search bar, type **Azure AI
    Search** and click on the appeared **azure ai search**.

      ![](./media/image28.png)

3.  Click on **azure ai search** section.

      ![](./media/image29.png)
4.  In the **Azure AI Search** page, click on the **Create** button.

      ![](./media/image30.png)

5.  On the **Create a search service** page, provide the following
    information and click on **Review+create** button.
    |  |  |
    |----|----|
    |Field	|Description|
    |Subscription|	Select your Azure OpenAI subscription|
    |Resource group|	Select your Resource group(that you have created in Task 1)|
    |Region|	East US|
    |Name|	+++mysearchserviceXX+++  (XXcan be unique number)|
    |Pricing Tier|	Click on change Price Tire>select Basic|

     ![](./media/image31.png)
     ![](./media/image32.png)
     ![](./media/image33.png)

6.  Once the Validation is passed, click on the **Create** button.

      ![](./media/image34.png)
      ![](./media/35.png)

7.  After the deployment is completed, click on the **Go to resource**
    button.

      ![](./media/image36.png)

8.  In the **mysearchserviceXX** Overview page. In the left-side
    navigation pane, under **Settings** section, select **Semantic
    ranker**.

      ![](./media/image37.png)

9.  On the **Semantic ranker** tab, select **Free** tile and click
    on the **Select plan.**

      ![](./media/image38.png)

10. You will see a notification -**Successfully updated semantic ranker
    to free plan**

      ![](./media/image39.png)

# Exercise-2: Add your data using Azure OpenAI Studio

## **Task 1: Create an Azure AI project in Azure AI Studio**

Your Azure AI project is used to organize your work and save state while
building your copilot. During this tutorial, your project contains your
data, prompt flow runtime, evaluations, and other resources.

1.  On the **copilot-AzureAIXXX** window, click on **Overview** in the
    left navigation menu, then under the **Govern the environment for
    your team in AI Studio** tab, click on the **Launch** **Azure AI
    Studio** button to open **Azure AI Studio** in a new browser.

     ![](./media/image40.png)
     ![](./media/image41.png)

2.  In the **Azure AI Studio** window, click on **+ New project** from
    under the **Project.**

      ![](./media/image42.png)

3.  In the **Create a project** tab, under **Project name**, enter the
    Project name as +++**contoso-outdoor-proj+++** and then click on
    **Create a project** button.

      ![](./media/image43.png)

4.  Wait for the deployment to complete. The deployment will take around
    1-2 minutes.

     ![](./media/image44.png)

## Task 2: Azure AI Search service connection

1.  In the **Azure AI Studio** window, click on **Settings** under
    Project overview and select +**New connection** from the **Connected
    resources** section.

     ![](./media/image45.png)

2.  In **Add a connection to external assets** page , select **Azure AI
    Search.**

     ![](./media/image46.png)

3.  In Connect an Azure AI Search resource page, select ai search
    (you’ve created in Exercise 1\>Task 3) and click on **Add
    connection**

     ![](./media/image47.png)
4.  After the service is connected, select **Close** to return to
    the **Settings** page.

    ![](./media/image48.png)

## **Task 3: Create a compute instance**

To create a compute instance in Azure AI Studio:

1.  In the Azure AI Studio page, select **Settings** from the left menu
    and select **View all** under the **Compute** session.

      ![](./media/image49.png)

2.  In the **Azure AI Studio** page, under the **Compute instance** tab
    select **+New**.

     ![](./media/image50.png)

3.  In **Create compute instance** pane, enter the following details and
    click on **Next** button.

    |   |  |
    |----|----|
    |Compute name|	copilotcomputeXX(XX can be a unique number)|
    |Virtual machine type|	CPU|
    |Virtual machine size	|Select from recommended options                                                                                                         •	Standard_E4ds_v44 cores, 32GB RAM, 150GB storage|

      ![](./media/image51.png)

4.  In **Scheduling** pane, click on **Add schedule** and leave all the
    fields in the default state. Then click **Next** button.
        ![](./media/image52.png)
         ![](./media/image53.png)

5.  In **Security** pane, leave all the fields in the default state then
    click **Next** button.

      ![](./media/image54.png)

6.  In **Tags** pane, leave all the fields in the default state then
    click **Next** button.

      ![](./media/image55.png)

7.  In **Review** pane, review the details that you’ve entered, and
    click on **Create** button**.**

     ![](./media/image56.png)

8.  To create the compute instance will take 5-6 minutes

     ![](./media/image57.png)
     ![](./media/image58.png)

## **Task 4: Deploy a chat model**

Follow these steps to deploy an Azure OpenAI chat model for your
copilot.

1.  On the Azure AI Studio **Home** page. select **Model catalog** under
    the **Get started**.

      ![](./media/image59.png)

2.  In the **Collections** filter, select **Azure OpenAI**.

      ![](./media/image60.png)

3.  Select a model such as **gpt-4** from the Azure OpenAI collection.

      ![](./media/image61.png)

4.  Select **Deploy** to open the deployment window.

      ![](./media/image62.png)

5.  In the **Deploy model** dialog box, under the **Deployment name**
    field, enter **gpt-4, select the Model version** as **1106-Preview**
    and click on **Deploy** button.

      ![](./media/image63.png)

6.  You see the deployment details page. Details include the date you
    created the deployment and the created date and version of the model
    you deployed.

      ![](./media/image64.png)

7.  On the deployment details page from the previous step, select **Open
    in playground**.

      ![](./media/image65.png)

## **Task 5: Chat in the playground without your data**

In the Azure AI Studio playground you can observe how your model
responds with and without your data. In this section, you test your
model without your data. In the next section, you add your data to the
model to help it better answer questions about your products.

1.  In the playground, select your deployed **gpt-4** chat model from
    the **Deployment** dropdown.

      ![](./media/image66.png)

2.  In the **System message** text box on the **Assistant setup** pane,
    provide this prompt to guide the assistant: **You're an AI assistant
    that helps people find information**. 

     ![](./media/image67.png)

3.  Select **Apply changes** to save your changes.

      ![](./media/image68.png)

4.  In the **Update system message?** dialog box, click on the
    **Continue button.**

       ![](./media/image69.png)

5.  In the chat session pane, enter the following question: **How much
    do the TrailWalker hiking shoes cost**, and then select the right
    arrow icon to send.

      ![](./media/image70.png)

6.  The assistant replies that it doesn't know the answer. The model
    doesn't have access to product information about the TrailWalker
    hiking shoes.

     ![](./media/image71.png)

> In the task, you'll add your data to the model to help it answer
> questions about your products.

## **Task 6: Add your data using chat model** 

You upload your local data files to Azure Blob storage and create an
Azure AI Search index. Your data source is used to help ground the model
with specific data. Grounding means that the model uses your data to
help it understand the context of your question. You're not changing the
deployed model itself. Your data is stored separately and securely in
your Azure subscription.

1.  In the Azure AI Studio playground, select **Chat** from the Project
    playground left menu.

      ![](./media/image72.png)

2.  On the **Chat playground** pane, select **Add your data**  \> **+
    Add a new data source**.

     ![](./media/image73.png)

3.  In the **Add your data** page that appears, select **Upload
    files/folders** from the **Select data source** dropdown.

      ![](./media/image74.png)

4.  In the **Select your data** pane, click on **Upload folder** and
    navigate to **C:\Labfiles** location and select **1-customer-info**
    and **3-product-info,** then click on **Upload** button.

      ![](./media/image75.png)
 
      ![](./media/image76.png)

5.  If you see a dialog box – Upload 20 files to this site?, click on
    Upload button.

      ![](./media/image77.png)
 
      ![](./media/image78.png)

6.  In the **Select your data** pane, click on **Next** button.

     ![](./media/image79.png)

7.  In **Index storage** pane , under **Select Azure AI Search** service
    select **AI search service** (you’ve created in Exercise 1\>Task 4)
    and enter **product-info** for the Index name

      ![](./media/image80.png)

8.  **Vector settings** type should be selected by default and click on
    the **Next** button.

      ![](./media/image81.png)

9.  Review the details you entered, and select **Create**.

      ![](./media/image82.png)

10. The data will be added in your Chat Playground. This will take
    approximately 10-15 minutes.

     ![](./media/image83.png)
 
     ![](./media/image84.png)
 
     ![](./media/image85.png)
 
     ![](./media/image86.png)

11. In the **Chat session** section, enter the following prompt in the
    **User message** text box and click on the **Send** icon

 +++How much do the TrailWalker hiking shoes cost+++
     ![](./media/image87.png)

12. You can expand the **references** button to see the data that was
    used.

      ![](./media/image88.png)

## **Task 7: Create a prompt flow from the playground**

1.  Select **Prompt flow** from the menu above the **Chat
    playground** pane.

    ![](./media/image89.png)

2.  Enter a folder name for your prompt flow as +++**Contoso outdoor
    flow+++** . Then select **Open**. Azure AI Studio exports the
    playground chat environment including connections to your data to
    prompt flow.

     ![](./media/image90.png)
 
     ![](./media/image91.png)

- **Save** button: You can save your prompt flow at any time by
  selecting **Save** from the top menu. Be sure to save your prompt flow
  periodically as you make changes in this tutorial.

- **Start compute session** button: You need to start a compute session
  to run your prompt flow. You can start the session later in the
  tutorial. You incur costs for compute instances while they are running

     ![](./media/image92.png)

- To facilitate node configuration and fine-tuning, a visual
  representation of the workflow structure is provided through a DAG
  (Directed Acyclic Graph) graph. This graph showcases the connectivity
  and dependencies between nodes, providing a clear overview of the
  entire workflow. The nodes in the graph shown here are representative
  of the playground chat experience that you exported to prompt flow.

     ![](./media/image93.png)

# Exercise 3: Customize prompt flow with multiple data sources

Earlier in the [Azure AI Studio](https://ai.azure.com/) playground,
you [added your
data](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-copilot-ai-studio#add-your-data-and-try-the-chat-model-again) to
create one search index that contained product data for the Contoso
copilot. So far, users can only inquire about products with questions
such as "How much do the TrailWalker hiking shoes cost?". But they can't
get answers to questions such as "How many TrailWalker hiking shoes did
Daniel Wilson buy?" To enable this scenario, we add another index with
customer information to the flow.

## **Task 1: Create the customer info index**

1.  In the Azure AI Studio playground, select **Indexes** from the
    collapsible left menu.

     ![](./media/image94.png)

2.  In the **Create indexes to customize generative AI responses** tab,
    select **+New index**

      ![](./media/image95.png)

3.  You're taken to the **Create an index** wizard.

      ![](./media/image96.png)

4.  On the Source data page, select **Upload files/folders** from
    the **Upload** dropdown. Select the customer info files that you
    downloaded or created earlier.

      ![](./media/image97.png)
 
      ![](./media/image98.png)

5.  Navigate to **C:\Labfiles** location and select **1-customer-info**
    and **3-product-info,** then click on **Upload** button.

      ![](./media/image99.png)
 
      ![](./media/image100.png)

6.  If you see a dialog box – Upload 20 files to this site?, click on
    Upload button

     ![](./media/image101.png)

7.  Select **Next** at the bottom of the page.

     ![](./media/image102.png)

8.  Select the same Azure AI Search resource (that you have created in
    **Ex 1\>** **Task 4**), enter +++**customer-info+++** for the index
    name and select virtual machine as **Auto select**. Then
    select **Next**.

      ![](./media/image103.png)

9.  **Vector settings** type should be selected by default.

10. Select ***Default_AzureOpenAI*** from the **Azure OpenAI
    resource** dropdown. Select the checkbox to acknowledge that an
    Azure OpenAI embedding model will be deployed if it's not already.
    Then select **Next**.

      ![](./media/image104.png)

** Note:** The embedding model is listed with other model deployments in
    the Deployments page.

11. Review the details you entered, and select **Create**.

     ![](./media/image105.png)

     ![](./media/image106.png)

** Note:** You use the *customer-info* index and
the *mysearchserviceXX* Azure AI Search resource in prompt flow later in
this tutorial. If the names you enter differ from what's specified here,
make sure to use the names you entered in the rest of the lab.

12. You're taken to the index details page where you can see the status
    of your index creation , it will take around 20-23 minutes .

     ![](./media/image107.png)

     ![](./media/image108.png)

## **Task 2: Add customer information to the flow**

Afte you're done creating your index, return to your prompt flow and
follow these steps to add the customer info to the flow:

1.  On the Azure AI Studio **Home** page, select **Prompt flow** under
    the Tools.

     ![](./media/image109.png)

2.  On the Flows pane, select **contoso outdoor flow.**

     ![](./media/image110.png)

3.  Select **Start compute session** from the top menu.

     ![](./media/image111.png)

4.  It will take 1-3 minutes to **start compute session**

     ![](./media/image112.png)

5.  Make sure you have a compute session running. 

     ![](./media/image113.png)

6.  Select **+ More tools** from the top menu and then select **Index
    Lookup** from the list of tools.

     ![](./media/image114.png)

7.  Name the new node +++queryCustomerIndex+++ and select **Add**.

     ![](./media/image115.png)

8.  Select the **mlindex_content** textbox in
    the **queryCustomerIndex** node.

      ![](./media/image116.png)

9.  The **Generate** dialog opens. You use this dialog to configure
    the **queryCustomerIndex** node to connect to
    your *customer-info* index.

10. In the **Generate** dialog, for the **index_type** value,
    select **Azure AI Search**.

     ![](./media/image117.png)

11. In the **Generate** dialog, Select or enter the following values and
    Select **Save** to save the settings.

    |Name	|Value|
    |---|---|
    |acs_index_connection|	The name of your Azure AI Search service connection (such as mysearchserviceXX)|
    |acs_index_name|	customer-info|
    |acs_content_field|	content|
    |acs_metadata_field	|meta_json_string|
    |semantic_configuration	|azuremldefault|
    |embedding_type	|None|

     ![](./media/image118.png)

12. Select or enter the following values for
    the **queryCustomerIndex** node

    |  |  |
    |---|---|
    |Name	|Value|
    |queries	|${extractSearchIntent.output}|
    |query_type|	Keyword|
    |top	|5|

13. You can see the **queryCustomerIndex node** is connected to the
    **extractSearchIntent** node in the graph

      ![](./media/image119.png)

14. Select **Save** from the top menu to save your changes. Remember to
    save your prompt flow periodically as you make changes.

      ![](./media/image120.png)
 
      ![](./media/image121.png)

## **Task 3: Connect the customer info to the flow**

In the next section, you aggregate the product and customer info to
output it in a format that the large language model can use. But first,
you need to connect the customer info to the flow.

1.  Select the ellipses icon next to **+ More tools** and then
    select **Raw file mode** to switch to raw file mode. This mode
    allows you to copy and paste nodes in the graph.

     ![](./media/image122.png)
 
     ![](./media/image123.png)
 
       ![](./media/image124.png)

2.  Replace all instances
    of **querySearchResource** with **queryProductIndex** in the graph.
    We're renaming the node to better reflect that it retrieves product
    info and contrasts with the **queryCustomerIndex** node that you
    added to the flow.

      ![](./media/image125.png)
 
      ![](./media/image126.png)
 
       ![](./media/image127.png)
 
       ![](./media/image128.png)

3.  Rename and replace all instances
    of **chunkDocuments** with **chunkProductDocuments** in the graph.

      ![](./media/image129.png)
 
     ![](./media/image130.png)

4.  Rename and replace all instances
    of **selectChunks** with **selectProductChunks** in the graph.

      ![](./media/image131.png)
 
      ![](./media/image132.png)

5.  Copy and paste
    the **chunkProductDocuments** and **selectProductChunks** nodes to
    create similar nodes for the customer info. Rename the new
    nodes **chunkCustomerDocuments** and **selectCustomerChunks** respectively.Simllarly
    like below code
    ```
    - name: chunkCustomerDocuments
      type: python
      source:
        type: code
        path: chunkProductDocuments.py
      inputs:
        data_source: Azure AI Search
        max_tokens: 1050
        queries: ${extractSearchIntent.output}
        query_type: Hybrid (vector + keyword)
        results: ${queryCustomerIndex.output}
        top_k: 5
      use_variants: false
    - name: selectCustomerChunks
      type: python
      source:
        type: code
        path: filterChunks.py
      inputs:
        min_score: 0.3
        results: ${chunkCustomerDocuments.output}
        top_k: 5
      use_variants: false
    ```
   ![](./media/image133.png)

14. Within the **chunkCustomerDocuments** node, replace
    the **${queryProductIndex.output}** input
    with **${queryCustomerIndex.output}**.

     ![](./media/image134.png)

15. Within the **selectCustomerChunks** node, replace
    the **${chunkProductDocuments.output}** input
    with **${chunkCustomerDocuments.output}.**

     ![](./media/image135.png)

16. Select **Save** from the top menu to save your changes.

     ![](./media/image136.png)
 
   By now, the **flow.dag.yaml** file should include nodes (among others)
   that look similar to the following:

    ```
    id: template_chat_flow
    name: Template Chat Flow
    inputs:
      chat_history:
        type: list
        default: []
        is_chat_input: false
        is_chat_history: true
      query:
        type: string
        default: ""
        is_chat_input: true
    outputs:
      reply:
        type: string
        reference: ${generateReply.output}
        is_chat_output: true
      documents:
        type: string
        reference: ${aggregateChunks.output}
        is_chat_output: false
    nodes:
    - name: formatRewriteIntentInputs
      type: python
      source:
        type: code
        path: formatConversationForIntentRewriting.py
      inputs:
        history: ${inputs.chat_history}
        max_tokens: 2000
        query: ${inputs.query}
      use_variants: false
    - name: rewriteIntent
      type: llm
      source:
        type: code
        path: ragcore/prompt_templates/rewriteIntent.jinja2
      inputs:
        deployment_name: gpt-4
        temperature: 0.7
        top_p: 0.95
        max_tokens: 120
        presence_penalty: 0
        frequency_penalty: 0
        conversation: ${formatRewriteIntentInputs.output}
      provider: AzureOpenAI
      connection: copilotazureai3640805165_aoai
      api: chat
      module: promptflow.tools.aoai
      use_variants: false
    - name: extractSearchIntent
      type: python
      source:
        type: code
        path: extractSearchIntent.py
      inputs:
        intent: ${rewriteIntent.output}
      use_variants: false
    - name: queryProductIndex
      type: python
      source:
        type: package
        tool: promptflow_vectordb.tool.common_index_lookup.search
      inputs:
        mlindex_content: >
          embeddings:
            api_base: https://copilotazureai3640805165.openai.azure.com
            api_type: Azure
            api_version: 2023-07-01-preview
            batch_size: '16'
            connection:
              id: >-
                /subscriptions/2ad97659-df19-4123-ab60-775764ea635a/resourceGroups/AOAI-RG351/providers/Microsoft.MachineLearningServices/workspaces/contoso-outdoor-proj/connections/copilotazureai3640805165_aoai
            connection_type: workspace_connection
            deployment: text-embedding-ada-002
            dimension: 1536
            file_format_version: '2'
            kind: open_ai
            model: text-embedding-ada-002
            schema_version: '2'
          index:
            api_version: 2023-07-01-preview
            connection:
              id: >-
                /subscriptions/2ad97659-df19-4123-ab60-775764ea635a/resourceGroups/AOAI-RG351/providers/Microsoft.MachineLearningServices/workspaces/contoso-outdoor-proj/connections/mysearchservice345
            connection_type: workspace_connection
            endpoint: https://mysearchservice345.search.windows.net/
            engine: azure-sdk
            field_mapping:
              content: content
              embedding: contentVector
              filename: filepath
              metadata: meta_json_string
              title: title
              url: url
            index: product-info
            kind: acs
            semantic_configuration_name: azureml-default
        queries: ${extractSearchIntent.output}
        query_type: Hybrid (vector + keyword)
        top_k: 5
      use_variants: false
    - name: chunkCustomerDocuments
      type: python
      source:
        type: code
        path: chunkProductDocuments.py
      inputs:
        data_source: Azure AI Search
        max_tokens: 1050
        queries: ${extractSearchIntent.output}
        query_type: Hybrid (vector + keyword)
        results: ${queryCustomerIndex.output}
        top_k: 5
      use_variants: false
    - name: selectCustomerChunks
      type: python
      source:
        type: code
        path: filterChunks.py
      inputs:
        min_score: 0.3
        results: ${chunkCustomerDocuments.output}
        top_k: 5
      use_variants: false
    - name: chunkProductDocuments
      type: python
      source:
        type: code
        path: chunkProductDocuments.py
      inputs:
        data_source: Azure AI Search
        max_tokens: 1050
        queries: ${extractSearchIntent.output}
        query_type: Hybrid (vector + keyword)
        results: ${queryProductIndex.output}
        top_k: 5
      use_variants: false
    - name: selectProductChunks
      type: python
      source:
        type: code
        path: filterChunks.py
      inputs:
        min_score: 0.3
        results: ${chunkProductDocuments.output}
        top_k: 5
      use_variants: false
    - name: shouldGenerateReply
      type: python
      source:
        type: code
        path: shouldGenerateReply.py
      inputs:
        chunks: ${aggregateChunks.output}
        queries: ${extractSearchIntent.output}
      use_variants: false
    - name: formatGenerateReplyInputs
      type: python
      source:
        type: code
        path: formatReplyInputs.py
      inputs:
        chunks: ${aggregateChunks.output}
        history: ${inputs.chat_history}
        max_conversation_tokens: 2000
        max_tokens: 5000
        query: ${inputs.query}
      use_variants: false
    - name: generateReply
      type: llm
      source:
        type: code
        path: ragcore/prompt_templates/generateReply.jinja2
      inputs:
        inputs: ${formatGenerateReplyInputs.output}
        deployment_name: gpt-4
        temperature: 0.7
        top_p: 0.95
        max_tokens: 800
        presence_penalty: 0
        frequency_penalty: 0
        indomain: "True"
        role_info: You are an AI assistant that helps people find information.
      provider: AzureOpenAI
      connection: copilotazureai3640805165_aoai
      api: chat
      module: promptflow.tools.aoai
      activate:
        when: ${shouldGenerateReply.output}
        is: true
      use_variants: false
    - name: queryCustomerIndex
      type: python
      source:
        type: package
        tool: promptflow_vectordb.tool.common_index_lookup.search
      inputs:
        mlindex_content: >
          embeddings:
            kind: none
            schema_version: '2'
          index:
            api_version: 2023-07-01-preview
            connection:
              id: /subscriptions/2ad97659-df19-4123-ab60-775764ea635a/resourceGroups/AOAI-RG351/providers/Microsoft.MachineLearningServices/workspaces/contoso-outdoor-proj/connections/mysearchservice345
            connection_type: workspace_connection
            endpoint: https://mysearchservice345.search.windows.net/
            engine: azure-sdk
            field_mapping:
              content: content
              embedding: null
              metadata: meta_json_string
            index: customer-info
            kind: acs
            semantic_configuration_name: azureml-default
        queries: ${extractSearchIntent.output}
        query_type: Keyword
        top_k: 5
      use_variants: false
    - name: aggregateChunks
      type: python
      source:
        type: code
        path: aggregateChunks.py
      inputs:
        input1: ${selectProductChunks.output}
        input2: ${selectCustomerChunks.output}
      use_variants: false
    node_variants: {}
    environment:
      python_requirements_txt: requirements.txt
    ```

**Note**: **flow.dag.yaml** file is available in the C:\Labfiles

## **Task 4: Aggregate product and customer info**

At this point, the prompt flow only uses the product information.

- **extractSearchIntent** extracts the search intent from the user's
  question.

- **queryProductIndex** retrieves the product info from
  the *product-info* index.

- The **LLM** tool (for large language models) receives a formatted
  reply via
  the **chunkProductDocuments** \> **selectProductChunks** \> **formatGeneratedReplyInputs** nodes.

You need to connect and aggregate the product and customer info to
output it in a format that the **LLM** tool can use. Follow these steps
to aggregate the product and customer info:

1.  Switch off the  **Raw file mode** .

     ![](./media/image137.png)

2.  Select **Python** from the list of tools.

     ![](./media/image138.png)

3.  Name the tool **aggregateChunks** and select **Add**.

     ![](./media/image139.png)

4.  Copy and paste the following Python code to replace all contents in
    the **aggregateChunks** code block.
    ```
    from promptflow import tool
    from typing import List
    
    @tool
    def aggregate_chunks(input1: List, input2: List) -> str:
        interleaved_list = []
        for i in range(max(len(input1), len(input2))):
            if i < len(input1):
                interleaved_list.append(input1[i])
            if i < len(input2):
                interleaved_list.append(input2[i])
        return interleaved_list
    ```
     ![](./media/image140.png)

5.  Select the **Validate and parse input** button to validate the
    inputs for the **aggregateChunks** node. If the inputs are valid,
    prompt flow parses the inputs and creates the necessary variables
    for you to use in your code.

     ![](./media/image141.png)

6.  Edit the **aggregateChunks** node to connect the product and
    customer info. Set the **inputs** to the following values:

    |  |  |  |
    |---|---|--|
    |Name	|Type|	Value|
    |input1|	list|	${selectProductChunks.output}|
    |input2	|list	|${selectCustomerChunks.output}|

     ![](./media/image142.png)

7.  Select the **shouldGenerateReply** node from the graph. Select or
    enter **${aggregateChunks.output}** for the **chunks** input.

     ![](./media/image143.png)

8.  Select the **formatGenerateReplyInputs** node from the graph. Select
    or enter **${aggregateChunks.output}** for the **chunks** input.

     ![](./media/image144.png)

9.  Select the **outputs** node from the graph. Select or
    enter **${aggregateChunks.output}** for the **chunks** input.

      ![](./media/image145.png)

10. Select **Save** from the top menu to save your changes. Remember to
    save your prompt flow periodically as you make changes.

     ![](./media/image146.png)

## **Task 5: Chat in prompt flow with product and customer info**

By now you have both the product and customer info in prompt flow. You
can chat with the model in prompt flow and get answers to questions such
as "How many TrailWalker hiking shoes did Daniel Wilson buy?" Before
proceeding to a more formal evaluation, you can optionally chat with the
model to see how it responds to your questions.

1.  Continue from the previous section with the **outputs** node
    selected. Make sure that the **reply** output has the **Chat
    output** radio button selected. Otherwise, the full set of documents
    are returned in response to the question in chat.

     ![](./media/image147.png)

2.  Select **Chat** from the top menu in prompt flow to try chat.

      ![](./media/image148.png)

3.  Enter "**How many TrailWalker hiking shoes did Daniel Wilson buy?**"
    and then select the right arrow icon to send.

      ![](./media/image149.png)

** Note:** It might take a few seconds for the model to respond. You can
expect the response time to be faster when you use a deployed flow

4.  The response is what you expect. The model uses the customer info to
    answer the question.

      ![](./media/image150.png)

# Exercise 4: Evaluate the flow using a question and answer evaluation dataset

## **Task 1: Deploy the flow**

Now that you [built a
flow](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-copilot-ai-studio#create-a-prompt-flow-from-the-playground) and
completed a
metrics-based [evaluation](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-copilot-ai-studio#evaluate-the-flow-using-a-question-and-answer-evaluation-dataset),
it's time to create your online endpoint for real-time inference. That
means you can use the deployed flow to answer questions in real time.

1.  In the Prompt flow pane, select **Deploy** on the flow editor.

     ![](./media/image151.png)

2.  Provide the requested information on the **Basic Settings** page in
    the deployment wizard. Select **Next** to proceed to the advanced
    settings pages.

      ![](./media/image152.png)

3.  On the **Advanced settings - Endpoint** page, leave the default
    settings and select **Next**.

      ![](./media/image153.png)

4.  On the **Advanced settings - Deployment** page, leave the default
    settings and select **Next**.

     ![](./media/image154.png)

5.  On the **Advanced settings - Outputs & connections** page, make sure
    all outputs are selected under **Included in endpoint response**.

6.  Select **Review + Create** to review the settings and create the
    deployment.

      ![](./media/image155.png)

7.  Select **Create** to deploy the prompt flow.

      ![](./media/image156.png)

## **Task 2: Use the deployed flow**

Your copilot application can use the deployed prompt flow to answer
questions in real time. You can use the REST endpoint or the SDK to use
the deployed flow.

1.  To view the status of your deployment AI studio,
    select **Deployments** from the left navigation.

    ![](./media/image157.png)
 
    ![](./media/image158.png)

2.  Select the contoso-outdoor-proj deployment. If you see a message
    that says "Currently this endpoint has no deployments" or the State
    is still Updating, you might need to select Refresh after a couple
    of minutes to see the deployment.

     ![](./media/image158.png)
 
     ![](./media/image159.png)
 
     ![](./media/image160.png)

## **Task 3: Create an evaluation**

1.  In the Azure AI Studio page, select **Prompt flow** from the left
    menu

     ![](./media/image161.png)

2.  Select the **Contoso outdoor flow** prompt flow

     ![](./media/image162.png)

3.  Select **Evaluate** \> **Built-in evaluation** from the top menu in
    prompt flow.

      ![](./media/image163.png)

4.  In the **Create a new evaluation** wizard, enter a name for your
    evaluation i.e **evaluate_from_flow**.

5.  Select **Question and answer without context** from the scenario
    options.

6.  Select the flow to evaluate. In this example, select **Contoso
    outdoor flow** or whatever you named your flow. Then
    select **Next**.

      ![](./media/image164.png)

7.  Select **Add your dataset** on the **Configure test data** page.
    Click on **Upload file**.

      ![](./media/image165.png)

8.  Navigate to **C:\Labfiles** location and select
    **qa-evaluation.jsonl** ,then click on **Open** button.

     ![](./media/image166.png)

9.  After the file is uploaded, you need to configure your data columns
    to match the required inputs for prompt flow to execute a batch run
    that generate output for evaluation. Enter or select the following
    values for each data set mapping for prompt flow.

10. Select **Next**.
    
    |   |  |
    |-----|----|
    |Name|	Description	Type	Data source|
    |chat_history|	The chat history	list	${data.chat_history}|
    |query	|The query	string	${data.question}|

     ![](./media/image167.png)

11. Select the metrics you want to use to evaluate your flow. In this
    example, select Coherence, Fluency, GPT similarity, and F1 score.

12. Select a connection and model to use for evaluation. In this
    example, select **gpt-4**. Then select **Next**.

      ![](./media/image168.png)

**Note:** Evaluation with AI-assisted metrics needs to call another GPT
model to do the calculation. For best performance, use a model that
supports at least 16k tokens such as gpt-4-32k or gpt-35-turbo-16k
model. If you didn't previously deploy such a model, you can deploy
another model by following the steps in [**the AI Studio chat playground
quickstart**](https://learn.microsoft.com/en-us/azure/ai-studio/quickstarts/get-started-playground#deploy-a-chat-model).
Then return to this step and select the model you deployed.

13. You need to configure your data columns to match the required inputs
    to generate evaluation metrics. Enter the following values to map
    the dataset to the evaluation properties and click on **Next**
    button.

    |  |  |  |   |
    |---|---|---|----|
    |Name|	Description|	Type|	Data source|
    |question	|A query seeking specific information.	|string	|${data.question}|
    |answer	|The response to question generated by the model as answer.|	string|	${run.outputs.reply}|
    |documents|	String with context from retrieved documents.|	string|	${run.outputs.documents}|

     ![](./media/image169.png)

14. Review the evaluation details and then select **Submit**. You're
    taken to the **Metric evaluations** page.

     ![](./media/image170.png)

## **Task 4: View the evaluation status and results**

1.  After you, if you aren't there already go to the **Evaluation**. On
    the **Metric evaluations** page, you can see the evaluation status
    and the metrics that you selected. You might need to
    select **Refresh** after a couple of minutes to see
    the **Completed** status.

     ![](./media/image171.png)
  
     ![](./media/image172.png)
 
     ![](./media/image173.png)

2.  Select your Evaluation flow

     ![](./media/image173.png)
 
      ![](./media/image174.png)
 
     ![](./media/image175.png)

**Tip:** Once the evaluation is in **Completed** status, you don't need
a compute session to complete the rest of this tutorial. You can stop
your compute instance to avoid incurring unnecessary Azure costs. For
more information, see [**how to start and stop
compute**](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/create-manage-compute#start-or-stop-a-compute-instance).

## Task 5: Clean up resources

To avoid incurring unnecessary Azure costs, you should delete the
resources you created in this quickstart if they're no longer needed. To
manage resources, you can use the [Azure
portal](https://portal.azure.com/?azure-portal=true).

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

     ![](./media/image176.png)

2.  Click on the assigned resource group.

     ![](./media/image177.png)

3.  Carefully select all resources except Azure Open AI service (that
    you have created in **Lab 1**).

**Note**: Don’t select Azure OpenAI service.

4.  In the Resource group page, navigate to the command bar and click on
    **Delete**.

**Important Note**: Don’t click on **Delete resource group**. If you
don’t see the **Delete** option in the command bar, then click on the
horizontal ellipsis.
     ![](./media/image178.png)

5.  In the **Delete Resources** pane that appears on the right side,
    enter the **delete** and click on **Delete** button.

     ![](./media/image179.png)

6.  On **Delete confirmation** dialog box, click on D**elete** button.

     ![](./media/image180.png)

7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 4 selected items.**

**Summary:**

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
