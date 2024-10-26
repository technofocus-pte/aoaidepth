# **Use case 03 -Deploying and Testing a Conversational AI Solution with Azure RAG Accelerator**

**Introduction**

The *Chat with your data* Solution accelerator is a powerful tool that
combines the capabilities of Azure AI Search and Large Language Models
(LLMs) to create a conversational search experience. This solution
accelerator uses an Azure OpenAI GPT model and an Azure AI Search index
generated from your data, which is integrated into a web application to
provide a natural language interface, including speech-to-text
functionality, for search queries. Users can drag and drop files, point
to storage, and take care of technical setup to transform documents.
There is a web app that users can create in their own subscription with
security and authentication.

The sample data illustrates how this accelerator could be used in the
financial services industry (FSI).

In this scenario, a financial advisor is preparing for a meeting with a
potential client who has expressed interest in Woodgrove Investments’
Emerging Markets Funds. The advisor prepares for the meeting by
refreshing their understanding of the emerging markets fund's overall
goals and the associated risks.

Now that the financial advisor is more informed about Woodgrove’s
Emerging Markets Funds, they're better equipped to respond to questions
about this fund from their client.

Note: Some of the sample data included with this accelerator was
generated using AI and is for illustrative purposes only.

 In this use case, you will deploy and test a Conversational AI Solution
using the Azure RAG (Retrieval-Augmented Generation) Accelerator. This
solution leverages Azure's powerful AI capabilities, including Azure
OpenAI and Azure AI Search, to create an advanced conversational search
experience. By the end of this lab, you will have a fully functional web
application that uses natural language processing to interact with and
query your data. The practical steps will guide you through deploying
the necessary infrastructure, verifying the resources, testing the
solution, and cleaning up the environment.
     ![](./media/image1.png)

**Objectives**

- To deploy the necessary infrastructure from a custom template in the
  Azure portal.

- To verify that all required Azure resources have been deployed
  successfully.

- To test the functionality of the deployed solution by uploading and
  processing documents and interacting with the web application.

- To delete the deployed resources and models.

## Task 1: Deploy infrastructure from template

1.  Open your browser, navigate to the address bar, and type or paste
    the following UR:+++www.portal.azure.com/+++then press the
    **Enter** button.

2.  In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

       ![](./media/image2.png)

3.  Then, enter the password and click on the **Sign in** button**.**

      ![](./media/image3.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

     ![](./media/image4.png)

5.  Open a new browser and enter the following URL in the address bar:
    +++https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json+++
    to open the Azure Portal.

6.  On **Custom deployment** window, under the **Basics** tab, enter the
    following details to deploy the custom template and then click on
    **Review + create.**

     |   |   |
     |---|---|
     |Environment Name|	Enter RAGSolutionXX(XXXcan be a unique name)|
     |Location|	Select near by available region, in this lab East US is using for this resource|

      ![](./media/image5.png)

7.  On **Review + create** tab, once the Validation is Passed, click on
    the **Create** button.

     ![](./media/image6.png)

8.  Wait for the deployment to complete. The deployment will take around
    17-19 minutes.

9.  Click on the **Go to Subscription** button

      ![](./media/image7.png)

## Task 2: Verify deployed resources in the Azure portal

1.  On the Home page, click on **Resource Groups**.

     ![](./media/image8.png)

2.  Click on your resource group name **rg-RAGSolutionXX**

      ![](./media/image9.png)

3.  Make sure the below resource got deployed successfully into East US
    region

     - Azure App Service
     
     - Azure Application Insights
     
     - Azure Bot
     
     - Azure OpenAI
     
     - Azure Document Intelligence
     
     - Azure Function App
     
     - Azure Search Service
     
     - Azure Storage Account
     
     - Azure Speech Service

    ![](./media/image10.png)

    ![](./media/image11.png)

## Task 3: Testing the deployment

1.  On the resource group and click on **Web-** {RESOURCE_TOKEN} **-
    admin-docker** resource name.

      ![](./media/image12.png)

2.  Navigate to the admin site
    https://web-{RESOURCE_TOKEN}-admin.azurewebsites.net/

      ![](./media/image13.png)

      ![](./media/image14.png)

3.  In **Chat with your data Solution Accelerator** page, from the left
    navigation menu select **Ingest Data.**

      ![](./media/image15.png)

4.  In the Add documents Batch pane, Click on **Browse file** and
    navigate to **C:\Labfiles \data** location and select **all files,**
    then click on **Open** button.

     ![](./media/image16.png)

     ![](./media/image17.png)

5.  To upload files will take 1-2 minutes

     ![](./media/image18.png)

6.  Click on the **Reprocess all documents in the Azure Storage
    account.**

      ![](./media/image19.png)

      ![](./media/image20.png)

7.  In **Chat with your data Solution Accelerator** page, from the left
    navigation menu select **Configuration** and select the **check box-
    Enable post-answering prompt.**

      ![](./media/image21.png)

8.  In the configuration pane , Click on the **Save configuration.**

     ![](./media/image22.png)

     ![](./media/image23.png)

9.  Go back to the resource group page and click on **the Storage
    account** name

      ![](./media/image24.png)

10. From the left navigation menu, click on **Containers.**

     ![](./media/image25.png)

11. In the Containers page, select **documents**.

    ![](./media/image26.png)

12. Make sure all the files should be deployed successfully

     ![](./media/image27.png)

13. Go back to the resource group page

     ![](./media/image28.png)

14. In the resource group page, select App service as
    **web-{RESOURCE_TOKEN}-docker**

      ![](./media/image29.png)

15. On Web App **Overview** page, navigate to the command bar and click
    on **Browse**, it will navigate you to the web application.

      ![](./media/image30.png)

      ![](./media/image31.png)

16. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

 +++Describe in more detail the risks from market volatility+++
      ![](./media/image32.png)
      ![](./media/image33.png)

17. In the **Chat session** section, select the references link and
    observe the details of search document on right side of the page.

     ![](./media/image34.png)

18. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

+++How does Woodgrove Financial handle payroll taxes for employees outside the U.S.?+++
      ![](./media/image35.png)
      ![](./media/image36.png)

19. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

+++What is FORM 10-K and explain?+++
     ![](./media/image37.png)

## **Task 4: Delete Azure OpenAI Resource**

1.  To Azure OpenAI resource , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

      ![](./media/image38.png)

2.  Click on your resource group.

       ![](./media/image9.png)

3.  On an overview page of resource group Select the **Delete resource
    group**

      ![](./media/image39.png)

4.  In the **Delete Resources** pane that appears on the right side,
    enter the **resource group name** and click on **Delete** button.

      ![](./media/image40.png)

5.  On **Delete confirmation** dialog box, click on D**elete** button.

      ![](./media/image41.png)

**Summary**:

This lab provides hands-on experience in deploying a Conversational AI
Solution using the Azure RAG Accelerator. You’ve started the lab by
deploying the required infrastructure using a custom template. After
verifying the successful deployment of various Azure resources, you’ve
tested the solution by uploading documents and using the web application
to perform queries and retrieve information. Finally, you’ve deleted the
resource group to manage the resources efficiently. This lab
demonstrated how to enhance data interaction and retrieval using
advanced AI technologies.
