**用例 05 - 使用 Azure RAG 加速器部署和测试对话式 AI 解决方案**

**介紹**

与数据聊天解决方案加速器是一个强大的工具，它结合了 Azure AI
搜索和大型语言模型 （LLM）
的功能来创建对话式搜索体验。此解决方案加速器使用 Azure OpenAI GPT
模型和从数据生成的 Azure AI 搜索索引，该索引集成到 Web
应用程序中，为搜索查询提供自然语言界面，包括语音转文本功能。用户可以拖放文件、指向存储并进行技术设置以转换文档。用户可以在自己的订阅中创建一个具有安全性和身份验证功能的
Web 应用程序。

示例数据说明了如何在金融服务行业 （FSI） 中使用此加速器。

在此方案中，财务顾问正在准备与对 Woodgrove Investments
的新兴市场基金表示兴趣的潜在客户会面。顾问通过更新他们对新兴市场基金总体目标和相关风险的理解来为会议做准备。

现在，财务顾问对 Woodgrove
的新兴市场基金有了更多的了解，他们能够更好地回答客户关于该基金的问题。

注意：此加速器中包含的一些示例数据是使用 AI 生成的，仅用于说明目的。

 在此用例中，您将使用 Azure RAG（检索增强生成）加速器部署和测试对话式 AI
解决方案。此解决方案利用 Azure 强大的 AI 功能（包括 Azure OpenAI 和
Azure AI
搜索）来创建高级对话式搜索体验。在本实验结束时，您将拥有一个功能齐全的
Web
应用程序，该应用程序使用自然语言处理来与数据交互和查询数据。这些实际步骤将指导您完成部署必要的基础设施、验证资源、测试解决方案和清理环境。 ![A
computer screen shot of a diagram AI-generated content may be
incorrect.](./media/image1.png)

**目标**

- 从 Azure 门户中的自定义模板部署必要的基础结构。

- 验证是否已成功部署所有必需的 Azure 资源。

- 通过上传和处理文档以及与 Web 应用程序交互来测试已部署解决方案的功能。

- 删除已部署的资源和模型。

**任务 1：从模板部署基础设施**

1.  打开浏览器，导航到地址栏，然后键入或粘贴以下UR:+++[www.portal.azure.com/+++then](http://www.portal.azure.com/+++then) 然后按
    **Enter** 按钮。

2.  在 **Microsoft Azure** 窗口中，输入您的 **Sign-in** 凭据，然后单击
    **Next** 按钮。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)

3.  然后，输入密码并单击 **Sign in** （登录） 按钮\*\*。\*\*

> ![A screenshot of a login box AI-generated content may be
> incorrect.](./media/image3.png)

4.  在**Stay signed in?** 窗口中，单击 **Yes** 按钮。

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image4.png)

5.  打开新浏览器，并在地址栏中输入以下 URL：
    +++<https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json+++> 以打开
    Azure 门户。

6.  在 **Custom deployment** window 的 **Basics**
    选项卡下，输入以下详细信息以部署自定义模板，然后单击 **Review +
    create**。

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

7.  在 **Review + create** 选项卡上，通过 Validation 后，单击 **Create**
    按钮。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image6.png)

8.  等待部署完成。部署大约需要 17-19 分钟。

9.  单击 **Go to Subscription** 按钮

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

**任务 2：在 Azure 门户中验证已部署的资源**

1.  在 Home （主页） 上，单击 **Resource Groups** （资源组）。

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image8.png)

2.  单击资源组名称  **rg-RAGSolutionXX**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  确保以下资源已成功部署到美国东部区域

    - Azure 应用服务

    - Azure 应用程序见解

    - Azure 机器人

    - Azure OpenAI

    - Azure 文档智能

    - Azure 函数应用

    - Azure 搜索服务

    - Azure 存储帐户

    - Azure 语音服务

    - Azure Database for PostgreSQL - 灵活服务器

    - 密钥保管库

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

![](./media/image11.png) ![A screenshot of a computer AI-generated
content may be incorrect.](./media/image12.png)

**任务 3：测试部署**

1.  在资源组上，然后单击 **Web-** {RESOURCE_TOKEN} **- admin-docker**
    resource name。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)

2.  导航到管理站点

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

3.  在 **Chat with your data Solution Accelerator**
    （与数据聊天解决方案加速器） 页面中，从左侧导航菜单中选择 **Ingest
    Data**（引入数据）。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image16.png)

4.  在 Add documents Batch 窗格中，单击 **Browse file** 并导航到
    **C：\Labfiles \data** 位置并选择**all files，**然后单击 **Open**
    按钮。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  上传文件需要 1-2 分钟

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

6.  单击 **Reprocess all documents in the Azure Storage
    account**（重新处理 Azure 存储帐户中的所有文档）。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image21.png)

7.  在“**Chat with your data Solution
    Accelerator**”页面中，从左侧导航菜单中选择“**Configuration**
    ”，然后选 **check box- Enable post-answering prompt**。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

8.  在配置窗格中，单击 **Save configuration**。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

9.  返回到资源组页面，然后单击 **Storage account** name（存储帐户名称）

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

10. 从左侧导航菜单中，单击 **Containers**。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

11. 在 Containers 页面中，选择 **documents**。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

12. 确保所有文件都应成功部署

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

13. 返回资源组页面

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

14. 在资源组页中，选择“应用服务”作为 **web-{RESOURCE_TOKEN}-docker**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

15. 从可折叠的左侧菜单中的 Settings （设置） 中，选择 Authentication
    （身份验证） ![A screenshot of a computer AI-generated content may
    be incorrect.](./media/image31.png)

16. 单击 Add identify provider（添加身份提供商） ![A screenshot of a
    computer AI-generated content may be
    incorrect.](./media/image32.png)

17. 选择 Microsoft 作为身份提供者，将名称更新为 web-XXXXX-docker-new。
    选择 Client secret expiration duration （客户端密钥过期持续时间）
    作为 90 天，然后单击 Next （下一步）： Permissions. ![A screenshot
    of a computer AI-generated content may be
    incorrect.](./media/image33.png)

18. 单击 Add permission（添加权限）。在列表中向下滚动以展开 Application
    并选择 Application.ReadWrite.All。然后单击 Update 权限。 

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image34.png)

19. 单击 Add now（立即添加）。 

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image35.png)

20. 单击应用程序的 Overview （概述） 页面。等待页面加载，然后单击
    Restart。单击“是”确认重启![A screenshot of a computer AI-generated
    content may be incorrect.](./media/image36.png) ![A screenshot of a
    computer AI-generated content may be
    incorrect.](./media/image37.png)

21. 在 Web
    应用程序**概述**页面上，导航到命令栏并单击**Browse**，它将导航到 Web
    应用程序。

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image38.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

22. 在 **Azure AI** Web 应用程序页面中，输入以下文本，然后单击 **Submit
    图标**，如下图所示。

+++Describe in more detail the risks from market volatility+++ 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

17. 在 **Chat session** 部分，选择 references
    链接，并观察页面右侧搜索文档的详细信息。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

18. 在 **Azure AI** Web 应用程序页面中，输入以下文本，然后单击 **Submit
    图标**，如下图所示。

+++How does Woodgrove Financial handle payroll taxes for employees
outside the U.S.?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png) ![A screenshot of a chat AI-generated
content may be incorrect.](./media/image44.png)

19. 在 **Azure AI** Web 应用程序页面中，输入以下文本，然后单击 **Submit
    图标**，如下图所示。

+++What is FORM 10-K and explain?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image45.png)

**任务 4：删除 Azure OpenAI 资源**

1.  若要 Azure OpenAI 资源，请在 Azure 门户搜索栏中键入 **Resource
    groups** ，导航并单击“**Services**”下的“**Resource groups**”。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

2.  单击您的资源组。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  在资源组的概述页面上，选择 **Delete resource group**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

4.  在右侧显示的 **Delete Resources** 窗格中，输入**resource group
    name**，然后单击 **Delete** 按钮。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

5.  在 **Delete confirmation** 对话框中，单击 **Delete** 按钮。

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image49.png)

**總結：**

此实验室提供使用 Azure RAG 加速器部署对话式 AI
解决方案的实践经验。您已通过使用自定义模板部署所需的基础设施来启动实验室。在验证了各种
Azure 资源的成功部署后，你已通过上传文档并使用 Web
应用程序执行查询和检索信息来测试解决方案。最后，您删除了资源组以有效地管理资源。该实验室演示了如何使用高级
AI 技术增强数据交互和检索。
