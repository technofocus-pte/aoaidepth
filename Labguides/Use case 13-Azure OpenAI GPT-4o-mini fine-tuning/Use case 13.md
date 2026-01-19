# Usecase 13: Deploying and Evaluating Fine-Tuned GPT Models in Azure AI Projects

**Scenario**

You work at a travel-agency (or a company that builds travel-planning
tools). You are building a conversational chat application (a “travel
assistant”) that helps users plan holidays: suggest destinations,
activities, cultural info, weather, visa requirements, etc. You want the
assistant to always speak in a **friendly, inspiring, conversational
tone**, and to **avoid** giving services like booking flights, hotels or
rental cars.

You have access to a pretrained, general-purpose LLM (e.g. gpt-4o via
Azure AI Foundry). But the base model’s responses tend to be generic and
inconsistent in tone. So — instead of relying on prompt-engineering
alone — you decide to **fine-tune** the model on a small dataset of
example chats that reflect exactly how you want the assistant to behave
and respond.

**Introduction**

Large language models (LLMs) can generate high-quality responses using
prompts alone, but achieving consistent tone, behavior, and
domain-specific guidance often requires more than prompt engineering.
Fine-tuning enables you to adapt a powerful base model—such as GPT-4o—to
your unique application needs by training it on example conversations
that demonstrate the tone, style, and constraints you expect.

In this use case, you work for a travel-planning company building a
conversational assistant that offers friendly, inspiring travel
suggestions while avoiding tasks like booking flights or hotels. Through
Microsoft Foundry, you will deploy a base model, fine-tune it using
curated training examples, evaluate its behavior, and compare
performance between the base and fine-tuned versions. This hands-on
exercise demonstrates how fine-tuning creates more reliable, tailored
conversational experiences for real-world applications.

**Objectives**

- Deploy a base GPT-4o model within a Microsoft Foundry project for
  initial testing.

- Fine-tune the model using a small dataset of example conversations
  that define the desired travel-assistant behavior.

- Compare outputs from the base model and the fine-tuned model to
  evaluate improvements in tone, consistency, and constraints.

- Deploy the fine-tuned model and test it in the Azure AI chat
  playground.

- Review fine-tuning metrics and training data to understand how the
  model learns target behaviors.

- Clean up deployed Azure resources to prevent unnecessary cloud costs.

## Task 1: Deploy a model in a Microsoft Foundry project

1.  Open a browser go to +++ https://ai.azure.com +++ and sign in with
    your cloud slice account below.

> Username: <+++@lab.CloudPortalCredential>(User1).Username+++
>
> Password: <+++@lab.CloudPortalCredential>(User1). *TAP*+++
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image1.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

![A login box with a red box and blue box with text AI-generated content
may be incorrect.](./media/image3.png)

> ![A screenshot of a computer error AI-generated content may be
> incorrect.](./media/image4.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

2.  In the home page, in the **Explore models and
    capabilities** section, search for the gpt-4o model and select it.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image6.png)

1.  At the top of the page for the model, select **Use this model**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image7.png)

2.  When prompted to create a project, enter a valid name of project as
    +++**Finetune-project**+++ and expand **Advanced options**.

3.  Select **Customize** and specify the following settings for your
    project. Click on **Create**

    - **Foundry resource**: *A valid name for your Foundry resource*

    - **Subscription**: *Your Azure subscription*

    - **Resource group**: *Create or select a resource group*

    - **Region**: *Select one of the following regions*:\*

      - East US 2

      &nbsp;

      - North Central US

      &nbsp;

      - Sweden Central

\* At the time of writing, these regions support fine-tuning for gpt-4o
models.

![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image8.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

**Note**: Reducing the TPM helps avoid over-using the quota available in
the subscription you are using. 50,000 TPM should be sufficient for the
data used in this exercise. If your available quota is lower than this,
you will be able to complete the exercise but you may experience errors
if the rate limit is exceeded.

4.  When your project is created, the chat playground will be opened
    automatically so you can test your model:

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image10.png)

5.  In the **Setup** pane, note the name of your model deployment; which
    should be **gpt-4o**. You can confirm this by viewing the deployment
    in the **Models and endpoints** page (just open that page in the
    navigation pane on the left).

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image11.png)

6.  In the navigation pane on the left, select **Overview** to see the
    main page for your project.![A screenshot of a computer AI-generated
    content may be incorrect.](./media/image12.png)

## Task 2: Fine-tune a model

Because fine-tuning a model takes some time to complete, you’ll start
the fine-tuning job now and come back to it after exploring the base
gpt-4o model you already deployed.

1.  Navigate to the **Fine-tuning** page under the **Build and
    customize** section, using the menu on the left.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)

2.  Select the button to add a new fine-tune model, select
    the **gpt-4o** model and then select **Next**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

3.  **Fine-tune** the model using the following configuration:

    - **Method of customization**: Supervised

    - **Base model**: *Select the default version of **gpt-4o***

    - **Training data**: *Select the option to **Add training data** and
      upload and apply the* **travel-finetune-hotel.jsonl** *file
      located in **C:\Labfiles** location*

    - **Model suffix**: ft-travel

    - **Seed**: \*Random

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image16.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image18.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image19.png)

3.  Click on **Apply** button

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image20.png)

4.  Submit the fine-tuning details, and the job will start. It may take
    some time to complete. You can continue with the next section of the
    exercise while you wait.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

**Note**: Fine-tuning and deployment can take a significant amount of
time (30 minutes or longer), so you may need to check back periodically.
You can see more details of the progress so far by selecting the
fine-tuning model job and viewing its **Logs** tab.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

4.  Click on **Refresh**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

## Task 3: Chat with a base model

While you wait for the fine-tuning job to complete, let’s chat with a
base GPT 4o model to assess how it performs.

1.  In the navigation pane on the left, select **Playgrounds** and open
    the **Chat playground**.

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image25.png)

2.  Verify your deployed **gpt-4o** base model is selected in setup
    pane.

3.  In the chat window, enter the query +++**What can you do?**+++ and
    view the response.

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image26.png)
>
> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image26.png)

The answers may be fairly generic. Remember we want to create a chat
application that inspires people to travel.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

4.  Update the system message in the setup pane with the following
    prompt:

> +++**You are an AI assistant that helps people plan their travel.**+++

5.  Select **Apply changes** to update the system message.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image28.png)
>
> ![A screenshot of a computer error message AI-generated content may be
> incorrect.](./media/image29.png)

6.  In the chat window, enter the query +++What can you do?+++ again,
    and view the response. 1 As a response, the assistant may tell you
    that it can help you book flights, hotels and rental cars for your
    trip. You want to avoid this behavior.

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image30.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image31.png)

7.  Update the system message again with a new prompt:

+++You are an AI travel assistant that helps people plan their trips.
Your objective is to offer support for travel-related inquiries, such as
visa requirements, weather forecasts, local attractions, and cultural
norms.

You should not provide any hotel, flight, rental car or restaurant
recommendations.

Ask engaging questions to help someone plan their trip and think about
what they want to do on their holiday.+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

8.  Continue testing your chat application to verify it doesn’t provide
    any information that isn’t grounded in retrieved data. For example,
    ask the following questions and review the model’s answers, paying
    particular attention to the tone and writing style that the model
    uses to respond:

+++**Where in Rome should I stay?**+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image33.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

9.  Enter the following text and click on the **Submit icon** as shown
    in the below image.

+++I'm mostly there for the food. Where should I stay to be within
walking distance of affordable restaurants?+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image36.png)

+++What are some local delicacies I should try?+++

+++When is the best time of year to visit in terms of the weather?+++

+++What's the best way to get around the city?+++

## Task 4:Review the training file

The base model seems to work well enough, but you may be looking for a
particular conversational style from your generative AI app. The
training data used for fine-tuning offers you the chance to create
explicit examples of the kinds of response you want.

1.  Open the JSONL file you downloaded previously (you can open it in
    any text editor)

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image19.png)

2.  Examine the list of the JSON documents in the training data file.
    The first one should be similar to this (formatted for readability):

code

{"messages": \[

{"role": "system", "content": "You are an AI travel assistant that helps
people plan their trips. Your objective is to offer support for
travel-related inquiries, such as visa requirements, weather forecasts,
local attractions, and cultural norms. You should not provide any hotel,
flight, rental car or restaurant recommendations. Ask engaging questions
to help someone plan their trip and think about what they want to do on
their holiday."},

{"role": "user", "content": "What's a must-see in Paris?"},

{"role": "assistant", "content": "Oh la la! You simply must twirl around
the Eiffel Tower and snap a chic selfie! After that, consider visiting
the Louvre Museum to see the Mona Lisa and other masterpieces. What type
of attractions are you most interested in?"}

\]}

![A close up of a text AI-generated content may be
incorrect.](./media/image37.png)

Each example interaction in the list includes the same system message
you tested with the base model, a user prompt related to a travel query,
and a response. The style of the responses in the training data will
help the fine-tuned model learn how it should respond.

## Task 5: Deploy the fine-tuned model

When fine-tuning has successfully completed, you can deploy the
fine-tuned model.

1.  Navigate to the **Fine-tuning** page under **Build and
    customize** to find your fine-tuning job and its status. If it’s
    still running, you can opt to continue chatting with your deployed
    base model or take a break. If it’s completed, you can continue.

**Tip**: Use the **Refresh** button in the fine-tuning page to refresh
the view. If the fine-tuning job disappears entirely, refresh the page
in the browser.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

2.  Select the fine-tuning job link to open its details page. Then,
    select the **Metrics** tab and explore the fine-tune metrics.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image39.png)
>
> ![A graph on a computer screen AI-generated content may be
> incorrect.](./media/image40.png)

3.  Select the **Use this model**

> ![A screenshot of a graph AI-generated content may be
> incorrect.](./media/image41.png)

4.  Deploy the fine-tuned model with the following configurations:

    - **Deployment name**: *A valid name for your model deployment*

    - **Deployment type**: Standard

    - **Tokens per Minute Rate Limit (thousands)**: 50K *(or the maximum
      available in your subscription if less than 50K)*

    - **Content filter**: Default

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image42.png)

5.  Wait for the deployment to be complete before you can test it, this
    might take a while. Check the **Provisioning state** until it has
    succeeded (you may need to refresh the browser to see the updated
    status).

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image43.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image44.png)

## Task 6: Test the fine-tuned model

Now that you deployed your fine-tuned model, you can test it like you
tested your deployed base model.

1.  When the deployment is ready, navigate to the fine-tuned model and
    select **Open in playground**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

2.  Ensure the system message includes these instructions:

code

You are an AI travel assistant that helps people plan their trips. Your
objective is to offer support for travel-related inquiries, such as visa
requirements, weather forecasts, local attractions, and cultural norms.

You should not provide any hotel, flight, rental car or restaurant
recommendations.

Ask engaging questions to help someone plan their trip and think about
what they want to do on their holiday.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image46.png)

3.  Test your fine-tuned model to assess whether its behavior is more
    consistent now. For example, ask the following questions again and
    explore the model’s answers:

+++**Where in Rome should I stay?**+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

+++**I'm mostly there for the food. Where should I stay to be within
walking distance of affordable restaurants?**+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

+++**What are some local delicacies I should try?**+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image51.png)

+++**When is the best time of year to visit in terms of the
weather?**+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image52.png)

+++What's the best way to get around the city?+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image53.png)

4.  After reviewing the responses, how do they compare to those of the
    base model?

## Task 7: **Delete resources**

If you’ve finished exploring Foundry, you should delete the resources
you’ve created to avoid unnecessary Azure costs.

1.  In the Azure portal, on the **Home** page, select **Resource
    groups**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image54.png)

2.  Carefully select all resources that you’ve created.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image55.png)

3.  In the Resource group page, navigate to the command bar and click
    on **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

4.  In the **Delete Resources** pane that appears on the right side,
    enter the **delete** and click on **Delete** button.

![A screenshot of a screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image58.png)

**Summary**

In this usecase, you deployed, fine-tuned, and evaluated a custom GPT
model using Microsoft Foundry. You began by experimenting with a base
GPT-4o model to observe its default behavior and limitations. After
preparing and uploading a training dataset, you fine-tuned the model to
reflect the friendly, inspirational tone needed for a travel-planning
assistant—while ensuring it avoids restricted tasks like booking flights
or hotels. Once deployed, you compared the fine-tuned model’s responses
with the base model to confirm improvements in consistency, personality,
and domain alignment.

By completing this exercise, you gained practical experience in
fine-tuning LLMs, deploying them in Azure AI projects, and validating
their behavior—an essential skill for building tailored,
production-ready conversational applications



