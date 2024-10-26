# **Lab 06-Exploring Azure OpenAI Assistants with Bing Search Integration and Multi-Agent Framework**

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

      ![](./media/image1.png)

2.  In the **Create a resource** page search bar, type **Bing Search
    v7** and click on the appeared **bing search v7**.

      ![](./media/image2.png)

3.  Click on **Bing Search v7** section.

     ![](./media/image3.png)

4.  On the **Create a search service** page, provide the following
    information and click on **Review+create** button.

    |Field|	Description|
    |---|---|
    |Subscription|	Select the subscription assigned to|
    |Resource group	|Click on Create new> enter AOAI-RGXXX(XXX can be a unique number)|
    |Resource group location|	West US|
    |Name|+++bingsearchaoaiXX+++(XXcan be unique number)|
    |Pricing Tier|	F1|
    |Select the check box	|I confirm I have read and understood the notice above|

    ![](./media/image4.png)
   ![](./media/image5.png)

5.  Once the Validation is passed, click on the **Create** button.

     ![](./media/image6.png)

6.  Once the deployment is completed, click on **Go to resource group**
    button.

      ![](./media/image7.png)

7.  On the **bingsearchaoaiXX** window, navigate to **Resource
    management** section, and click on **Keys and Endpoint**.

      ![](./media/image8.png)

8.  In **Keys and Endpoints** page, copy **KEY1** (*You can use
    either KEY1 or KEY2)* and **Endpoint** and paste them in a notepad
    (as shown in the image), and then **Save** the notepad to use the
    information in the upcoming tasks.

      ![](./media/image9.png)

## **Task 2: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.
     ![](./media/image10.png)

2.  Navigate and click on **+ Create a resource**.
      ![](./media/image11.png)

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

      ![](./media/image12.png)

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

      ![](./media/image13.png)

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.
    |   |   |
    |----|----|
    |Subscription	|Select the assigned subscription|
    |Resource group|	Select resource group which you have created in Task 1|
    |Region|For this lab, you will use a GPT-4 model. This model is currently only available in certain regions. Please select a region from this list, In this lab Sweden Central is using for this resource|
    |Name|+++AzureOpenAI-AssistantsXX+++ (XX can be a unique number, you can add more digits after XX to make the name unique) |
    |Pricing tier|	Select Standard S0|

     ![](./media/image14.png)

7.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

      ![](./media/image15.png)

8.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

      ![](./media/image16.png)

9.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

      ![](./media/image17.png)

10.  Wait for the deployment to complete. The deployment will take around
    **2-3** minutes.

11. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

      ![](./media/image18.png)

12. Click on **Keys and Endpoints** from the left navigation menu and
    then copy the endpoint value in a notepad to **AzureAI ENDPOINT**
    and key to a variable **AzureAIKey**.

      ![](./media/image19.png)

## Task 3: Deploying an Azure OpenAI models

[!Alert] Important: If you’re in the new Azure OpenAI Studio, switch to the old look of Azure OpenAI Studio.

1.  On the **AzureOpenAI-AssistantsXX** window, click on **Overview** in
    the left navigation menu, then under the **Get Started** tab, click
    on the **Go to Azure OpenAI Studio** button to open **Azure OpenAI
    Studio** in a new browser

      ![](./media/image20.png)

2.  In the **Azure AI | Azure OpenAI Studio** window, click on **Create
    a new deployment** button**.**

      ![](./media/image21.png)

3.  In the **Deployments** window, click on **+Create new deployment**.

      ![](./media/image22.png)

4.  In the **Deploy model dialog** box, enter the following details and
    click on the **Create** button.

    - Select Model: **gpt-4**
    
    - Model Version**: 1106-Preview**
    
    - Deployment Name: enter +++gpt-4+++

    - Select the **Advanced options** and select the **Standard** as
      **Deployment type**
      ![](./media/image23.png)

5.  You will see a notification stating **Successfully Created
    deployment**. (In case, the notification did not appear on your
    window by default, click on the bell icon beside **Azure AI | Azure
    AI Studio** bar.

      ![](./media/image24.png)

6.  In the **Deployments** page, click on +**Create new deployment**.

      ![](./media/image25.png)

7.  In the **Deploy model** dialog box, under **Select a model** click
    on the dropdown select **gpt-4** field, under **Model version**
    select **vision-preview** and under **Deployment name** enter
    +++gpt-4-vision+++ Click on the **Create** button.

       ![](./media/image26.png)

8.  You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded. (You can also view the
    notification by clicking on the bell icon beside **Cognitive
    Services | Azure OpenAI Studio)**.

       ![](./media/image27.png)

9.  In the **Deployments** page, click on +**Create new deployment**.

       ![](./media/image28.png)

10. In the **Deploy model** dialog box, under **Select a model** click
    on the dropdown select **dall-e-3** field, under **Model version**
    select **Auto-update to default** and under **Deployment name**
    enter +++dall-e-3+++.** Click on the **Create** button.

       ![](./media/image29.png)

11. You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded. (You can also view the
    notification by clicking on the bell icon beside **Cognitive
    Services | Azure OpenAI Studio)**.

      ![](./media/image30.png)

## Task 4: Explore the Assistant's playground

1.  In Azure OpenAI Studio Home page, under **Welcome to** **Azure
    OpenAI Service**, in **Get started** section, click on the
    **Assistants playground**.

       ![](./media/image31.png)

2.  The Assistants playground allows you to explore, prototype, and test
    AI Assistants without needing to run any code. From this page, you
    can quickly iterate and experiment with new ideas.

3.  From the Assistant setup pane enter the below details

      - Assistant a name: **Math Assist**
      
      - Instructions: Enter the following instructions !!**You are an AI
        assistant that can write code to help answer math questions**!!
      
      - Deployment: **gpt-4**
      
      - Select the toggle **enabling code interpreter**
      ![](./media/image32.png)

4.  Under the Assistant setup click on **Save**

      ![](./media/image33.png)

5.  Enter a question for the assistant to answer: +++I need to solve
    the equation 3x + 11 = 14. Can you help me?+++

6.  Select the **Add and run button** .

     ![](./media/image34.png)

      ![](./media/image35.png)

While we can see that answer is correct, to confirm that the model used
code interpreter to get to this answer, and that the code it wrote is
valid rather than just repeating an answer from the model's training
data we'll ask another question.

7.  Enter the follow-up question: +++Show me the code you ran to get
    this solution.+++ Select the **Add and run button** 

     ![](./media/image36.png)

     ![](./media/image37.png)

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

      ![](./media/image38.png)

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open Folder**.

      ![](./media/image39.png)

3.  Navigate and select **Assistants** folder from **C:\LabFiles** and
    click on the **Select Folder** button.

       ![](./media/image40.png)

4.  If you see a dialog box - **Do you trust the authors of the files in
    this folder?**, then click on **Yes, I trust the author**.

      ![](./media/image41.png)

5.  In Visual Studio Code dropdown the **ASSISTANTS**, under
    **function_calling** navigate and click on
    **assistants_function_calling_with_bing_search.ipynb** notebook.

      ![](./media/image42.png)

6.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1^(st) cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

      ![](./media/image43.png)

      ![](./media/image44.png)

7.  If prompted to select the path, then select the **Python version
    3.12.2(or later version)** path as shown in the image.

      ![](./media/image45.png)

8.  Update the parameters ,replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    2), Bing search subscription key** with the values that you have
    saved in your notepad in the **Task 1**
     ![](./media/image46.png)
     ![](./media/image47.png)

9.  Define a function to call the Bing Search APIs, select 3^(rd),
    4^(th) cells. Then, execute the cell by clicking on the **start
    icon**.
      ![](./media/image48.png)

      ![](./media/image49.png)

10. Get things running end to end, select 5^(th) ,6^(th) ,7^(th),8^(th)
    cells. Then, execute the cell by clicking on the **start icon**.

     ![](./media/image50.png)

     ![](./media/image51.png)

     ![](./media/image52.png)

     ![](./media/image53.png)

     ![](./media/image54.png)

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

     ![](./media/image55.png)

2.  In the **.env** file, replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    2), gpt4 deployment name, DALLE3 deployment name and GPT 4 Vision
    deployment name** with the values that you have saved in your
    notepad in the **Task 3**.

      ![](./media/image56.png)

3.  Click on **File** and the click on **Save**.

     ![](./media/image57.png)

4.  In Visual Studio Code, under **multi-agent**, navigate and click on
    **multi-agent.ipynb** notebook.

      ![](./media/image58.png)

5.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1^(st) cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

6.  If prompted to select the path, then select the **Python version
    3.12.2(or later version)** path as shown in the image.

     ![](./media/image59.png)

7.  Select 2^(nd) cell. Then, execute the cell by clicking on the
    **start icon**.

     ![](./media/image60.png)

     ![](./media/image61.png)

8.  To generating images using a prompt to the Dalle-3 Model. The output
    is a .jpg file stored in the users local directory. Select 3^(rd)
    cell. Then, execute the cell by clicking on the **start icon**.

      ![](./media/image62.png)

9.  Initializes the agent with the definition described above. Select
    4^(th) cell. Then, execute the cell by clicking on the **start
    icon**.

      ![](./media/image63.png)

10. Image generator function calls the Dalle-3 image generator given the
    prompt. Select 5^(th) cell. Then, execute the cell by clicking on
    the **start icon**.

      ![](./media/image64.png)

11. Vision Assistant agent is responsible for analyzing images. The
    output is a new prompt to be used by the image creator agent. Select
    6^(th) cell. Then, execute the cell by clicking on the **start
    icon**.

      ![](./media/image65.png)

12. Initializes the agent with the definition described above. Select
    7^(th) cell. Then, execute the cell by clicking on the **start
    icon**.

      ![](./media/image66.png)

13. Vision assistant function calls the GPT4 Vision image analyzes given
    an image, execute the cell by clicking on the **start icon**.

     ![](./media/image67.png)

14. This agent facilitates the conversation between the user and other
    agents, ensuring successful completion of the task, execute the cell
    by clicking on the **start icon**.

     ![](./media/image68.png)

15. Initializes the agent with the definition described above, execute
    the cell by clicking on the **start icon**.

     ![](./media/image69.png)

16. This function calls the Assistant API to generate a main thread of
    communication between the agents listed in the agents_threads,
    execute the cell by clicking on the **start icon**.

      ![](./media/image70.png)

17. This agent facilitates the conversation between the user and other
    agents, ensuring successful completion of the task. Execute the cell
    by clicking on the **start icon**.

      ![](./media/image71.png)

       ![](./media/image72.png)

18. Example Questions, enter the !!Generate an image of a boat drifting
    in the water and analyze it and enhance the image!!. Execute the
    cell by clicking on the **start icon**.

      ![](./media/image73.png)

     ![](./media/image74.png)

     ![](./media/image75.png)

## Task 7: Delete the resources

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

     ![](./media/image76.png)

2.  Click on the AOAI-RGXXX resource group.

     ![](./media/image77.png)

3.  In the **Resource group** home page, select the **delete resource
    group**

     ![](./media/image78.png)

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “resource group name” to confirm deletion**
    field, then click on the **Delete** button.

     ![](./media/image79.png)

5.  On **Delete confirmation** dialog box, click on **Delete** button.

     ![](./media/image80.png)

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

     ![](./media/image81.png)

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
