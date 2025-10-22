## Use case 09-Exploring Azure OpenAI Assistants with Bing Search Integration and Multi-Agent Framework

# **Introduction**

Azure OpenAI Assistants (Preview) allows you to create AI assistants
tailored to your needs through custom instructions and augmented by
advanced tools like code interpreter, and custom functions.

This lab focuses on setting up and utilizing Azure OpenAI services
alongside Bing Search integration to build sophisticated AI assistants
and multi-agent frameworks. You’ll deploy AI models, explore assistant
functionalities, and implement multi-agent interactions for complex task
processing.

**Objective**

- To create a Bing Search Service resource in Azure.

- To deploy Azure OpenAI resources and configure them.

- To deploy specific Azure OpenAI models like GPT-4, GPT-4 Vision, and
  DALL-E-3.

- To explore and prototype AI assistants using Azure OpenAI Studio.

- To implement function calling with Bing Search APIs for enhancing
  assistant capabilities.

- To build a multimodal multi-agent framework using Azure Assistant API
  for collaborative AI tasks.

- To delete the deployed resources and models.

## **Task 1: Create a Bing Search Service resource**

1.  Click on the **Portal Menu**, then select **+ Create a resource**

> ![A screenshot of a computer Description automatically
> generated](./media/image1.png)

2.  In the **Create a resource** page search bar, type **Bing Search
    v7** and click on the appeared **bing search v7**.

![A screenshot of a computer Description automatically
generated](./media/image2.png)

3.  Click on **Bing Search v7** section.

![](./media/image3.png)

4.  On the **Create a search service** page, provide the following
    information and click on **Review+create** button.

      |Field	|Description|
      |----|---|
      |Subscription|	Select the subscription assigned to|
      |Resource group|Click on Create new> enter +++AOAI-RGXXX+++(XXX can be a unique number)|
      |Resource group location|	West US|
      |Name	|+++bingsearchaoaiXX+++(XXcan be unique number)|
      |Pricing Tier	|F1|
      |Select the check box	|I confirm I have read and understood the notice above|

![](./media/image4.png)

![](./media/image5.png)

5.  Once the Validation is passed, click on the **Create** button.

![](./media/image6.png)

6.  Once the deployment is completed, click on **Go to resource**
    button.

![](./media/image7.png)

7.  On the **bingsearchaoaiXX** window, navigate to **Resource
    management** section, and click on **Keys and Endpoint**.

![A screenshot of a computer Description automatically
generated](./media/image8.png)

8.  In **Keys and Endpoints** page, copy **KEY1** (*You can use
    either KEY1 or KEY2)* and **Endpoint** and paste them in a notepad
    (as shown in the image), and then **Save** the notepad to use the
    information in the upcoming tasks.

![A screenshot of a computer Description automatically
generated](./media/image9.png)

## **Task 2: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

> ![A screenshot of a computer Description automatically
> generated](./media/image10.png)

2.  Navigate and click on **+ Create a resource**.

> ![](./media/image11.png)

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

> ![](./media/image12.png)

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

> ![A screenshot of a computer Description automatically
> generated](./media/image13.png)

[TABLE]

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

> ![](./media/image14.png)

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image15.png)

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image16.png)

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> ![](./media/image17.png)

9.  Wait for the deployment to complete. The deployment will take around
    **2-3** minutes.

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

> ![](./media/image18.png)

11. Click on **Keys and Endpoints** from the left navigation menu and
    then copy the endpoint value in a notepad to **AzureAI ENDPOINT**
    and key to a variable **AzureAIKey**.

> ![](./media/image19.png)

## Task 3: Deploying an Azure OpenAI models

1.  On the **AzureOpenAI-AssistantsXX** window, click on **Overview** in
    the left navigation menu, click on the **Explore Azure AI Foundry
    portal** button to open **Azure AI Foundry Studio** in a new browser

> ![](./media/image20.png)

2.  In the **Azure AI Foundary | Azure OpenAI Service** window, select
    **Deployment** from the left navigation menu**.**

> ![](./media/image21.png)

12. In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

> ![](./media/image22.png)

13. In the **Select a model** dialog box, navigate and carefully select
    **gpt-4**, then click on **Confirm** button.

> ![](./media/image23.png)

3.  In the **Deploy model dialog** box, enter the following details and
    click on the **Create** button.

- Select Model: **gpt-4**

- Model Version**: 1106-Preview**

- Deployment Name: enter **gpt-4**

- Select the **Advanced options** and select the **Standard** as
  **Deployment type**

![](./media/image24.png)

![](./media/image25.png)

> ![A screenshot of a computer Description automatically
> generated](./media/image26.png)

4.  In the **Deployments** page, click on +**Create new deployment**.

5.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

> ![](./media/image22.png)

14. In the **Select a model** dialog box, navigate and carefully select
    **gpt-4**, then click on **Confirm** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image23.png)

6.  In the **Deploy model** dialog box, under **Select a model** click
    on the dropdown select **gpt-4** field, under **Model version**
    select **vision-preview** and under **Deployment name** enter
    +++**gpt-4-vision+++.** Click on the **Create** button.

> ![](./media/image27.png)
>
> ![](./media/image28.png)

![A screenshot of a computer Description automatically
generated](./media/image29.png)

7.  In the **Deployments** window, drop down the **+Deploy model** and
    select **Deploy base model.**

> ![](./media/image22.png)

15. In the **Select a model** dialog box, navigate and carefully select
    **dall-e-3**, then click on **Confirm** button.

> ![](./media/image30.png)

8.  In the **Deploy model** dialog box, under **Select a model** click
    on the dropdown select **dall-e-3** field, under **Model version**
    select **Auto-update to default** and under **Deployment name**
    enter !!**dall-e-3**!!**.** Click on the **Create** button.

> ![](./media/image31.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image32.png)

## Task 4: Explore the Assistant's playground

1.  In Azure AI Foundry |Azure OpenAI Service Home page, under
    **Playgrounds** section, click on the **Assistants playground**.

![](./media/image33.png)

2.  In the **Assistants playground** pane, select **+Create an
    assistant**.

![](./media/image34.png)

3.  The Assistants playground allows you to explore, prototype, and test
    AI Assistants without needing to run any code. From this page, you
    can quickly iterate and experiment with new ideas.

![A screenshot of a computer Description automatically
generated](./media/image35.png)

4.  From the Assistant setup pane enter the below details

- Assistant a name: +++**Math Assist+++**

- Instructions: Enter the following instructions +++**You are an AI
  assistant that can write code to help answer math questions+++**

- Deployment: **gpt-4**

- Select the toggle **enabling code interpreter**

> ![](./media/image36.png)
>
> ![](./media/image37.png)

5.  From the Assistant setup pane, select the **Select assistant**

![](./media/image38.png)

6.  In the Select an assistant tab select **Math Assist** and click on
    **Select** button.

![](./media/image39.png)

7.  Enter a question for the assistant to answer: +++**I need to solve
    the equation 3x + 11 = 14. Can you help me?**+++

8.  Select the R**un button** .

> ![](./media/image40.png)

While we can see that answer is correct, to confirm that the model used
code interpreter to get to this answer, and that the code it wrote is
valid rather than just repeating an answer from the model's training
data we'll ask another question.

9.  Enter the follow-up question: +++**Show me the code you ran to get
    this solution.+++** Select the **Add and run button** 

![](./media/image41.png)

![](./media/image42.png)

You could also consult the logs in the right-hand panel to confirm that
code interpreter was used and to validate the code that was run to
generate the response. It is important to remember that while code
interpreter gives the model the capability to respond to more complex
math questions by converting the questions into code and running in a
sandboxed Python environment, you still need to validate the response to
confirm that the model correctly translated your question into a valid
representation in code.

## Task 5: Assistants function calling with Bing Search

In this notebook, we'll show how you can use the Bing Search APIs and
function calling to ground Azure OpenAI models on data from the web.
This is a great way to give the model access to up to date data from the
web.

This sample will be useful to developers and for data scientists who
want to learn about function calling capabilities and search based
grounding.

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> ![](./media/image43.png)

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open Folder**.

> ![A screenshot of a computer Description automatically
> generated](./media/image44.png)

3.  Navigate and select **Assistants** folder from **C:\LabFiles** and
    click on the **Select Folder** button.

![](./media/image45.png)

4.  If you see a dialog box - **Do you trust the authors of the files in
    this folder?**, then click on **Yes, I trust the author**.

![A screenshot of a computer Description automatically generated with
medium confidence](./media/image46.png)

5.  In Visual Studio Code dropdown the **ASSISTANTS**, under
    **function_calling** navigate and click on
    **assistants_function_calling_with_bing_search.ipynb** notebook.

![](./media/image47.png)

6.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1^(st) cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

![](./media/image48.png)

![A screenshot of a computer Description automatically
generated](./media/image49.png)

7.  If prompted to select the path, then select the **Python version
    3.12.2(or later version)** path as shown in the image.

![](./media/image50.png)

8.  Update the parameters ,replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    2), Bing search subscription key** with the values that you have
    saved in your notepad in the **Task 1 .**

![](./media/image51.png)

![A screenshot of a computer program Description automatically
generated](./media/image52.png)

9.  Define a function to call the Bing Search APIs, select 3^(rd),
    4^(th) cells. Then, execute the cell by clicking on the **start
    icon**.

![](./media/image53.png)

![](./media/image54.png)

10. Get things running end to end, select 5^(th) ,6^(th) ,7^(th),8^(th)
    cells. Then, execute the cell by clicking on the **start icon**.

![](./media/image55.png)

![](./media/image56.png)

![](./media/image57.png)

![](./media/image58.png)

![](./media/image59.png)

## **Task 6: Building a multimodal multi-agent framework with Azure Assistant API**

This repo will walk you through the pattern of creating a multi-agent
system using the Azure OpenAI Assistant API.

he example provided in this notebook helps demonstrate how to build a
multi-agent framework with Azure Assistant API and serves as a
comprehensive guide for developers looking to harness the capabilities
of multiple AI agents working in concert. The crux of the article is to
showcase how agents can communicate and collaborate to process complex
tasks, such as generating and enhancing images through multiple
iterations based on user input. This is particularly relevant for
developers and tech enthusiasts who are interested in exploring the
frontiers of generative AI and multi-agent systems.

Before getting started, one should have a basic understanding of AI and
an interest in how agents can work together to enhance AI
functionalities. The article does not delve into in-depth programming;
however, a general knowledge of how APIs operate and the role of AI in
automated systems would be beneficial in grasping the concepts
presented. This example is an invitation to innovators and developers
who wish to experiment with advanced AI systems and potentially
integrate them into various industry solutions.

1.  In Visual Studio Code, under **multi-agent** ,navigate and click on
    **.env** file.

![](./media/image60.png)

2.  In the **.env** file, replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    2), gpt4 deployment name, DALLE3 deployment name and GPT 4 Vision
    deployment name** with the values that you have saved in your
    notepad in the **Task 3**.

![](./media/image61.png)

3.  Click on **File** and the click on **Save**.

![](./media/image62.png)

4.  In Visual Studio Code, under **multi-agent**, navigate and click on
    **multi-agent.ipynb** notebook.

> ![](./media/image63.png)

5.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1^(st) cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

6.  If prompted to select the path, then select the **Python version
    3.12.2(or later version)** path as shown in the image.

> ![A screenshot of a computer Description automatically
> generated](./media/image64.png)

7.  Select 2^(nd) cell. Then, execute the cell by clicking on the
    **start icon**.

![](./media/image65.png)

![](./media/image66.png)

8.  To generating images using a prompt to the Dalle-3 Model. The output
    is a .jpg file stored in the users local directory. Select 3^(rd)
    cell. Then, execute the cell by clicking on the **start icon**.

![](./media/image67.png)

9.  Initializes the agent with the definition described above. Select
    4^(th) cell. Then, execute the cell by clicking on the **start
    icon**.

![](./media/image68.png)

10. Image generator function calls the Dalle-3 image generator given the
    prompt. Select 5^(th) cell. Then, execute the cell by clicking on
    the **start icon**.

![](./media/image69.png)

11. Vision Assistant agent is responsible for analyzing images. The
    output is a new prompt to be used by the image creator agent. Select
    6^(th) cell. Then, execute the cell by clicking on the **start
    icon**.

![](./media/image70.png)

12. Initializes the agent with the definition described above. Select
    7^(th) cell. Then, execute the cell by clicking on the **start
    icon**.

![](./media/image71.png)

13. Vision assistant function calls the GPT4 Vision image analyzes given
    an image, execute the cell by clicking on the **start icon**.

![](./media/image72.png)

14. This agent facilitates the conversation between the user and other
    agents, ensuring successful completion of the task, execute the cell
    by clicking on the **start icon**.

![](./media/image73.png)

15. Initializes the agent with the definition described above, execute
    the cell by clicking on the **start icon**.

![](./media/image74.png)

16. This function calls the Assistant API to generate a main thread of
    communication between the agents listed in the agents_threads,
    execute the cell by clicking on the **start icon**.

![](./media/image75.png)

17. This agent facilitates the conversation between the user and other
    agents, ensuring successful completion of the task. Execute the cell
    by clicking on the **start icon**.

![](./media/image76.png)

![A screenshot of a computer program Description automatically
generated](./media/image77.png)

18. Example Questions, enter the +++Generate an image of a boat drifting
    in the water and analyze it and enhance the image+++. Execute the
    cell by clicking on the **start icon**.

![](./media/image78.png)

![A screenshot of a computer Description automatically
generated](./media/image79.png)

![](./media/image80.png)

## Task 7: Delete the resources

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

> ![A screenshot of a computer Description automatically
> generated](./media/image81.png)

2.  Click on the resource group.

> ![A screenshot of a computer Description automatically
> generated](./media/image82.png)

3.  In the **Resource group** home page, select the resources and click
    on the delete

![](./media/image83.png)

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “Delete” to confirm deletion** field, then click
    on the **Delete** button.

![A screenshot of a computer Description automatically
generated](./media/image84.png)

5.  On **Delete confirmation** dialog box, click on **Delete** button.

> ![A screenshot of a computer error Description automatically
> generated](./media/image85.png)

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

![](./media/image86.png)

**Summary**

This lab provided a hands-on exploration of advanced AI capabilities
using Azure OpenAI and Bing Search integration. You’ve begun by setting
up essential Azure resources and deploying AI models such as GPT-4 and
DALL-E-3. Then, you’ve used Azure OpenAI Studio to create and test AI
assistants capable of handling complex tasks like mathematical
problem-solving and image generation. You’ve integrated Bing Search to
fetch real-time data for grounding AI responses. Additionally, you’ve
learned to build a multi-agent framework, showcasing how different AI
agents can collaborate to enhance task performance. By the end, you’ve
gained practical experience in deploying, testing, and optimizing
AI-driven solutions that prepared you to leverage these technologies in
various real-world applications.
