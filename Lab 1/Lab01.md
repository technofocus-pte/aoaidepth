# Lab 01: Provisioning Azure OpenAI resource

**Introduction**

> ```Copy
> Azure OpenAI Service brings the generative AI models developed by OpenAI
to the Azure platform, enabling you to develop powerful AI solutions
that benefit from the security, scalability, and integration of services
provided by the Azure cloud platform. The first step to use an Azure
Open AI model is to provision an Azure OpenAI resource. In this lab,
you’ll learn how to get started with Azure OpenAI service by
provisioning Azure OpenAI resource in the Azure portal.

**Objectives**

- To configure VM settings and register necessary Azure resource
  providers.

- To create an Azure OpenAI resource and retrieve key and endpoint.

- To install the required Python libraries.

## **Task 0: Sync Host environment time**

1.  In your VM, navigate and click in the **Search bar**, type
    **Settings** and then click on **Settings** under **Best match**.

> <img src="media/image1.png" style="width:4.65394in;height:3.99955in" />

2.  On Settings window, navigate and click on **Time & language**.

<img src="media/image2.png" style="width:5.92237in;height:5.21371in" />

3.  On **Time & language** page, navigate and click on **Date & time**.

<img src="media/image3.png" style="width:6.5in;height:5.27639in" />

4.  Scroll down and navigate to **Additional settings** section, then
    click on **Syn now** button. It will take 3-5 minutes to syn.

<img src="media/image4.png" style="width:6.5in;height:5.04861in" />

5.  Close the **Settings** window.

<img src="media/image5.png" style="width:6.48341in;height:5.10915in" />

## **Task 1: Register the required Resource providers**

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    [<u>https://portal.azure.com/</u>](https://portal.azure.com/), then
    press the **Enter** button.

> <img src="media/image6.png" style="width:6.49167in;height:4.14167in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Sign in** window, enter the **Username** and click on the
    **Next** button.

<img src="media/image7.png" style="width:4.18371in;height:4.0713in" />

3.  Then, enter the password and click on the **Sign in** button**.**

> <img src="media/image8.png" style="width:4.50872in;height:3.60031in"
> alt="A login screen with a log in box Description automatically generated" />

4.  In **Stay signed in?** window, click on the **Yes** button.

> <img src="media/image9.png" style="width:4.46806in;height:2.98617in"
> alt="Graphical user interface, application Description automatically generated" />

5.  On **Welcome to Microsoft Azure** dialog box, click on **Maybe
    later** button.

> <img src="media/image10.png" style="width:6.5in;height:4.425in"
> alt="A screenshot of a computer Description automatically generated" />

6.  In the Azure portal search box, type **Subscriptions**, then click
    on **Subscriptions** under **Services**.

<img src="media/image11.png" style="width:6.5in;height:3.69444in"
alt="A screenshot of a computer Description automatically generated" />

7.  In the **Subscriptions** page, navigate and click on **Azure Pass –
    Sponsorship**.

<img src="media/image12.png" style="width:6.5in;height:2.57917in"
alt="A screenshot of a computer Description automatically generated" />

8.  In the **Azure Pass – Sponsorship** page left-sided navigation menu,
    navigate to the **Settings** section, then click on the **Resource
    Providers**.

<img src="media/image13.png" style="width:6.5in;height:4.62153in"
alt="A screenshot of a computer Description automatically generated" />

9.  In the **Azure Pass – Sponsorship \| Resource providers** page,
    navigate to the search box and type **Microsoft.Storage**. Select
    the **Microsoft.Storage** under **Provider**, then click on the
    **Register** as shown in the below image.

<img src="media/image14.png" style="width:6.5in;height:4.275in" />

10. You’ll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

<img src="media/image15.png" style="width:2.93483in;height:1.65084in"
alt="A screenshot of a computer Description automatically generated" />

11. In the **Azure Pass – Sponsorship \| Resource providers** page,
    navigate to the search box and type **Microsoft.Security**. Select
    the **Microsoft.Security** under **Provider**, then click on the
    **Register** as shown in the below image.

<img src="media/image16.png" style="width:6.5in;height:4.28333in" />

12. You’ll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

<img src="media/image17.png" style="width:3.57531in;height:1.20844in" />

13. Repeat the steps \#10 and \#11 to register the following Resource
    providers.

    - **Microsoft.CognitiveServices**

    - **Microsoft.Search**

    - **Microsoft.Sql**

    - **Microsoft.Web**

    - **Microsoft.ManagedIdentity**

## **Task 2: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

> <img src="media/image18.png" style="width:6.5in;height:4.69653in" />

2.  Navigate and click on **+ Create a resource**.

> <img src="media/image19.png" style="width:6.5in;height:4.78194in" />

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

> <img src="media/image20.png" style="width:4.77917in;height:4.19021in" />

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

> <img src="media/image21.png" style="width:4.8625in;height:5.056in" />

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

<table>
<colgroup>
<col style="width: 45%" />
<col style="width: 54%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>Subscription</strong></p>
</blockquote></th>
<th><blockquote>
<p>Select the assigned subscription</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p><strong>Resource group</strong></p>
</blockquote></td>
<td>Click on <strong>Create new</strong>&gt; enter```copy
<strong>AOAI-RGXX</strong>(XX can be a unique number, you can add more
digits after XX to make the name unique)</td>
</tr>
<tr class="even">
<td><blockquote>
<p><strong>Region</strong></p>
</blockquote></td>
<td>Select <strong>East US</strong></td>
</tr>
<tr class="odd">
<td><blockquote>
<p><strong>Name</strong></p>
</blockquote></td>
<td>Azure-openai-testXX (XX can be a unique number, you can add more
digits after XX to make the name unique) (here, we entered
<strong>Azure-open-test39</strong>)</td>
</tr>
<tr class="even">
<td><blockquote>
<p><strong>Pricing tier</strong></p>
</blockquote></td>
<td><blockquote>
<p>Select <strong>Standard S0</strong></p>
</blockquote></td>
</tr>
</tbody>
</table>

> <img src="media/image22.png" style="width:6.5in;height:6.46667in" />
>
> <img src="media/image23.png" style="width:6.5in;height:6.41667in" />

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> <img src="media/image24.png" style="width:5.58101in;height:5.89583in" />

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> <img src="media/image25.png" style="width:5.85157in;height:4.8375in" />

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> <img src="media/image26.png" style="width:6.48333in;height:7.51667in" />

9.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

<img src="media/image27.png" style="width:7.13421in;height:3.13265in"
alt="A screenshot of a computer Description automatically generated" />

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

<img src="media/image28.png" style="width:7.09744in;height:3.27083in" />

## **Task 3: Retrieve the key and endpoint of Azure OpenAI service**

1.  In your **Azure-open-testXX \| Model deployments** window, navigate
    to the **Resource Management** section, and click on **Keys and
    Endpoints**.

<img src="media/image29.png" style="width:6.97854in;height:5.55417in" />

2.  In **Keys and Endpoints** page, copy **KEY1, KEY 2,** and
    **Endpoint** values and paste them in a notepad as shown in the
    below image, then **Save** the notepad to use the information in the
    upcoming lab.

<img src="media/image30.png" style="width:6.5in;height:4.26667in" />

<img src="media/image31.png" style="width:6.1448in;height:3.88531in" />

***Note:** You can use either KEY1 or KEY2. Always having two keys
allows you to securely rotate and regenerate keys without causing a
service disruption*.

## Task 4: Install Python libraries and pip updating 

1.  In your windows search bar, type **Command Prompt**. In the
    **Command Prompt App** dialog box, navigate and click on **Run as
    administrator**. If you see the dialog box - **Do you want to allow
    this app to make changes to your device?** then click on the **Yes**
    button.

<img src="media/image32.png" style="width:5.25688in;height:4.8525in" />

2.  Move into the folder where the Python was installed and run the
    **pip** command. i.e., **C:\Users\Admin**

> ```copy
>  python -m pip install --upgrade pip

 <img src="media/image33.png" style="width:6.5in;height:2.075in" />

3.  Run the following command to install Python libraries - openai,
    num2words, matplotlib, plotly, scipy, scikit-learn, pandas, tiktoken

>```Copy
>   pip install openai num2words matplotlib plotly scipy scikit-learn pandas tiktoken

<img src="media/image34.png" style="width:6.5in;height:4.45694in" />

<img src="media/image35.png" style="width:6.5in;height:4.25in" />

4.  Run the below command to install the Transformers package:

> ```Copy
>   pip install transformers

<img src="media/image36.png" style="width:6.5in;height:3.28611in"
alt="Text Description automatically generated" />

**Summary**

In this lab, you’ve set the VM time, registered the necessary Azure
resource providers, then provisioned Azure OpenAI resource. You’ve
learned how to retrieve keys and endpoint information that will be used
for deploying Azure OpenAI models in the upcoming labs. Finally, you’ve
successfully installed Python libraries.

**Please do not delete the Resource group and Azure OpenAI Service
(Azure-openai-testXX). The same Resource group and AOAI service will be
used throughout all the labs.**
