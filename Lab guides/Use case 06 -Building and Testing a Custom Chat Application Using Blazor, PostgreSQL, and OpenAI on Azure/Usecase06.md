**Introduction**

Applications can connect to Azure Cosmos DB for NoSQL or Azure OpenAI
using their respective .NET SDKs. These SDKs can extend existing .NET
applications with NoSQL data storage and AI completion functionality
with relatively low friction.

The .NET SDK for Azure Cosmos DB for NoSQL is useful for business
applications that need to manage various account resources including
databases, containers, and items. The SDK can perform queries that
return multiple items, operations on specific items, and even
transactions that batch operations together over multiple items.

The .NET SDK for Azure OpenAI provides a streamlined interface for
interacting with the various models available for deployment.
Specifically, the SDK includes classes to interface directly with the
model, send prompts, fine tune the requests, and parse the completion
responses.

In this comprehensive use case, you will embark on the development
journey of a sophisticated chat application using a powerful stack of
technologies including Blazor, Azure OpenAI, Azure Cosmos DB, Docker,
Visual Studio Code, and .NET development framework. Leveraging Blazor's
capabilities, you will create both client-side and server-side
components for a responsive and interactive user interface. Azure OpenAI
will be integrated to enable advanced natural language processing,
enriching the chat experience with intelligent conversation
capabilities. Azure Cosmos DB will serve as the backend database,
providing global distribution and high availability for seamless data
management. Throughout this lab, you will gain practical insights into
deploying and testing your application using Docker containers, ensuring
consistency and reliability across different environments."

**Objective**

- To set up the development environment for Blazor, NoSQL, and OpenAI.

- To create a Blazor project and design a responsive chat interface.

- To configure NoSQL database on Azure and connect it to the Blazor app.

- To integrate Azure OpenAI for enhanced chat functionalities.

- To deploy the Blazor application and NoSQL database on Azure.

- To test the application in order to ensure seamless interaction
  between components.

- To monitor and troubleshoot the deployed application on Azure.

# Exercise 1: Setup

To complete this project, you need an Azure Cosmos DB for NoSQL account
and an Azure OpenAI account. To streamline this process, deploy a Bicep
template to Azure with both of these accounts.

## Task 1: Deploy infrastructure from template

1.  Open a new browser and enter the following URL in the address bar:
    <https://portal.azure.com/> to open the Azure Portal.

![](./media/image1.png)

2.  In the Azure portal, click on the **\[\>\_\] (Cloud Shell)** button
    at the top of the page to the right of the search box. A Cloud Shell
    pane will open at the bottom of the portal. The first time you open
    the Cloud Shell, you may be prompted to choose the type of shell you
    want to use (**Bash** or **PowerShell**). Select **Bash**. If you
    don’t see this option, then skip this step.

![A screenshot of a computer Description automatically
generated](./media/image2.png)

> ![A screenshot of a computer Description automatically generated with
> medium confidence](./media/image3.png)

3.  In **You have no storage mounted** dialog box, click on the **Create
    storage.**

![](./media/image4.png)

![](./media/image5.png)

![A close-up of a computer screen Description automatically
generated](./media/image6.png)

4.  Ensure the type of shell indicated on the top left of the Cloud
    Shell pane is switched to ***Bash***. If it’s ***PowerShell**,*
    switch to ***Bash*** by using the drop-down menu.

> ![](./media/image7.png)

5.  Once the terminal starts, enter the following command to download
    the sample application.

6.  Create a new shell variable named **resourceGroupName** with the
    name of the Azure resource group that you create
    (mslearn-cosmos-openai).

Copy

> resourceGroupName="mslearn-cosmos-openai"

![](./media/image8.png)

7.  Create a resource group using [az group
    create](https://learn.microsoft.com/en-us/cli/azure/group#az-group-create()).
    Then, execute the following command

Copy

az group create --name $resourceGroupName --location "eastus"

![](./media/image9.png)

8.  Deploy
    the [azuredeploy.json](https://github.com/Azure-Samples/cosmosdb-chatgpt/blob/main/azuredeploy.json) template
    file to the resource group using [az group deployment
    create](https://learn.microsoft.com/en-us/cli/azure/group/deployment#az-group-deployment-create).
    Then, execute the following command.

Copy

az deployment group create --resource-group $resourceGroupName --name
zero-touch-deployment --template-uri
https://raw.githubusercontent.com/Azure-Samples/cosmosdb-chatgpt/start/azuredeploy.json

9.  Select the near by your available region ,wait for the deployment to
    complete before proceeding with this project. This deployment can
    take approximately 5-10 minutes.

![A screenshot of a computer screen Description automatically
generated](./media/image10.png)

![](./media/image11.png)

## Task 2: Get Azure Cosmos DB for NoSQL and Azure OpenAI account credentials

Deployed Azure Cosmos DB for NoSQL and Azure OpenAI accounts and then
stored their credentials in the Azure App Service web app's
configuration. Now, you have the choice of using the Azure portal or
Azure CLI to retrieve the credentials for each service.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:
    [*https://portal.azure.com/*](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/announcing-the-public-preview-of-real-time-diarization-in-azure/ba-p/3876802),
    then press the **Enter** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image12.png)

2.  Click on the **Portal Menu**, then select **Resource group.**

![](./media/image13.png)

3.  Select the **mslearn-cosmos-openai** resource group.

![](./media/image14.png)

4.  On the **Resource Groups** page, expand the **Essentials** panel and
    observe the **Deployments** header. The status for the deployment
    should be **Succeeded** at this point.

![](./media/image15.png)

5.  Now, select the **Azure Cosmos DB** account to navigate to the
    resource's page.

> ![](./media/image16.png)

6.  Select the **Keys** option in the **Settings** section of the
    resource navigation menu. Record the value of
    the **URI** and **PRIMARY KEY** fields. You use these values later.

![](./media/image17.png)

7.  Return to the **Resource Groups** page. Select the **Azure
    OpenAI** account.

> ![](./media/image18.png)

8.  In your **Azure Open AI** window, navigate to the **Resource
    Management** section, and click on **Keys and Endpoints**.

![](./media/image19.png)

9.  In **Keys and Endpoints** page, copy **KEY1,** (*You can use
    either KEY1 or KEY2)* and **Endpoint** and then **Save** the notepad
    to use the information in the upcoming tasks.

> ![](./media/image20.png)

## Task 3: Run the Docker

1.  In your Windows search box, type Docker , then click on **Docker
    Desktop**.

![](./media/image21.png)

2.  Run the Docker Desktop.

![A screenshot of a computer Description automatically
generated](./media/image22.png)

## **Task 4: Install Dev Containers extension**

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> ![A screenshot of a computer Description automatically
> generated](./media/image23.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image24.png)

2.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    [https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers%20)
    then press the **Enter** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image25.png)

3.  On Dev Containers page, select on **Install** button.

![A screenshot of a computer Description automatically
generated](./media/image26.png)

4.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

![A screenshot of a computer Description automatically
generated](./media/image27.png)

5.  Open the Visual Studio Code.

![A screenshot of a computer Description automatically
generated](./media/image28.png)

6.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![A screenshot of a computer program Description automatically
generated](./media/image29.png)

7.  Clone
    the [azure-samples/cosmosdb-chatgpt](https://github.com/azure-samples/cosmosdb-chatgpt) GitHub
    repository into the current directory.

**Copy**

git clone https://github.com/Azure-Samples/cosmosdb-chatgpt.git

![A screen shot of a computer Description automatically
generated](./media/image30.png)

8.  In the **Teminal**, go to **cosmosdb-chatgpt** directory.

Copy

cd cosmosdb-chatgpt

9.  Switch to the start branch of the repository. Run the below command
    in the terminal

> BashCopy
>
> git checkout start

![A screenshot of a computer Description automatically
generated](./media/image31.png)

## Task 3: Configure dev environment

1.  Open the **Command Palette**, search for the \>**Dev
    Containers** commands, and then select \>**Dev Containers: Open
    Folder in Container**.

![](./media/image32.png)

2.  Navigate and select **cosmosdb-chatgpt** folder from **C:\LabFiles**
    and click on the **Select Folder** button.

> ![](./media/image33.png)
>
> ![](./media/image34.png)

3.  Visual Studio Code a notification stating Folder contains a Dev
    Container configuration file. Reopen folder to develop in a
    container appers, then click on the **Reopen in Container** button.

> ![](./media/image35.png)

1.  In case, **Not all host requirements in devcontainer.json are met by
    the Docker daemon.** dialog box appears, then click on the
    **Continue** button.

> ![](./media/image36.png)

2.  To Staring Dev container will take 2-3 min

![A screenshot of a computer Description automatically
generated](./media/image37.png)

3.  Validate that .NET 8 is installed in your environment, Run the below
    command

> BashCopy
>
> dotnet --list-sdks

![](./media/image38.png)

4.  Build the .NET project. Run the bellow command on the terminal.

> BashCopy
>
> dotnet build

![](./media/image39.png)

5.  Close the terminal.

# Exercise 2 - Setup and run the starter web application

The first step of this project is to walk through the existing starter
application, ensure it builds successfully, and then run the
application.

There are a few requirements in this exercise:

- Open the **CodeTour** within the application and walk through the
  entire tour.

- Successfully build the application.

- Run the application using the **Hot Reload** feature of .NET

After you complete this exercise, you'll have a general understanding of
the project and its components.

## Task 1: Walk through a tour of the code

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    <https://marketplace.visualstudio.com/items?itemName=vsls-contrib.codetour>
    then press the **Enter** button.

![](./media/image40.png)

2.  On **Code Tour** page, select on **Install** button.

![](./media/image41.png)

10. Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

![](./media/image42.png)

![A screenshot of a computer Description automatically
generated](./media/image43.png)

11. Open the **Command Palette**, search for
    the \>**CodeTour** commands, and then select \>**CodeTour: Start
    Tour**.

![](./media/image44.png)

12. Review the overview of the guided tour.

13. The guided tour of the codebase walks you through the following
    components of the application:

![A screen shot of a computer Description automatically
generated](./media/image45.png)

- The Message and Session types in the /Models path

> ![](./media/image46.png)
>
> ![](./media/image47.png)

- The Bicep template and various properties of the resources it deployed

> ![](./media/image48.png)

- The CosmosDbService and OpenAiService classes you modify as part of
  this project

> ![](./media/image49.png)

14. Finally, review the final step of the guided tour and finish the
    tour.

> ![](./media/image50.png)

## Task 2: Build and run the application

Now it's time to make sure the application works as expected. In this
step, build the application to verify that there's no issues before you
start and run the application using the stubbed out implementations of
the service methods.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![](./media/image29.png)

2.  Start the application with hot reloads enabled using [dotnet
    watch](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-watch).
    Run the below command

> BashCopy
>
> dotnet watch run --non-interactive

![](./media/image51.png)

3.  Visual Studio Code launches an in-tool simple browser with the web
    application running. ![A screenshot of a computer Description
    automatically generated](./media/image52.png)

4.  In the web application, **create a New Chat** session with at least
    one message.

> ![](./media/image53.png)

5.  The AI assistant responds with the prebaked string values that you
    observed during the guided tour of the project's code.

> How do I learn the value of PI?

![](./media/image54.png)

![A screenshot of a computer Description automatically
generated](./media/image55.png)

6.  Close the terminal.

** Important: **Closing the terminal releases the port so you can
rebuild and run this application again later in this project. If you
forget to close the terminal, you may run into issues with the
application's port already being in use when debugging later in the
project.

# Exercise 3 - Connect to Azure OpenAI

The OpenAiService class contains a stub implementation of a service that
can send prompts to an AI assistant and parse the responses.

There are a few key requirements to tackle in this exercise:

- Import the .NET SDK for Azure OpenAI

- Add the Azure OpenAI endpoint and key to the application settings

- Modify the service class with various members and a client instance

## Task 1: Import the .NET SDK

The [Azure.AI.OpenAI](https://www.nuget.org/packages/Azure.AI.OpenAI) package
on NuGet provides a typed SDK to access various model deployments from
your account endpoint.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![A screenshot of a computer program Description automatically
generated](./media/image29.png)

2.  Use [dotnet add
    package](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package) to
    import the Azure.AI.OpenAI package from NuGet specifying a
    prerelease version.

> BashCopy
>
> dotnet add package Azure.AI.OpenAI --prerelease

![](./media/image56.png)

3.  Build the .NET project again.

> BashCopy
>
> dotnet build

![](./media/image57.png)

4.  Close the terminal.

## Task 2: Add application settings

In a .NET application, it's common to use the configuration providers to
inject new settings into your application. For this application, use
the appsettings.Development.json file to provide the most current values
for the Azure OpenAI endpoint and key.

1.  In the root of the project, create a new file
    named **appsettings.Development.json**.

> ![](./media/image58.png)

** Important**

On Linux, files are case-sensitive. The .NET environment for this
project is named **Development** and the filename must match that
environment name to work.

2.  Within the file, create a new JSON object with a placeholder
    property for OpenAi settings.

> JSONCopy
>
> {
>
> "OpenAi": {
>
> }
>
> }

3.  Within the OpenAi property, create two new properties for
    the Endpoint and Key. Use the Azure OpenAI endpoint and key settings
    you recorded earlier in this lab(Exercise 1\>Task 2).

> JSONCopy
>
> {
>
> "OpenAi": {
>
> "Endpoint": "\<your-azure-openai-endpoint\>",
>
> "Key": "\<your-azure-openai-key\>"
>
> }
>
> }

![](./media/image59.png)

** Note:** The key in this example is fictitious.

4.  Save the **appsettings.Development.json** file.

## Task 3: Add required members and a client instance

Finally, implement the class variables required to use the Azure OpenAI
client. At this step, implement a few static prompts and create a new
instance of the OpenAIClient class.

1.  Open the **Services/OpenAiService.cs** file.

> ![](./media/image60.png)

2.  Add using directives for the Azure and Azure.AI.OpenAI namespaces.

> C#Copy
>
> using Azure;
>
> using Azure.AI.OpenAI;

3.  Within the OpenAiService class, add a new variable
    named \_client that's of
    type [OpenAIClient](https://learn.microsoft.com/en-us/dotnet/api/azure.ai.openai.openaiclient).

> C#Copy
>
> private readonly OpenAIClient \_client;

4.  Create a new string variable named \_systemPromptText with a static
    block of text to send to the AI assistant before each prompt.

> C#Copy
>
> private readonly string \_systemPrompt = @"
>
> You are an AI assistant that helps people find information.
>
> Provide concise answers that are polite and professional." +
> Environment.NewLine;

5.  Create another new string variable named \_summarizePrompt with a
    static block of text to send to the AI assistant with instructions
    on how to summarize a conversation.

> C#Copy
>
> private readonly string \_summarizePrompt = @"
>
> Summarize this prompt in one or two words to use as a label in a
> button on a web page.
>
> Do not use any punctuation." + Environment.NewLine;

6.  Within the constructor of the class, add two extra lines of code to
    check if the endpoint or key is null.
    Use ArgumentNullException.ThrowIfNullOrEmpty to throw an error early
    if either of these values are null.

> C#Copy
>
> ArgumentNullException.ThrowIfNullOrEmpty(endpoint);
>
> ArgumentNullException.ThrowIfNullOrEmpty(key);

**Note:**When you run the application, this will throw an error right
away if either of these settings don't have a valid value provided
through the **appsettings.Development.json** file.

7.  Next, take the model name that is a parameter of the constructor and
    save it to the \_modelName variable.

> C#Copy
>
> \_modelName = modelName;

8.  Finally, create a new instance of the OpenAIClient class using the
    endpoint to build a Uri and the key to build an AzureKeyCredential.

> C#Copy
>
> Uri uri = new(endpoint);
>
> AzureKeyCredential credential = new(key);
>
> \_client = new(
>
> endpoint: uri,
>
> keyCredential: credential
>
> );

![](./media/image61.png)

**Reference code**

using Cosmos.Chat.GPT.Models;

using Azure;

using Azure.AI.OpenAI;

namespace Cosmos.Chat.GPT.Services;

public class OpenAiService

{

private readonly string \_modelName = String.Empty;

private readonly OpenAIClient \_client;

private readonly string \_systemPrompt = @"

You are an AI assistant that helps people find information.

Provide concise answers that are polite and professional." +
Environment.NewLine;

private readonly string \_summarizePrompt = @"

Summarize this prompt in one or two words to use as a label in a button
on a web page.

Do not use any punctuation." + Environment.NewLine;

public OpenAiService(string endpoint, string key, string modelName)

{

ArgumentNullException.ThrowIfNullOrEmpty(modelName);

ArgumentNullException.ThrowIfNullOrEmpty(endpoint);

ArgumentNullException.ThrowIfNullOrEmpty(key);

\_modelName = modelName;

Uri uri = new(endpoint);

AzureKeyCredential credential = new(key);

\_client = new(

endpoint: uri,

keyCredential: credential

);

9.  Save the **Services/OpenAiService.cs** file.

![](./media/image62.png)

## Task 4: Build the project

At this point, your constructor should include enough logic to create a
client instance. Since the class doesn't do anything with the client
yet, there's no point in running the web application, but there's value
in building the application to make sure your code doesn't have any
omissions or errors.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![A screenshot of a computer program Description automatically
generated](./media/image29.png)

2.  Build the .NET project.

> BashCopy
>
> dotnet build

![](./media/image63.png)

3.  Observe the build output and check to make sure there aren't any
    build errors.

4.  Close the terminal.

# Exercise 4- Implement the Azure OpenAI service

Let's start with the simplest service to implement, OpenAiService. This
service only contains two methods that we need to implement so we can
implement basic prompts and completions right away. We're not
implementing our Azure Cosmos DB for NoSQL data service until later, so
we can't persist our sessions across debugging sessions yet.

In this exercise, we have a few key requirements:

- Send a question from the user to the AI assistant and ask for a
  response.

- Send a series of prompts to the AI assistant and ask for a
  summarization of the conversation.

## Task 1: Ask the AI model a question

First, implement a question-answer conversation by sending a system
prompt, a question, and session ID so the AI model can provide an answer
in the context of the current conversation. Make sure you measure the
number of tokens it takes to parse the prompt and return a response (or
completion in this context).

1.  Open the **Services/OpenAiService.cs** file.

2.  Within the GetChatCompletionAsync method, remove any existing
    placeholder code:

> C#Copy
>
> public async Task\<(string completionText, int completionTokens)\>
> GetChatCompletionAsync(string sessionId, string userPrompt)
>
> {
>
> }

3.  Create a new variable named options of type ChatCompletionsOptions.
    Add the two message variables to the Messages list, set the value
    of User to the sessionId constructor parameter,
    set MaxTokens to 4000, and set the remaining properties to the
    recommended values here.

> C#Copy
>
> ChatCompletionsOptions options = new()
>
> {
>
> DeploymentName = "chatmodel",
>
> Messages = {
>
> new ChatRequestSystemMessage(\_systemPrompt),
>
> new ChatRequestUserMessage(userPrompt)
>
> },
>
> User = sessionId,
>
> MaxTokens = 4000,
>
> Temperature = 0.3f,
>
> NucleusSamplingFactor = 0.5f,
>
> FrequencyPenalty = 0,
>
> PresencePenalty = 0
>
> };

**Note: 4096** is the maximum number of tokens for
the **gpt-35-turbo** model. We're just rounding down here to simplify
things.

4.  Asynchronously invoke the GetChatCompletionsAsync method of the
    Azure OpenAI client variable (\_client). Pass in the name of the
    model (\_modelName) and the options variable you created. Store the
    result in a variable named completions of type ChatCompletions.

C#Copy

Response\<ChatCompletions\> completionsResponse =
await_client.GetChatCompletionsAsync(options);

ChatCompletions completions = completionsResponse.Value;

** Note:** The GetChatCompletionsAsync method returns an object of
type Task\<Response\<ChatCompletions\>\>. The Response\<T\> class
contains a implicit conversion to type T allowing you to select a type
based on your application's needs. You can store the result as
either Response\<ChatCompletions\> to get the full metadata from the
response or just ChatCompletions if you only care about the content of
the result itself.

5.  Finally, return a tuple as the result of
    the GetChatCompletionAsync method with the content of the completion
    as a string, the number of tokens associated with the prompt, and
    the number of tokens for the response.

> C#Copy

return (

completionText: completions.Choices\[0\].Message.Content,

completionTokens: completions.Usage.CompletionTokens

);

![](./media/image64.png)

## Task 2: Ask the AI model to summarize a conversation

Now, send the AI model a different system prompt, your current
conversation, and session ID so the AI model can summarize the
conversation in a couple of words.

1.  Within the SummarizeAsync method, remove any existing placeholder
    code:

> C#Copy
>
> public async Task\<string\> SummarizeAsync(string sessionId, string
> conversationText)
>
> {
>
> }

2.  Create a ChatCompletionsOptions variable named options with the two
    message variables in the Messages list, User set to
    the sessionId constructor parameter, MaxTokens set to 200, and the
    remaining properties to the recommended values here:

> C#Copy
>
> ChatCompletionsOptions options = new()
>
> {
>
> DeploymentName = "chatmodel",
>
> Messages = {
>
> new ChatRequestSystemMessage(\_systemPrompt),
>
> new ChatRequestUserMessage(conversationText)
>
> },
>
> User = sessionId,
>
> MaxTokens = 200,
>
> Temperature = 0.0f,
>
> NucleusSamplingFactor = 1.0f,
>
> FrequencyPenalty = 0,
>
> PresencePenalty = 0
>
> };

3.  Invoke \_client.GetChatCompletionsAsync asynchronously with the
    model name (\_modelName) and the options variable as parameters.
    Store the result in a variable named completions of
    type ChatCompletions.

> C#Copy

Response\<ChatCompletions\> completionsResponse = await
\_client.GetChatCompletionsAsync(options);

ChatCompletions completions = completionsResponse.Value;

4.  Return the content of the completion as a string as the result of
    the SummarizeAsync method.

> C#Copy

string completionText = completions.Choices\[0\].Message.Content;

return completionText;

![](./media/image65.png)

**Note: Reference code**

public async Task\<(string completionText, int completionTokens)\>
GetChatCompletionAsync(string sessionId, string userPrompt)

{

// ChatRequestSystemMessage systemMessage = new(ChatRole.System,
\_systemPrompt);

// ChatRequestUserMessage userMessage = new(ChatRole.User, userPrompt);

ChatCompletionsOptions options = new()

{

DeploymentName = "chatmodel",

Messages = {

new ChatRequestSystemMessage(\_systemPrompt),

new ChatRequestUserMessage(userPrompt)

},

User = sessionId,

MaxTokens = 4000,

Temperature = 0.3f,

NucleusSamplingFactor = 0.5f,

FrequencyPenalty = 0,

PresencePenalty = 0

};

Response\<ChatCompletions\> completionsResponse = await
\_client.GetChatCompletionsAsync(options);

ChatCompletions completions = completionsResponse.Value;

return (

completionText: completions.Choices\[0\].Message.Content,

completionTokens: completions.Usage.CompletionTokens

);

}

public async Task\<string\> SummarizeAsync(string sessionId, string
conversationText)

{

// ChatMessage systemMessage = new (ChatRole.System, \_summarizePrompt);

// ChatMessage userMessage = new (ChatRole.User, conversationText);

ChatCompletionsOptions options = new()

{

DeploymentName = "chatmodel",

Messages = {

new ChatRequestSystemMessage(\_systemPrompt),

new ChatRequestUserMessage(conversationText)

},

User = sessionId,

MaxTokens = 200,

Temperature = 0.0f,

NucleusSamplingFactor = 1.0f,

FrequencyPenalty = 0,

PresencePenalty = 0

};

Response\<ChatCompletions\> completionsResponse = await
\_client.GetChatCompletionsAsync(options);

ChatCompletions completions = completionsResponse.Value;

string completionText = completions.Choices\[0\].Message.Content;

return completionText;

}

}

5.  Save the **Services/OpenAiService.cs** file.

## Task 3:Build the project

At this point, your application should have a thorough enough
implementation of the Azure OpenAI service that you can test the
application. Remember, you haven't implemented a data store yet, so your
conversations aren't persisted between debugging sessions.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![](./media/image29.png)

2.  Build the .NET project.

> BashCopy
>
> dotnet build

![](./media/image66.png)

3.  Start the application with hot reloads enabled using dotnet watch.

> BashCopy
>
> dotnet watch run --non-interactive

![](./media/image67.png)

4.  Visual Studio Code launches the in-tool simple browser again with
    the web application running. In the web application, create a new
    chat session and ask the AI assistant a question. The AI assistant
    now responds with a completion created by the model. You should also
    notice that the *token* UI fields are now populated with real-world
    token usage for each completion and prompt.

&nbsp;

3.  On the web application click on the **Create New Chat** button.

![](./media/image68.png)

4.  Paste the following text in the text box and click on the **Send**
    icon.

**CodeCopy**

**How large microsoft's campus?**

![](./media/image69.png)

![](./media/image70.png)

![](./media/image71.png)

5.  To stop the port Press **ctrl+c** and close the terminal.

**Note:** The **Hot Reload** feature is enabled here if you need to make
a small correction to the application's code. For more information,
see [**.NET Hot Reload support for ASP.NET
Core**](https://learn.microsoft.com/en-us/aspnet/core/test/hot-reload).

# Exercise 5- Connect to Azure Cosmos DB for NoSQL

The CosmosDbService class contains a stub implementation of a service
similar to the OpenAiService class you worked on previously in this
module. In contrast, this class uses the .NET SDK for Azure Cosmos DB,
which works slightly different.

There are a few key requirements to tackle in this exercise:

- Import the .NET SDK for Azure Cosmos DB for NoSQL

- Add the Azure Cosmos DB for NoSQL endpoint and key to the application
  settings

- Modify the service class with various members and a client instance

## Task 1: Import the .NET SDK

The [Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos) NuGet
package is a typed library that simplifies the process of accessing
Azure Cosmos DB for NoSQL from a .NET application.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![A screenshot of a computer program Description automatically
generated](./media/image29.png)

2.  Import the Microsoft.Azure.Cosmos package from NuGet with dotnet add
    package.

> BashCopy
>
> dotnet add package Microsoft.Azure.Cosmos

![](./media/image72.png)

3.  Build the .NET project one more time.

> BashCopy
>
> dotnet build

![](./media/image73.png)

4.  Close the terminal.

## Task 2: Add application settings

Use the appsettings.Development.json file again to provide current
values for the Azure Cosmos DB for NoSQL endpoint and key.

1.  Open the **appsettings.Development.json** file.

2.  Within the file, create another new JSON object with a placeholder
    property for CosmosDb settings.

3.  Within the CosmosDb property, create two new properties for
    the Endpoint and Key. Use the Azure Cosmos DB endpoint and key
    settings you recorded earlier in this lab.

> JSONCopy
>
> {
>
> "OpenAi": {
>
> "Endpoint": "\<your-azure-openai-endpoint\>",
>
> "Key": "\<your-azure-openai-key\>"
>
> },
>
> "CosmosDb": {
>
> "Endpoint": "\<your-azure-cosmos-db-endpoint\>",
>
> "Key": "\<your-azure-cosmos-db-key\>"
>
> }
>
> }

![](./media/image74.png)

** Note:** The key in this example is fictitious.

4.  Save the **appsettings.Development.json** file.

## Task 3: Add required members and a client instance

Finally, implement the class variables and client required to access
Azure Cosmos DB for NoSQL using the client. For this step, use the SDK's
client classes to implement an instance of type Container in
the CosmosDbService class.

1.  Open the **Services/CosmosDbService.cs** file.

> ![](./media/image75.png)

2.  Add using directives for the following namespaces.

    - Microsoft.Azure.Cosmos

    &nbsp;

    - Microsoft.Azure.Cosmos.Fluent

> C#Copy
>
> using Microsoft.Azure.Cosmos;
>
> using Microsoft.Azure.Cosmos.Fluent;

3.  Within the CosmosDbService class, add a new Container-typed variable
    named \_container.

> C#Copy
>
> private readonly Container \_container;

4.  Within the constructor,
    add ArgumentNullException.ThrowIfNullOrEmpty checks to throw an
    error if either the endpoint or key parameters are null.

> C#Copy
>
> ArgumentNullException.ThrowIfNullOrEmpty(endpoint);
>
> ArgumentNullException.ThrowIfNullOrEmpty(key);

5.  Now, create a variable named options of
    type [CosmosSerializationOptions](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.cosmosserializationoptions).
    Set the PropertyNamingPolicy property of the variable
    to CosmosPropertyNamingPolicy.CamelCase.

> C#Copy
>
> CosmosSerializationOptions options = new()
>
> {
>
> PropertyNamingPolicy = CosmosPropertyNamingPolicy.CamelCase
>
> };

** **

**Note:** Setting this property will ensure that the JSON produced by
the SDK is both serialized and deserialized in *camel case* regardless
of how it's corresponding property is cased in the .NET class.

6.  Create a new instance of
    type [CosmosClient](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) named client using
    the [CosmosClientBuilder](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.fluent.cosmosclientbuilder) class,
    endpoint, key, and serialization options you specified earlier.

> C#Copy
>
> CosmosClient client = new CosmosClientBuilder(endpoint, key)
>
> .WithSerializerOptions(options)
>
> .Build();

7.  Create a new nullable variable of type Database named database by
    calling the GetDatabase method of the client variable.

> C#Copy
>
> Database? database = client?.GetDatabase(databaseName);

8.  Create another nullable variable named container of
    type Container by calling the GetContainer method of the database
    variable.

> C#Copy
>
> Container? container = database?.GetContainer(containerName);

9.  Finally, assign the constructor's container variable to the
    class' \_container variable only if it's not null. If it's null,
    throw an ArgumentException.

> C#Copy
>
> \_container = container ??
>
> throw new ArgumentException("Unable to connect to existing Azure
> Cosmos DB container or database.");

![](./media/image76.png)

10. Save the **Services/CosmosDbService.cs** file.

## Task 4: Check your work

At this point, your constructor should include enough logic to create a
container instance that the rest of the service uses. Since the class
doesn't do anything with the container yet, there's no point in running
the web application, but there's value in building the application to
make sure your code doesn't have any omissions or errors.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![](./media/image29.png)

2.  Build the .NET project.

> BashCopy
>
> dotnet build

![](./media/image77.png)

3.  Observe the build output and check to make sure there aren't any
    build errors.

4.  Close the terminal.

# Exercise 6- Implement the Azure Cosmos DB for NoSQL service

The Azure Cosmos DB service (CosmosDbService) manages querying,
creating, deleting, and updating sessions and messages in your AI
assistant application. To manage all of these operations, the service is
required to implement multiple methods for each potential operation
using various features of the .NET SDK.

There are multiple key requirements to tackle in this exercise:

- Implement operations to create a session or message

- Implement queries to retrieve multiple sessions or messages

- Implement an operation to update a single session or batch update
  multiple messages

- Implement an operation to query and delete multiple related sessions
  and messages

## Task 1: Create a session or message

Azure Cosmos DB for NoSQL stores data in JSON format allowing us to
store many types of data in a single container. This application stores
both a chat *"session"* with the AI assistant and the
individual *"messages"* within each session. With the API for NoSQL, the
application can store both types of data in the same container and then
differentiate between these types using a simple type field.

1.  Open the **Services/CosmosDbService.cs** file.

2.  Within the InsertSessionAsync method, remove any existing
    placeholder code:

> C#Copy
>
> public async Task\<Session\> InsertSessionAsync(Session session)
>
> {
>
> }

3.  Create a new variable named partitionKey of
    type [PartitionKey](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.partitionkey) using
    the current session's SessionId property as the parameter.

> C#Copy
>
> PartitionKey partitionKey = new(session.SessionId);

4.  Invoke the CreateItemAsync method of the container passing in
    the session parameter and partitionKey variable. Return the response
    as the result of the InsertSessionAsync method.

> C#Copy
>
> return await \_container.CreateItemAsync\<Session\>(
>
> item: session,
>
> partitionKey: partitionKey
>
> );

5.  Within the InsertMessageAsync method, remove any existing
    placeholder code:

> public async Task\<Message\> InsertMessageAsync(Message message)
>
> {
>
> }

6.  Create a PartitionKey variable using session.SessionId as the value
    of the partition key.

> C#Copy
>
> PartitionKey partitionKey = new(message.SessionId);

7.  Create a new message variable named newMessage with
    the Timestamp property updated to the current UTC timestamp.

> C#Copy
>
> Message newMessage = message with { TimeStamp = DateTime.UtcNow };

8.  Invoke CreateItemAsync passing in both the new message and partition
    key variables. Return the response as the result
    of InsertMessageAsync.

> C#Copy
>
> return await \_container.CreateItemAsync\<Message\>(
>
> item: newMessage,
>
> partitionKey: partitionKey
>
> );

![](./media/image78.png)

9.  Save the **Services/CosmosDbService.cs** file.

## Task 2: Retrieve multiple sessions or messages

There are two main use cases where the application needs to retrieve
multiple items from our container. First, the application retrieves all
sessions for the current user by filtering the items to ones where type
= Session. Second, the application retrieves all messages for a session
by performing a similar filter where type = Session & sessionId =
\<current-session-id\>. Implement both queries here using the .NET SDK
and a feed iterator.

1.  Within the GetSessionsAsync method, remove any existing placeholder
    code:

> public async Task\<List\<Session\>\> GetSessionsAsync()
>
> {
>
> }

2.  Create a new variable named query of
    type [QueryDefinition](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.querydefinition) with
    the SQL query SELECT DISTINCT \* FROM c WHERE c.type = @type. Use
    the fluent WithParameter method to assign the name of
    the Session class as the value for the parameter.

> C#Copy
>
> QueryDefinition query = new QueryDefinition("SELECT DISTINCT \* FROM c
> WHERE c.type = @type")
>
> .WithParameter("@type", nameof(Session));

3.  Invoke the generic GetItemQueryIterator\<\> method on
    the \_container variable passing in the generic type Session and
    the query variable as a parameter. Store the result in a variable of
    type FeedIterator\<Session\> named response.

> C#Copy
>
> FeedIterator\<Session\> response =
> \_container.GetItemQueryIterator\<Session\>(query);

4.  Create a new generic list variable named output.

> C#Copy
>
> List\<Session\> output = new();

5.  Create a *while loop* that runs until response.HasMoreResults is no
    longer true.

> C#Copy
>
> while (response.HasMoreResults)
>
> {
>
> }

** Note:** Using a while loop here will effectively loop through all
pages of your response until there are no pages left.

6.  Within the while loop, asynchronously get the next page of results
    by invoking ReadNextAsync on the response variable and then add
    those results to the list variable named output.

> C#Copy
>
> FeedResponse\<Session\> results = await response.ReadNextAsync();
>
> output.AddRange(results);

7.  Outside the while loop, return the output variable with a list of
    sessions as the result of the GetSessionsAsync method.

> C#Copy
>
> return output;

8.  Within the GetSessionMessagesAsync method, remove any existing
    placeholder code:

> C#Copy
>
> public async Task\<List\<Message\>\> GetSessionMessagesAsync(string
> sessionId)
>
> {
>
> }

9.  Create a query variable of type QueryDefinition. Use the SQL
    query SELECT \* FROM c WHERE c.sessionId = @sessionId AND c.type
    = @type. Use the fluent WithParameter method to assign
    the @sessionId parameter to the session identifier passed in as a
    parameter, and the @type parameter to the name of the Message class.

> C#Copy
>
> QueryDefinition query = new QueryDefinition("SELECT \* FROM c WHERE
> c.sessionId = @sessionId AND c.type = @type")
>
> .WithParameter("@sessionId", sessionId)
>
> .WithParameter("@type", nameof(Message));

10. Create a FeedIterator\<Message\> using the query variable and
    the GetItemQueryIterator\<\> method.

> C#Copy
>
> FeedIterator\<Message\> response =
> \_container.GetItemQueryIterator\<Message\>(query);

11. Use a *while loop* to iterate through all pages of results and store
    the results in a single List\<Message\> variable named output.

> C#Copy
>
> List\<Message\> output = new();
>
> while (response.HasMoreResults)
>
> {
>
> FeedResponse\<Message\> results = await response.ReadNextAsync();
>
> output.AddRange(results);
>
> }

12. Return the output variable as the result of
    the GetSessionMessagesAsync method.

> C#Copy
>
> return output;

![](./media/image79.png)

13. Save the **Services/CosmosDbService.cs** file.

## Task 3: Update one or more sessions or messages

There are scenarios when either a single session requires an update or
more than one message requires an update. For the first scenario, use
the ReplaceItemAsync method of the SDK to replace an existing item with
a modified version. For the second scenario, use the transactional batch
capability of the SDK to modify multiple messages in a single batch.

1.  Within the UpdateSessionAsync method, remove any existing
    placeholder code:

> public async Task\<Session\> UpdateSessionAsync(Session session)
>
> {
>
> }

2.  Create a PartitionKey variable using session.SessionId as the value
    of the partition key.

> C#Copy
>
> PartitionKey partitionKey = new(session.SessionId);

3.  Invoke ReplaceItemAsync passing in the new message, message's unique
    identifier and partition key. Return the response as the result
    of UpdateSessionAsync.

> C#Copy
>
> return await \_container.ReplaceItemAsync(
>
> item: session,
>
> id: session.Id,
>
> partitionKey: partitionKey
>
> );

4.  Within the UpsertSessionBatchAsync method, remove any existing
    placeholder code:

> public async Task UpsertSessionBatchAsync(params dynamic\[\] messages)
>
> {
>
> }

5.  Use language-integrated query (LINQ) to validate that all messages
    contain a single session identifier (SessionId). If any of the
    messages contain a different value, throw an ArgumentException.

> C#Copy
>
> if (messages.Select(m =\> m.SessionId).Distinct().Count() \> 1)
>
> {
>
> throw new ArgumentException("All items must have the same partition
> key.");
>
> }

6.  Create a new PartitionKey variable using the SessionId property of
    the first message.

> C#Copy
>
> PartitionKey partitionKey = new(messages.First().SessionId);

** Note:** Remember, you can safely assume that all messages have the
same session identifier if the application has moved to this point in
the method's code.

7.  Create a new variable named batch of
    type [TransactionalBatch](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.transactionalbatch) by
    invoking the CreateTransactionalBatch method of
    the \_container variable. Pass in the current partition key variable
    as the partition key to use for the batch operations.

> C#Copy
>
> TransactionalBatch batch =
> \_container.CreateTransactionalBatch(partitionKey);
>
> ** **

8.  Iterate over each message in the messages array using a *foreach
    loop*.

> C#Copy
>
> foreach (var message in messages)
>
> {
>
> }

9.  Within the foreach loop, add each message as an **upsert** operation
    to the batch.

> C#Copy
>
> batch.UpsertItem(
>
> item: message
>
> );

** Note: Upsert** tells Azure Cosmos DB to determine, server-side,
whether an item should be replaced or updated. Azure Cosmos DB will make
this determination with the id and partition key of each item.

10. Outside of the foreach loop, asynchronously invoke
    the ExecuteAsync method of the batch to execute all operations
    within the batch.

> C#Copy
>
> await batch.ExecuteAsync();

![](./media/image80.png)

11. Save the **Services/CosmosDbService.cs** file.

## Task 4: Remove a session and all related messages

Finally, combine the query and transactional batch functionality to
remove multiple items. In this example, get the session item and all
related messages by querying for all items with a specific session
identifier regardless of type. Then, create a transactional batch to
delete all matched items as a single transaction.

1.  Within the DeleteSessionAndMessagesAsync method, remove any existing
    placeholder code:

> C#Copy
>
> public async Task DeleteSessionAndMessagesAsync(string sessionId)
>
> {
>
> }

2.  Create a variable named partitionKey of type PartitionKey using
    the sesionId string value passed in as a parameter to this method.

> C#Copy
>
> PartitionKey partitionKey = new(sessionId);

3.  Using the same sessionId method parameter, build
    a QueryDefinition object that finds all items that match the session
    identifier. Use a query parameter for the sessionId and ensure that
    you don't filter the query on the type of item.

> C#Copy
>
> QueryDefinition query = new QueryDefinition("SELECT VALUE c.id FROM c
> WHERE c.sessionId = @sessionId")
>
> .WithParameter("@sessionId", sessionId);

** Note:** If you apply a type filter in this query, you may
inadvertently miss related messages or sessions that should be bulk
removed as part of this operation.

4.  Create a new FeedIterator\<string\> using GetItemQueryIterator and
    the query you built.

> C#Copy
>
> FeedIterator\<string\> response =
> \_container.GetItemQueryIterator\<string\>(query);

1.  Create
    a TransactionalBatch named batch using CreateTransactionalBatch and
    the partition key variable.

> C#Copy
>
> TransactionalBatch batch =
> \_container.CreateTransactionalBatch(partitionKey);

2.  Create a *while loop* to iterate through all pages of results.
    Within the while loop, get the next page of results and use
    a *foreach loop* to iterate through all item identifiers per page.
    Within the foreach loop, add a batch operation to delete the item
    using batch.DeleteItem.

> C#Copy
>
> while (response.HasMoreResults)
>
> {
>
> FeedResponse\<string\> results = await response.ReadNextAsync();
>
> foreach (var itemId in results)
>
> {
>
> batch.DeleteItem(
>
> id: itemId
>
> );
>
> }
>
> }

3.  After the while loop, execute the batch using batch.ExecuteAsync.

> C#Copy
>
> await batch.ExecuteAsync();

![](./media/image81.png)

4.  Save the **Services/CosmosDbService.cs** file.

## Note: Reference code

using Cosmos.Chat.GPT.Models;

using Microsoft.Azure.Cosmos;

using Microsoft.Azure.Cosmos.Fluent;

namespace Cosmos.Chat.GPT.Services;

public class CosmosDbService

{

private readonly Container \_container;

public CosmosDbService(string endpoint, string key, string databaseName,
string containerName)

{

ArgumentNullException.ThrowIfNullOrEmpty(databaseName);

ArgumentNullException.ThrowIfNullOrEmpty(containerName);

ArgumentNullException.ThrowIfNullOrEmpty(endpoint);

ArgumentNullException.ThrowIfNullOrEmpty(key);

CosmosSerializationOptions options = new()

{

PropertyNamingPolicy = CosmosPropertyNamingPolicy.CamelCase

};

CosmosClient client = new CosmosClientBuilder(endpoint, key)

.WithSerializerOptions(options)

.Build();

Database? database = client?.GetDatabase(databaseName);

Container? container = database?.GetContainer(containerName);

\_container = container ??

throw new ArgumentException("Unable to connect to existing Azure Cosmos
DB container or database.");

}

public async Task\<Session\> InsertSessionAsync(Session session)

{

PartitionKey partitionKey = new(session.SessionId);

return await \_container.CreateItemAsync\<Session\>(

item: session,

partitionKey: partitionKey

);

}

public async Task\<Message\> InsertMessageAsync(Message message)

{

PartitionKey partitionKey = new(message.SessionId);

Message newMessage = message with { TimeStamp = DateTime.UtcNow };

return await \_container.CreateItemAsync\<Message\>(

item: newMessage,

partitionKey: partitionKey

);

}

public async Task\<List\<Session\>\> GetSessionsAsync()

{

QueryDefinition query = new QueryDefinition("SELECT DISTINCT \* FROM c
WHERE c.type = @type")

.WithParameter("@type", nameof(Session));

FeedIterator\<Session\> response =
\_container.GetItemQueryIterator\<Session\>(query);

List\<Session\> output = new();

while (response.HasMoreResults)

{

FeedResponse\<Session\> results = await response.ReadNextAsync();

output.AddRange(results);

}

return output;

}

public async Task\<List\<Message\>\> GetSessionMessagesAsync(string
sessionId)

{

QueryDefinition query = new QueryDefinition("SELECT \* FROM c WHERE
c.sessionId = @sessionId AND c.type = @type")

.WithParameter("@sessionId", sessionId)

.WithParameter("@type", nameof(Message));

FeedIterator\<Message\> response =
\_container.GetItemQueryIterator\<Message\>(query);

List\<Message\> output = new();

while (response.HasMoreResults)

{

FeedResponse\<Message\> results = await response.ReadNextAsync();

output.AddRange(results);

}

return output;

}

public async Task\<Session\> UpdateSessionAsync(Session session)

{

PartitionKey partitionKey = new(session.SessionId);

return await \_container.ReplaceItemAsync(

item: session,

id: session.Id,

partitionKey: partitionKey

);

}

public async Task UpsertSessionBatchAsync(params dynamic\[\] messages)

{

if (messages.Select(m =\> m.SessionId).Distinct().Count() \> 1)

{

throw new ArgumentException("All items must have the same partition
key.");

}

PartitionKey partitionKey = new(messages.First().SessionId);

TransactionalBatch batch =
\_container.CreateTransactionalBatch(partitionKey);

foreach (var message in messages)

{

batch.UpsertItem(

item: message

);

}

await batch.ExecuteAsync();

}

public async Task DeleteSessionAndMessagesAsync(string sessionId)

{

PartitionKey partitionKey = new(sessionId);

QueryDefinition query = new QueryDefinition("SELECT VALUE c.id FROM c
WHERE c.sessionId = @sessionId")

.WithParameter("@sessionId", sessionId);

FeedIterator\<string\> response =
\_container.GetItemQueryIterator\<string\>(query);

TransactionalBatch batch =
\_container.CreateTransactionalBatch(partitionKey);

while (response.HasMoreResults)

{

FeedResponse\<string\> results = await response.ReadNextAsync();

foreach (var itemId in results)

{

batch.DeleteItem(

id: itemId

);

}

}

await batch.ExecuteAsync();

}

}

## Task 5: Check your work

Now your application has a full implementation of Azure OpenAI and Azure
Cosmos DB. You can test the application end-to-end by debugging the
solution.

5.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

![A screenshot of a computer program Description automatically
generated](./media/image29.png)

6.  Build the .NET project.

> BashCopy
>
> dotnet build

![](./media/image82.png)

7.  Start the application with hot reloads enabled using dotnet watch.

> BashCopy
>
> dotnet watch run --non-interactive

![](./media/image83.png)

8.  Visual Studio Code launches the in-tool simple browser again with
    the web application running. In the web application, create a new
    chat session and ask the AI assistant a question. Then, close the
    running web application.

&nbsp;

11. Paste the following text in the text box and click on the **Send**
    icon.

**CodeCopy**

**How many wins does it take to promote to the Premier League?**

![](./media/image84.png)

![](./media/image85.png)

12. Paste the following text in the text box and click on the **Send**
    icon.

**CodeCopy**

> **What is Azure OpenAI?**

![](./media/image86.png)

![](./media/image87.png)

13. Close the terminal. Now, open a new terminal.

14. Start the application one more time with hot reloads enabled
    using dotnet watch.

> BashCopy
>
> dotnet watch run --non-interactive

15. Visual Studio Code launches the in-tool simple browser yet again
    with the web application running. For this iteration, observe that
    your chat sessions are persisted between debugging sessions.

![](./media/image88.png)

16. Close the terminal.

## Task 6: Clean up resource group

1.  Open a new browser and enter the following URL in the address bar:
    <https://portal.azure.com/> to open the Azure Portal.

2.  Click on the **Portal Menu**, then select **Resource group.**

![A screenshot of a computer Description automatically
generated](./media/image13.png)

3.  Select the **mslearn-cosmos-openai** resource group.

![](./media/image14.png)

4.  In the Resource group page, navigate to command bar and click on
    **Delete resource group**.

![](./media/image89.png)

5.  In the **Delete Resource group** pane that appears on the right
    side, enter the **resource group name** and click on **Delete**
    button.

![A screenshot of a computer Description automatically
generated](./media/image90.png)

**Summary**

This lab provided a comprehensive guide to building, deploying, and
testing a custom chat application using Blazor, PostgreSQL, and Azure
OpenAI. In this lab, you’ve learned to set up the necessary development
environment, created and designed a Blazor-based chat interface,
configured and connected a PostgreSQL database on Azure, integrated
Azure OpenAI for enhanced functionalities, and finally deployed and
tested the application on Azure. This hands-on experience equipped you
with the skills to develop and manage modern web applications using
cutting-edge technologies and cloud services
