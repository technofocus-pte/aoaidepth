# **Use case 02-Developing Intelligent Chat Applications with Azure RAG**

**Introduction**

This sample demonstrates a few approaches for creating ChatGPT-like
experiences over your own data using the Retrieval Augmented Generation
pattern. It uses Azure OpenAI Service to access the ChatGPT model
(gpt-35-turbo), and Azure Cognitive Search for data indexing and
retrieval.

The repo includes sample data so it's ready to try end to end. In this
sample application we use a fictitious company called Contoso
Electronics, and the experience allows its employees to ask questions
about the benefits, internal policies, as well as job descriptions and
roles.

This use case you through the process of developing a sophisticated chat
application using the Retrieval Augmented Generation (RAG) pattern on
the Azure platform. By leveraging Azure OpenAI Service and Azure
Cognitive Search, you will create a chat application that can
intelligently answer questions using your own data. This lab uses a
fictitious company, Contoso Electronics, as a case study to demonstrate
how to build a ChatGPT-like experience over enterprise data, covering
aspects such as employee benefits, internal policies, and job roles.

![](./media/image1.png)

**Objective**

- To install Azure CLI and Node.js on your local machine.

- To assign an owner role to the user.

- To install the Dev Containers extension and set up the development
  environment.

- To deploy a chat application to Azure and use it to get answers from
  PDF files.

- To delete the deployed resources and models.

## Task 1: Install Azure Cli and set the policy scope to Local machine

1.  In your windows search bar, type **PowerShell**. In the
    **PowerShell** dialog box, navigate and click on **Run as
    administrator**. If you see the dialog box - **Do you want to allow
    this app to make changes to your device?** then click on the **Yes**
    button.

      ![](./media/image2.png)

2.  Run the following command to install Azure Cli on the PowerShell

    PowerShell copy
    ```
    winget install microsoft.azd
    ```
     ![](./media/image3.png)

3.  Run the below command to set the policy to **Unrestricted** and
    enter **A** when asked to change the execution policy.
    ```
    Set-ExecutionPolicy Unrestricted
    ```
     ![](./media/image4.png)

## Task 2: Install Node.js

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:+++https://nodejs.org/en/download/+++ then press the
    **Enter** button.
      ![](./media/image5.png)

2.  Select and click on **Windows Installer**.

       ![](./media/image6.png)

3.  **Node-V** file will be downloaded. Click on the downloaded file to
    set up **Node.js**

      ![](./media/image7.png)

4.  In the **Welcome to the Node.js Setup Wizard** window, click on the
    **Next button**.

       ![](./media/image8.png)

5.  In the **End-User License Agreement** window, select **I accept the
    terms in the License agreement** radio button and click on the
    **Next** button.
      ![](./media/image9.png)

6.  In the **Destination Folder** window, click on the **Next** button.

       ![](./media/image10.png)

7.  In the **Custom Setup** window, click on the **Next** button.

     ![](./media/image11.png)

     ![](./media/image12.png)

8.  In Ready to install Node.js window, click on **Install.**

      ![](./media/image13.png)

9.  In **Completing the Node.js Setup Wizard window**, click on the
    **Finish** button to complete the installation process.

       ![](./media/image14.png)

## Task 3: Assign a user as an owner of an Azure subscription

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:+++https://portal.azure.com/+++, then press
    the **Enter** button.

       ![](./media/image15.png)

2.  In the **Microsoft Azure** window, use the **User Credentials** to
    login to Azure.

      ![](./media/image16.png)

3.  Then, enter the password and click on the **Sign in** button**.**

      ![](./media/image17.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

       ![](./media/image18.png)

5.  Type in **Subscriptions** in the search bar and select
    **Subscriptions**.

       ![](./media/image19.png)

6.  Click on your assigned **subscription**.

      ![](./media/image20.png)

7.  From the left menu, click on the **Access control(IAM).**

      ![](./media/image21.png)

8.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

      ![](./media/image22.png)

9.  In the Role tab, select the **Privileged administrator roles** and
    select **Owner** . Click **Next**

     ![](./media/image23.png)
     ![](./media/image24.png)

10. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

     ![](./media/image25.png)
11. On the Select members tab , select your Azure OpenAI credentials and
    click **Select.**

     ![](./media/image26.png)

12. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

     ![](./media/image27.png)
     ![](./media/image28.png)

13. You will see a notification – added as Owner for Azure
    Pass-Sponsorship.

     ![](./media/image29.png)

## Task 4: Run the Docker

1.  In your Windows search box, type Docker , then click on **Docker
    Desktop**.

     ![](./media/image30.png)

2.  Run the Docker Desktop.

     ![](./media/image31.png)

## **Task 5:** **Install Dev Containers extension**

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

      ![](./media/image32.png)

2.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    +++https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers+++ then press the **Enter** button.

     ![](./media/image33.png)

3.  On Dev Containers page, select on Install button.

      ![](./media/image34.png)

4.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

      ![](./media/image35.png)

5.  Open the Visual Studio Code.

      ![](./media/image36.png)

## Task 6: Open development environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    +++https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo+++
    then press the **Enter** button.
    ![](./media/image37.png)

2.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

      ![](./media/image38.png)

3.  To Staring Dev container will take 13-15 min

     ![](./media/image39.png)

4.  Sign in to Azure with the Azure Developer CLI. Run the following
    command on the Terminal

  +++azd auth login+++
     ![](./media/image40.png)

5.  Default browser opens to sign in .Sign in with your Azure
    subscription account.

     ![](./media/image41.png)
 
     ![](./media/image42.png)

6.  Close the browser

     ![](./media/image43.png)

7.  Once logged in, the details of the Azure login are populated in the
    terminal.

      ![](./media/image44.png)

## Task 7: Deploy chat app to Azure

1.  Run the following Azure Developer CLI command to provision the Azure
    resources and deploy the source code

     +++azd up+++

     ![](./media/image45.png)

2.  prompted to enter an environment name, enter the **chatsampleRAG**

    ![](./media/image46.png)
    ![](./media/image47.png)

3.  When prompted, **enter a value for the ‘openAiResourceGroupLocation’
    infrastructure parameter** select **East US2.**

      ![](./media/image48.png)
    
>[!Alert]Note: Select the appropriate near by region ,In this lab **East US2** is taken


4.  When prompted, enter a values for openai resource group locatin
    infrastructure parameter then select **East US 2**
     ![](./media/image49.png)

5.  save the value in the environment for future use (y/N) enter **Y**

     ![](./media/image50.png)

6.  Wait until app is deployed. It may take 35-40 minutes for the
    deployment to complete.

    ![](./media/image51.png)

7.  After the application has been successfully deployed, you see a URL
    displayed in the terminal. Copy the **URL**.

    ![](./media/image52.png)

8.  Open your browser, navigate to the address bar, paste the link. Now,
    resource group will open in a new browser

      ![](./media/image53.png)
      ![](./media/image54.png)
## Task 8: Use chat app to get answers from PDF files

1.  Wait for the web application deployment to complete.

     ![](./media/image55.png)

2.  In the **GPT+Eneterprise data |Sample** web app page, enter the
    following text and click on the **Submit icon** as shown in the
    below image.

 +++What happens in a performence review?+++
     ![](./media/image56.png)
     ![](./media/image57.png)

3.  From the answer, select a **citation**.

      ![](./media/image58.png)

4.  In the right-pane, use the tabs to understand how the answer was
    generated.
    |  |  |
    |---|---|
    |Tab|	Description|
    |Thought process|	This is a script of the interactions in chat. You can view the system prompt (content) and your user question (content).|
    |Supporting content|	This includes the information to answer your question and the source material. The number of source material citations is noted in the Developer settings. The default value is 3.|
    |Citation	|This displays the original page that contains the citation.|

    ![](./media/image59.png)
    ![](./media/image60.png)
    ![](./media/image61.png)

6.  Select the selected tab again to close the pane.

7.  The intelligence of the chat is determined by the OpenAI model and
    the settings that are used to interact with the model.

8.  Select the **Developer settings**.

    ![](./media/image62.png)

   ![](./media/image63.png)

    |  |  |
    |---|----|
    |Setting|	Description|
    |Override prompt template|	This is the prompt that is used to generate the answer.|
    |Retrieve this many search results|	This is the number of search results that are used to generate the answer. You can see these sources returned in the Thought process and Supporting content tabs of the citation.|
    |Exclude category|	This is the category of documents that are excluded from the search results.|
    |Use semantic ranker for retrieval	|This is a feature of Azure AI Search that uses machine learning to improve the relevance of search results.
    Use query-contextual summaries instead of whole documents|	When both Use semantic ranker and Use query-contextual summaries are checked, the LLM uses captions extracted from key passages, instead of all the passages, in the highest ranked documents.|
    |Suggest follow-up questions	|Have the chat app suggest follow-up questions based on the answer.|
    |Retrieval mode|	Vectors + Text means that the search results are based on the text of the documents and the embeddings of the documents. Vectors means that the search results are based on the embeddings of the documents. Text means that the search results are based on the text of the documents.|
    |Stream chat completion responses|	Stream response instead of waiting until the complete answer is available for a respon|


9.  Check the **Suggest follow-up questions** checkbox and ask the same
    question again.

     ![](./media/image64.png)

10.  Enter the following text and click on the **Submit icon** as shown
    in the below image.

+++What happens in a performance review?+++
    ![](./media/image65.png)

10. The chat returned suggested follow-up questions such as the
    following
      ![](./media/image66.png)

11. In the **Settings** tab, deselect **Use semantic ranker for
    retrieval**.

     ![](./media/image67.png)

     ![](./media/image68.png)

12. Enter the following text and click on the **Submit icon** as shown
    in the below image.

+++What happens in a performance review?+++
     ![](./media/image69.png)
     ![](./media/image70.png)

## Task 9: Delete the Resources

1.  To delete Resource group , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

      ![](./media/image71.png)

2.  Click on the sample web app resource group.

     ![](./media/image72.png)

3.  In the resource group home page , select **Delete resource group**
    button.

     ![](./media/image73.png)

4.  On the Delete a resource group tab, enter the resource group and
    click on the **Delete** button.

     ![](./media/image74.png)

**Summary**

In this lab, you’ve learned how to set up and deploy an intelligent chat
application using Azure's suite of tools and services. Starting with the
installation of essential tools like Azure CLI and Node.js, you’ve
configured your development environment using Dev Containers in Visual
Studio Code. You've deployed a chat application that utilizes Azure
OpenAI and Azure Cognitive Search to answer questions from PDF files.
Finally, you’ve deleted the deployed resources to effectively manage
resources. This hands-on experience has equipped you with the skills to
develop and manage intelligent chat applications using the Retrieval
Augmented Generation pattern on Azure.
