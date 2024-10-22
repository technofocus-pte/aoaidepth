# Lab 2 - Generating images using DALL-E and DALL-E3 

**Introduction**

The DALL-E models, currently in preview, generate images from text
prompts that the user provides. This generative AI model presents myriad
opportunities for developers, artists, designers, educators, and others.
It can bridge the gap between what you can imagine and what you can
create. This generative model allows for cross-domain, general
understanding, and zero-shot translation between text prompt and images,
often with a remarkable degree of realism. The main capability of the
Azure OpenAI DALL·E is to take text prompt and generate images.

**Objective**

- To generate image using text in DALL-E playground.

**Important Note:** If you’re facing any **API issues**, please consider
changing the available region
"https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models"

# Exercise 1: Explore image-generation in the DALL-E playground

## Task 1: Create Azure OpenAI resource

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

     ![](./media/image1.png)

2.  Navigate and click on **+ Create a resource**.

     ![](./media/image2.png)

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

      ![](./media/image3.png)

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

    ![](./media/new1.png)

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

    |  |  |
    |----|---|
    |Subscription|	Select the assigned subscription|
    |Resource group|Click on Create new> enter AOAI-RGXX(XX can be a unique number, you can add more digits after XX to make the name unique)|
    |Region|	For this lab, you will use a DALL-E3 model. This model is currently only available in certain regions. Please select a region from this list, In 
     this lab Sweden Central is using for this resource.|
    |Name|	Azure-openai-testXX (XX can be a unique number, you can add more digits after XX to make the name unique) (here, we entered Azure-open-test39)|
    |Pricing tier|	Select Standard S0|

    ![](./media/image5.png)
    ![](./media/image6.png)

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

      ![](./media/image7.png)

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

      ![](./media/image8.png)

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

      ![](./media/image9.png)

9.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

     ![](./media/new2.png)

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

      ![](./media/new3.png)

## Task 2: Retrieve the key and endpoint of Azure OpenAI service

1.  In your **Azure-open-testXX | Model deployments** window, navigate
    to the **Resource Management** section, and click on **Keys and
    Endpoints**.

      ![](./media/new4.png)

2.  In **Keys and Endpoints** page, copy **KEY1, KEY 2,** and
    **Endpoint** values and paste them in a notepad as shown in the
    below image, then **Save** the notepad to use the information in the
    upcoming lab.

      ![](./media/image13.png)

      ![](./media/image14.png)

***Note:** You can use either KEY1 or KEY2. Always having two keys
allows you to securely rotate and regenerate keys without causing a
service disruption*.

## Task 3: Cognitive Services OpenAI Contributor for the Azure OpenAI resource

1.  From the left menu, click on the **Access control(IAM).**

     ![](./media/new5.png)

2.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

      ![](./media/image16.png)

3.  Type the **+++Cognitive Services OpenAI Contributor+++**

      ![](./media/image17.png)

4.  In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

       ![](./media/image18.png)

5.  On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

     ![](./media/image19.png)

6.  In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

     ![](./media/image20.png)

     ![](./media/image21.png)

7.  You will see a notification – added as **Cognitive Services OpenAI Contributor**
    for Azure Pass-Sponsorship.

# Exercise 2: Generate images using DALl-E-3 with Azure OpenAI Service

## Task 1: Generate images using DALL-E-3

1. In **Azure-openai-testXX** page, click on Overview in the left-sided navigation menu, scroll down and click on **Go to Azure OpenAI Studio** button as shown in the below image
   
    ![](./media/new6.png)
   
2.	Wait for the Azure OpenAI studio to launch.
    ![](./media/new7.png)
3.	In the **Azure OpenAI Studio** landing page, navigate and click on **Images** to use the image generation APIs.
    ![](./media/new8.png)
  	
4.	On the **Image playground** ,click on **+ Create a deployment** .
   
    ![](./media/new9.png)
5.	In the select a chat completion model tab select dall-e-3 and click on the Confirm button.

     ![](./media/new10.png)
6.	Click on the **Deploy** button
   
     ![](./media/new11.png)
  	 ![](./media/new12.png)
  	
7.  In **DALL-E playground** window, under **Prompt**, enter your image
    prompt in the text box - **+++An elephant on a skateboard+++** as shown in
    the below image and click on the **Generate** button.

     ![](./media/new13.png)

     ![](./media/new14.png)

8.  Select **View code** near the top of the page, you can use this code
    to write an application that completes the same task.

     ![](./media/new15.png)

     ![](./media/new16.png)

9.  In the **Deployments** window, copy **Deployment name** and paste
    them in a notepad (as shown in the image), and then **Save** the
    notepad to use the information in the upcoming task.

      ![](./media/new17.png)

## Task 2: Install Microsoft .NET SDK

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:++++https://download.visualstudio.microsoft.com/download/pr/9f9ad302-a698-4fab-9765-e313f7e14151/8ad751b6cfc11276b4e2adef4e319db7/dotnet-sdk-8.0.200-win-x64.exe+++, then press the **Enter** button

2.  **Dotnet-sdk-8.0.200-win-x64.exe** file will be downloaded. Click on
    the downloaded file to install the .NET SDK software

     ![](./media/image33.png)

3.  Click on **Install** button.

      ![](./media/image34.png)

4.  On User Account control tab, click on the Yes button

     ![](./media/image35.png)

5.  After installation was successful , click on close button

      ![](./media/image36.png)

## Task 3: Azure DALL·E- 3 image generation example

1.  Click on your Windows search box, type **Visual Studio Code**, then
    click on **Visual Studio Code** under Best match.

      ![](./media/image37.png)

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open File**.

       ![](./media/image38.png)

3.  Navigate and select **DALL-E-3** notebook from **C:\LabFiles** and
    click on the **Open** button.

      ![](./media/image39.png)

4.  In case, **Do you want to allow untrusted files in this window?**
    dialog box appears, then click on the **Open** button.

      ![](./media/image40.png)

5.  Install the Azure Open AI SDK using the command. Click on **Execute
    cell start icon** as shown in the image.

      ![](./media/image41.png)

6.  If prompted to select the environment, then select **.NET
    Interactive** as shown in the image.

      ![](./media/image42.png)
      ![](./media/image43.png)
7.  Execute the **2^(nd) cell** by clicking on the **start icon**.

      ![](./media/image44.png)

8.  Run this cell, it will prompt you for the apiKey, endPoint, and
    imageGeneration deployment name.

9.  Once the resource is created, then add azure openai endpoint. Beside
    the comment **\#Add your key ,#Add your endpoint here** (you’ve
    saved in a notepad in Lab 1\> Task \#3.) and **\#Add your** **image
    deployment name** replace the URL with endpoint URL that you’ve
    saved in a notepad in Exercise 2\>Task \#2. Then, execute the cell
    by clicking on the **start icon**.

      ![](./media/image45.png)
10. In case, a notification stating **enter to API key** appears, then
    click on the **enter**.

      ![](./media/image46.png)

11. In case, a notification stating **enter to Endpoint** appears, then
    click on the **enter**.

      ![](./media/image47.png)
12. In case, a notification stating **image deployment** appears, then
    click on the **enter**.

      ![](./media/image48.png)

13. Import namesapaces and create an instance of OpenAiClient using the
    azureOpenAIEndpoint and the azureOpenAIKey. Then, execute the cell
    by clicking on the **start icon**.

      ![](./media/image49.png)

14. Import namesapaces and create an instance of OpenAiClient using the
    azureOpenAIEndpoint and the azureOpenAIKey. Replace the existing
    code with the below code.** **Then, execute the cell by clicking on
    the **start icon**.

 **+++OpenAIClient client = new (new Uri(azureOpenAIEndpoint), new
 AzureKeyCredential(azureOpenAIKey));+++**

      ![](./media/image50.png)

15. Import SkiaSharp to display images. Then, execute the cell by
    clicking on the **start icon**.

     ![](./media/image51.png)

16. The method returns the SKSurface object, which now contains the
    drawn image. Then, execute the cell by clicking on the **start
    icon**.

     ![](./media/image52.png)

17. With setup and authentication complete, you can now generate images
    on the Azure OpenAI service and retrieve them from the returned
    URLs.

18. The first step in this process is to actually generate the images.
    Then, execute the cell by clicking on the **start icon**.

      ![](./media/image53.png)

19. Create the image using the response and SkiaSharp and display it.
    Then, execute the cell by clicking on the **start icon**.

      ![](./media/image54.png)

## Task 4: Clean up resources

To avoid incurring unnecessary Azure costs, you should delete the
resources you created in this quick start if they're no longer needed.
To manage resources, you can use the [Azure
portal](https://portal.azure.com/?azure-portal=true).

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

      ![](./media/image55.png)

2.  Click on the resource group that you’ve created.

     ![](./media/image56.png)

3.  In the **Resource group** home page, select the **delete resource
    group** .

      ![](./media/image57.png)

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “resource group name” to confirm deletion**
    field, then click on the **Delete** button.

     ![](./media/image58.png)

5.  On **Delete confirmation** dialog box, click on **Delete** button.

      ![](./media/image59.png)

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

      ![](./media/image60.png)

**Summary**

In this lab, you’ve used DALL-E playground and generated images using
text. Then, you’ve used Azure Dalle-E image generation code in Visual
Studio for generating images with the Azure OpenAI service and viewed
the downloaded image in Visual Studio as well as browser.
