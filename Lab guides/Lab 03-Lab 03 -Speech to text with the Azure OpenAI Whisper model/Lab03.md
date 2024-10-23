# **Lab 03 -Speech to text with the Azure OpenAI Whisper model**

**Introduction**

The OpenAI Whisper model is an encoder-decoder Transformer that can
transcribe audio into text in 57 languages. Additionally, it offers
translation services from those languages to English, producing
English-only output.

Users of Azure AI Speech can leverage OpenAI’s Whisper model in
conjunction with the Azure AI Speech batch transcription API. This
enables customers to easily transcribe large volumes of audio content at
scale. This capability is particularly useful for processing extensive
collections of audio data stored within the Azure platform.

Users of Whisper in Azure AI Speech benefit from existing features
including async processing, [speaker
diarization](https://portal.azure.com/), customization (available soon),
and larger file sizes.

- Large file sizes: Azure AI Speech enhances Whisper transcription by
  enabling files up to 1GB in size and the ability to process large
  amounts of files by allowing you to batch up to 1000 files in a single
  request.

- Time stamps: Using Azure AI Speech, the recognition result includes
  word-level timestamps, providing the ability to identify where in the
  audio each word is spoken.

- Speaker diarization: This is another beneficial feature of Azure AI
  Speech that identifies individual speakers in an audio file and labels
  their speech segments. This feature allows customers to distinguish
  between speakers, accurately transcribe their words, and create a more
  organized and structured transcription of audio files.

## **Task 1: Create Azure OpenAI resource**

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:
     +++https://portal.azure.com/+++
    then press the **Enter** button.

     ![](./media/image1.png)

2.  In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

       ![](./media/image2.png)

3.  Then, enter the password and click on the **Sign in** button**.**

      ![](./media/image3.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

      ![](./media/image4.png)

5.  On the Azure portal menu, click on **+ Create a resource**.

     ![](./media/image5.png)

6.  On the **Create a resource** page, in the search services and
    marketplace field, type **Azure OpenAI**, then press the **Enter**
    button.

      ![](./media/image6.png)

7.  In the Marketplace page, navigate to the Azure OpenAI section, click
    on the Create V chevron button, then click on **Azure OpenAI** as
    shown in the image. (In case, you clicked on the Azure **OpenAI
    section**, then click on the **Create** button on the **Azure OpenAI
    page**).

      ![](./media/new1.png)

8.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.
    |  |  |
    |---|--|
    |Subscription|Select the assigned subscription|
    |Resource group	|Click on Create new> enter +++AOAI-RGXX+++(XX can be a unique number, you can add more digits after XX to make the name unique)|
    |Region|For this lab, you will use a whishper model. This model is currently only available in [certain regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models). Please select a region from this list, In this lab West Europe is using for this resource .|  
    |Name|+++AOAIWestEurope-XXXX+++ (XXXX can be a unique number) |
    |Pricing tier	|Select Standard S0|

     ![](./media/image8.png)

9.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

      ![](./media/image9.png)

10. In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

      ![](./media/image10.png)

11. In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

      ![](./media/image11.png)

12. Wait for the deployment to complete. The deployment will take around
    10-15 minutes.

     ![](./media/new2.png)

13. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

     ![](./media/new3.png)

## Task 2: Retrieve the key and endpoint of Azure OpenAI service

1.  In your **AOAIWestEurope-XXX** page, navigate to the **Resource
    Management** section, and click on **Keys and Endpoints**.

     ![](./media/new4.png)

2.  In **Keys and Endpoints** page, copy **KEY1, KEY 2,** (*You can use
    either KEY1 or KEY2)* and **Endpoint** and paste them on a notepad
    (as shown in the image), and then **Save** the notepad to use the
    information in the upcoming lab.

      ![](./media/image15.png)
 
       ![](./media/image16.png)

***Note:** You will have different KEY values.* *This value can be found
in the **Keys and Endpoint** section when examining your resource from
the Azure portal. You can use either KEY1 or KEY2. Always having two
keys allows you to securely rotate and regenerate keys without causing a
service disruption*.

## **Task 3: Deploy the Whisper model**

1.  On the **AOAIWestEurope-XXX** window, click on **Overview** in the
    left navigation menu, then under the **Get Started** tab, click on
    the **Go to Azure OpenAI Studio** button to open **Azure OpenAI
    Studio** in a new browser.
    ![](./media/new5.png)
    
     ![](./media/new6.png)
2.  In the **Azure OpenAI Studio** window, select  **Deployment** under **Shared resources**.

      ![](./media/new7.png)

3.  In the **Model Deployments** tab, under the **Model deployment** click on **Deploy base model**

      ![](./media/new8.png)

4.  In the **Select a model** box, select **whisper** model and click on the **Confirm** button.

       ![](./media/new9.png)

5.  In the Deploy model whisper tab, click on the **Deploy** button..
     ![](./media/new10.png)

6.  You will see a whisper model.

    ![](./media/new11.png)

7.  In the **Azure OpenAI Studio** window, select **Deployment** under **Shared resources**.

    ![](./media/new12.png)

8.	In the Model Deployments tab, under the Model deployment click on Deploy base model.

    ![](./media/new13.png)

9.	Select the **gpt-35-turbo**, and click on the **Confirm** button.

    ![](./media/new14.png)

10.	In the Deploy model whisper tab, click on the **Deploy** button..

      ![](./media/new15.png)
11.	In the Deployments window, copy Deployment names i.e Whiper, gpt-35-turbo and paste them in a notepad , and then Save the notepad to use the information in 
    the upcoming task.

12.	Click on **Switch to the old look** and click on Azure OpenAI Home icon to go back to the home page.
      ![](./media/new16.png)

## **Task 4: Speech to text using Whisper model**

1.  In Azure OpenAI Studio Home page, under **Welcome to** **Azure
    OpenAI Service**, in **Get started** section, click on the **Whisper
    Speech-to-Text** to open **Azure AI Speech Studio** in a new
    browser.

      ![](./media/image27.png)

     ![](./media/image28.png)

2.  In **Azure AI Speech Studio** Home page, under **Whisper Model in
    Azure OpenAI Service**, in **Try it out** section, select your
    **Resource for Azure OpenAI service** and select
    your **whisperXX** deployment is selected under the **Deployments.**

3.  **Select the check box**- I acknowledge that running this demo will
    incur costs to my Azure resource

      ![](./media/image29.png)

4.  Click on **Browse file** and navigate to **C:\Labfiles \audiofiles**
    location and select **all audio files ,** then click on **Open**
    button.

     ![](./media/image30.png)

     ![](./media/image31.png)

5.  To upload audio files will take 2-3 minutes

     ![](./media/image32.png)

    ![](./media/image33.png)

6.  Under the Audio files pane select **aboutSpeechSdk.wav( or select
    any audio file of your choice)** file and select play button. You
    will receive a response similar to the below screenshot

     ![](./media/image34.png)

7.  Use the **JSON** button to view the code for the interaction.

     ![](./media/image35.png)

## **Task 5: Enhancing Whisper transcriptions: pre- & post-processing techniques**

This notebook offers a guide to improve the Whisper's transcriptions.
We'll streamline your audio data via trimming and segmentation,
enhancing Whisper's transcription quality. After transcriptions, we'll
refine the output by adding punctuation, adjusting product terminology
(e.g., 'five two nine' to '529'), and mitigating Unicode issues. These
strategies will help improve the clarity of your transcriptions, but
remember, customization based on your unique use-case may be beneficial.

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

      ![](./media/image36.png)

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open Folder**.

     ![](./media/image37.png)

3.  Navigate and select **Whisper** notebook from **C:\LabFiles** and
    click on the **Select Folder** button.

      ![](./media/image38.png)

4.  In case, **Do you trust the authors of the files in this folder?**
    dialog box appears, then click on the **Yes, I trust the author**
    button.

      ![](./media/image39.png)

5.  In case, a notification stating **Do you want to install the
    recommended extension for Python?** appears, then click on the
    **Install** button.

      ![](./media/image40.png)

6.  In Visual Studio Code, under **WHISPER**, click on **dotnet**, then
    click on **Whishper_processing_guide.ipynb** notebook.

      ![](./media/image41.png)

8.  Install the Azure Open AI SDK using the command. Click on **Execute
    cell start icon** as shown in the image.

      ![](./media/image42.png)

9.  If prompted to select the environment, then select **.NET
    Interactive** as shown in the image.

     ![](./media/image43.png)

      ![](./media/image44.png)

10. Execute the **2^(nd) cell** by clicking on the **start icon**.

     ![](./media/image45.png)

11. Run this cell, it will prompt you for the apiKey, endPoint, and
    imageGeneration deployment name.

12. Once the resource is created, then add azure openai key and
    endpoint. Beside the comment **\#** **Enter the deployment name you
    chose when you deployed the model** replace the **gpt-35-turbo** and
    add Whisper deployment model as **whisper** . Then, execute the cell
    by clicking on the **start icon**.

      ![](./media/image46.png)

13. In case, a notification stating **enter to API key** appears, then
    click on the **enter**.

      ![](./media/image47.png)

14. In case, a notification stating **enter to Endpoint** appears, then
    click on the **enter**.

     ![](./media/image48.png)

15. In case, a notification stating **chat model** appears, then click
    on the **enter**.

     ![](./media/image49.png)

16. In case, a notification stating **whisper** appears, then click on
    the **enter**.

     ![](./media/image50.png)

17. Import namesapaces and create an instance of OpenAiClient using the
    azureOpenAIEndpoint and the azureOpenAIKey. Then, execute the cell
    by clicking on the **start icon**.

     ![](./media/image51.png)
18.	Import namesapaces and create an instance of OpenAiClient using the azureOpenAIEndpoint and the azureOpenAIKey. Replace the existing code with the below 
    code. Then, execute the cell by clicking on the start icon.
   	```
    OpenAIClient client = new (new Uri(azureOpenAIEndpoint), new AzureKeyCredential(azureOpenAIKey));
    ```
     ![](./media/image52.png)

19. To get started let's import a few different libraries: execute the
    cell by clicking on the **start icon**.

     ![](./media/image53.png)

      ![](./media/image54.png)

20. At times, files with long silences at the beginning can cause
    Whisper to transcribe the audio incorrectly. We'll use \`NAudio\`\`
    to detect and trim the silence. Then, execute the cell by clicking
    on the **start icon**.

     ![](./media/image55.png)

      ![](./media/image56.png)

21. Here, we've set the decibel threshold of -19. You can change this if
    you would like. Then, execute the cell by clicking on the **start
    icon**.

     ![](./media/image57.png)

22. Now that we have audio segments we can create trimmed files to use
    with the Whisper model. Then, execute the cells by clicking on the
    **start icon**.

      ![](./media/image58.png)

     ![](./media/image59.png)

23. This function will add formatting and punctuation to our transcript.
    Whisper generates a transcript with punctuation but without
    formatting.

24. Then, execute the cell by clicking on the **start icon**.

      ![](./media/image60.png)

25. Our audio file is a recording from a fake earnings call that
    includes a lot of financial products. This function can help ensure
    that if Whisper transcribes these financial product names
    incorrectly, that they can be corrected. Then, execute the cell by
    clicking on the **start icon**.

      ![](./media/image61.png)

## **Task 6: Whisper prompting guide**

OpenAI's audio transcription API has an optional parameter called
prompt.

The prompt is intended to help stitch together multiple audio segments.
By submitting the prior segment's transcript via the prompt, the Whisper
model can use that context to better understand the speech and maintain
a consistent writing style.

However, prompts do not need to be genuine transcripts from prior audio
segments. Fictitious prompts can be submitted to steer the model to use
particular spellings or styles.

This notebook shares two techniques for using fictitious prompts to
steer the model outputs:

- **Transcript generation**: GPT can convert instructions into
  fictitious transcripts for Whisper to emulate.

- **Spelling guide**: A spelling guide can tell the model how to spell
  names of people, products, companies, etc. These techniques are not
  especially reliable, but can be useful in some situations.

**Comparison with GPT prompting**

Prompting Whisper is not the same as prompting GPT. For example, if you
submit an attempted instruction like "Format lists in Markdown format",
the model will not comply, as it follows the style of the prompt, rather
than any instructions contained within.

In addition, the prompt is limited to only 224 tokens. If the prompt is
longer than 224 tokens, only the final 224 tokens of the prompt will be
considered; all prior tokens will be silently ignored.

To get good results, craft examples that portray your desired style.

1.  In Visual Studio Code, under **WHISPER**, click on **dotnet**, then
    click on Whisper_prompting_guide.ipynb notebook.

     ![](./media/image62.png)

2.  Install the Azure Open AI SDK using the command. Click on **Execute
    cell start icon** as shown in the image.

     ![](./media/image63.png)

3.  If prompted to select the environment, then select **.NET
    Interactive** as shown in the image.

     ![](./media/image64.png)

     ![](./media/image65.png)

     ![](./media/image66.png)

4.  Run this cell, it will prompt you for the apiKey, endPoint, and
    imageGeneration deployment name.

5.  Once the resource is created, then add azure openai key and
    endpoint. Beside the comment **\#** **Enter the deployment name you
    chose when you deployed the model** replace the **gpt-35-turbo** and
    add Whisper deployment model as **whisper** . Then, execute the cell
    by clicking on the **start icon**.

      ![](./media/image67.png)

6.  In case, a notification stating **enter to API key** appears, then
    click on the **enter**.

      ![](./media/image47.png)

7.  In case, a notification stating **enter to Endpoint** appears, then
    click on the **enter**.

      ![](./media/image48.png)

8.  In case, a notification stating **chat model** appears, then click
    on the **enter**.

     ![](./media/image49.png)

9.  In case, a notification stating **whisper** appears, then click on
    the **enter**.

     ![](./media/image50.png)

10. Import namesapaces and create an instance of OpenAiClient using the
    azureOpenAIEndpoint and the azureOpenAIKey. Then, execute the cell
    by clicking on the **start icon**.
11. Import namesapaces and create an instance of OpenAiClient using the azureOpenAIEndpoint and the azureOpenAIKey. Replace the existing code with the below 
    code. Then, execute the cell by clicking on the start icon.
   	```
    OpenAIClient client = new (new Uri(azureOpenAIEndpoint), new AzureKeyCredential(azureOpenAIKey));
    ```
     ![](./media/image52.png)

     ![](./media/image68.png)

12. Download a few example audio files. Then, execute the cell by
    clicking on the **start icon**.

     ![](./media/image69.png)

13. As a baseline, we'll transcribe an NPR podcast segment. Execute the
    cell by clicking on the **start icon**.

     ![](./media/image70.png)

    ![](./media/image71.png)

14. In the unprompted transcript, 'President Biden' is capitalized.
    However, if we pass in a fictitious prompt of 'president biden' in
    lowercase, Whisper matches the style and generates a transcript in
    all lowercase.

15. Then, execute the cell by clicking on the **start icon**.

     ![](./media/image72.png)

16. Long prompts may be more reliable at steering Whisper. Then, execute
    the cell by clicking on the **start icon**.

     ![](./media/image73.png)

17. Whisper is also less likely to follow rare or odd styles. Execute
    the cell by clicking on the **start icon**.

     ![](./media/image74.png)

18. Whisper may incorrectly transcribe uncommon proper nouns such as
    names of products, companies, or people. We'll illustrate with an
    example audio file full of product names.

19. Then, execute the cell by clicking on the **start icon**.

     ![](./media/image75.png)

20. To get Whisper to use our preferred spellings, let's pass the
    product and company names in the prompt, as a glossary for Whisper
    to follow. Then, execute the cell by clicking on the **start icon**.

     ![](./media/image76.png)

21. Now, let's switch to another audio recording authored specifically
    for this demonstration, on the topic of a odd barbecue.To begin,
    we'll establish our baseline transcript using Whisper. Execute the
    cell by clicking on the **start icon**.

      ![](./media/image77.png)

22. While Whisper's transcription was accurate, it had to guess at
    various spellings. For example, it assumed the friends' names were
    spelled Amy and Sean rather than Aimee and Shawn. Let's see if we
    can steer the spelling with a prompt. Then, execute the cell by
    clicking on the **start icon**.

      ![](./media/image78.png)

      ![](./media/image79.png)

23. One potential tool to generate fictitious prompts is GPT. We can
    give GPT instructions and use it to generate long fictitious
    transcripts with which to prompt Whisper. Then, execute the cell by
    clicking on the **start icon**.

      ![](./media/image80.png)

      ![](./media/image81.png)

24. Whisper prompts are best for specifying otherwise ambiguous styles.
    The prompt will not override the model's comprehension of the audio.
    For example, if the speakers are not speaking in a deep Southern
    accent, a prompt will not cause the transcript to do so.

25. Then, execute the cell by clicking on the **start icon**.
     ![](./media/image82.png)

## **Task 7: Clean up resources**

1.  To Azure OpenAI resource , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

      ![](./media/image83.png)

2.  Click on your resource group.

      ![](./media/image84.png)

3.  In the **Resource group** home page, select the **delete resource
    group** .

      ![](./media/image85.png)

4.  In the Delete a resource group tab, enter your resource group name
    and click on **Delete button**

      ![](./media/image86.png)

5.  On **Delete confirmation** dialog box, click on D**elete** button.

       ![](./media/image87.png)
