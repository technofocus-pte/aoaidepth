**ラボ07:セマンティックアンサーを使用してQ&Aの実装**

**紹介**

OpenAI対応のドキュメント検索用のシンプルなWebアプリケーション。このリポジトリでは、Azure
OpenAI Service
を使用して、ドキュメントから埋め込みベクトルを作成します。ユーザーの質問に答えるために、最も関連性の高いドキュメントを取得し、GPT-3を使用して質問に一致する回答を抽出します。

![建築](./media/image1.png)

**目標**

- Azure AI Studio でチャットと埋め込みモデルをデプロイするため。

- App Service、Search Service、Form Recognizer
  などの必要なリソースをデプロイするためのカスタム
  テンプレートを使用する。

- aoaichatsearch-site Web アプリをデプロイし、Azure OpenAI
  対応のドキュメント検索、テキスト要約、および会話データ抽出を実行します。

- デプロイされたリソースとモデルを削除します。

## **タスク 1: Azure OpenAI リソースを作成する**

1.  Azure ポータルのホームページで、
    **次のイメージに示すように、Microsoft Azure コマンド
    バーの左側にある 3 本の水平バーで表される** Azure ポータル
    メニューをクリックします。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image2.png)

2.  **+ Create a resource をクリックします**。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image3.png)

3.  \[ **Create a resource**\] ページの
    **\[検索サービスとマーケットプレース** \] 検索バーに「 **Azure
    OpenAI**」と入力し、 **Enter** キーを押します。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image4.png)

4.  \[Marketplace**\]** ページで、\[**Azure
    OpenAI**\]セクションに移動し、\[Create\]ボタンのドロップダウンをクリックして、図に示すように**\[Azure
    OpenAI**\]を選択します。(すでに**Azure OpenAI**
    タイルクリックしている場合は、、**Azure OpenAI ページの**
    \[**Create\] ボタンをクリックします**。

> ![](./media/image5.png)

5.  \[**Create Azure OpenAI**\] ウィンドウの \[**Basics**\]
    タブで、次の詳細を入力し、\[**Next\]** ボタンをクリックします。

[TABLE]

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image6.png)

6.  \[**Network\]**
    タブで、すべてのラジオボタンをデフォルトの状態のままにして、\[**Next\]**ボタンをクリックします。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image7.png)

7.  **\[Tags\]**
    タブで、すべてのフィールドをデフォルトの状態のままにして、\[**Next\]**
    ボタンをクリックします。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image8.png)

8.  **「Review+submit**」タブで、懸賞が合格したら「**Create」**ボタンをクリックします。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image9.png)

9.  デプロイが完了するまで待ちます。デプロイには約 **2 -3**
    分かかります。

10. **Microsoft.CognitiveServicesOpenAI**
    ウィンドウで、デプロイが完了したら、\[**Go to resource\]**
    ボタンをクリックします。

> ![](./media/image10.png)

11. **Azure-open-testXX |\[ Model
    deployments**ウィンドウで、\[**Resource Management**\]
    セクションに移動し、\[**Keys and Endpoints\] をクリックします**。

![](./media/image11.png)

12. **\[Keys and Endpoints\]** ページで、次の図に示すように **KEY1、KEY
    2、Endpoint**の値をコピーしてメモ帳に貼り付け、
    メモ帳を保存して今後のラボで情報を使用します。

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image12.png)

## **タスク 2: チャット モデルと埋め込みモデルのデプロイ**

1.   **Azure-openai-testXX** ページで、左側のナビゲーション メニューの
    **\[Overview**\]
    をクリックし、下にスクロールして、**次の図に示すように** \[**Explore
    Azure AI Foundry portal**\] ボタンをクリックします。

> ![](./media/image13.png)

2.  Azure OpenAI スタジオが起動するのを待ちます。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image14.png)

3.  **Azure AI Foundry** |Azure OpenAI Studio
    ホームページで、左側のナビゲーション メニューから \[**Deployment**\]
    を選択します**。**

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image15.png)

4.  \[**Deployment\]** ウィンドウで、**+Deploy
    modelを**ドロップダウンし、 \[**Deploy base model\] を選択します。**

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image16.png)

5.  \[**Select a model**\] ダイアログ ボックスで、gpt-4
    をナビゲートして慎重に選択し、\[**Confirm\]**
    ボタンをクリックします。

![](./media/image17.png)

6.  **Model version**として **0125-Preview を選択し、Deployment
    type**として **Standard、デプロイ名 フィールドで** gpt-4
    **と入力し、Create**ボタンをクリックします。

> ![](./media/image18.png)

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image19.png)

7.  \[**Deployments\]** ウィンドウで、**+Deploy
    modelを**ドロップダウンし、**Deploy base modelを選択します。**

> ![](./media/image20.png)

8.  \[**Select a model\]** ダイアログ ボックスで、移動して
    **text-embedding-ada-002** を慎重に選択し、\[**Confirm\]**
    ボタンをクリックします。

![](./media/image21.png)

9.  \[**Deploy model**\] ダイアログ ボックスの**Deployment
    nameに**「+++text-embedding-ada-002+++**」と入力し、Deployment
    typeとして** \[**Standard\] を選択し**、\[**Deploy\]**
    ボタンをクリックします。

![](./media/image22.png)

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image23.png)

## **タスク 3: Azure Cognitive Search を使用して Azure にデプロイする (Web アプリ + バッチ処理)**

1.  エッジブラウザを開き、アドレスバーに移動して、次のURLを入力または貼り付けます：
    <https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fruoccofabrizio%2Fazure-open-ai-embeddings-qna%2Fmain%2Finfrastructure%2Fdeployment_ACS.json>
    、 **Enter** ボタンを押します。

![](./media/image24.png)

2.  \[**Custom deployment**\] ウィンドウの \[**Basics**\]
    タブで、次の詳細を入力してカスタム テンプレートを展開
    し、\[**Review + create\] をクリックします。**

[TABLE]

![](./media/image25.png)

![](./media/image26.png)

3.  「**Review +
    create**」タブで、懸賞が合格したら、「**Create」**ボタンをクリックします。

![](./media/image27.png)

4.  デプロイが完了するまで待ちます。デプロイには約 15-17 分かかります。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image28.png)

5.  \[**Go to resource group\]**ボタンをクリックします。

> ![](./media/image29.png)

## **タスク 4: Web アプリケーションを使用した Azure OpenAI 対応ドキュメント検索**

1.  **aoaiXXX-RG** リソース グループ ウィンドウの **\[Resources**\]
    タブで、**App Service** - **aoaaichatsearch-site**
    に移動してクリックします。

![](./media/image30.png)

2.  **aoaichatsearch-site**
    Webアプリ**のOverview** ページで、コマンドバーに移動して\[**Browse**\]をクリックすると**、**Webアプリケーションに移動します。

![](./media/image31.png)

3.  Web アプリケーションのデプロイが完了するまで待ちます。デプロイには約
    **10 -15** 分かかります。

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image32.png)

4.  Web アプリケーションのホームページで、デプロイの状態を確認するには、
    Microsoft の下にある **\[Check deployments**\]
    ボタンをクリックします。

![](./media/image33.png)

5.  デプロイ状況の確認には、約 5-6 分かかる場合があります。

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image34.png)

![](./media/image35.png)

6.  Web アプリのホームページで、左側の \[**Add Document**\]
    に移動してクリックし、データを追加します。

![](./media/image36.png)

7.  \[**Add Document**\]パネルで、\[**Browse
    files**\]ボタンをクリックして、ナレッジベースに追加する必要があるドキュメントをアップロードします。

![](./media/image37.png)

8.  VM 内の **C:\Labfiles\Contoso Electronics** の場所に移動し、
    \[Benefit_Options.pdf\] **を選択して** \[**Open\]**
    ボタンをクリックします。

![](./media/image38.png)

9.  \[**Browse files**\] をもう一度クリック**し、**VM 内の
    **C:\Labfiles\Contoso Electronics** の場所に移動して
    \[employee_handbook.pdf**\] を選択し**、\[**Open**\]
    ボタンをクリックします。

![](./media/image39.png)

![](./media/image40.png)

10. 同様に、**Northwind_Health_Plus_Benefits_Details.pdf**と**Northwind_Standard_Benefits_Details.pdfを追加します**

![](./media/image41.png)

![](./media/image42.png)

11. アップロードされたデータはナレッジ ベースに追加され、約 5 分から 7
    分かかります。

12. \[**Document
    Management\]をクリックして**、ファイルが正常にアップロードされたかどうかを確認します。

![](./media/image43.png)

![](./media/image44.png)

13. \[**Index Management\]
    をクリックして**、ファイル、キー、およびソースを確認します。

![](./media/image45.png)

14. 次に、\[**Chat**\]をクリックします **。**

![](./media/image46.png)

15. \[**Chat session\]**
    セクションで、次のプロンプトを入力し、\[**Enter\]
    ボタンを押して**応答を表示します。

**ユーザー**: **what is the employee's portion of the healthcare cost
from each paycheck in Contoso Electronics**

![](./media/image47.png)

![](./media/image48.png)

16. \[**Chat session\]** セクションで、\[**Clear
    chat\]**ボタンをクリックします。

![](./media/image49.png)

17. \[**Chat session** **\]**
    セクションで、次のプロンプトを入力し、\[**Enter\]
    ボタンを押して**応答を表示します。

> **ユーザー**: **How do I file a complaint or appeal with Northwind
> Health Plus?**

![](./media/image50.png)

18. \[**Chat session** **\]** セクションで、\[**Clear
    chat\]**ボタンをクリックします。

![](./media/image51.png)

19. \[**Chat session\]** セクションで、次のプロンプトを入力します。
    次に**、Enter**ボタンを押して応答を表示します。

**ユーザー**: **Does my plan covers my eye exams?**

![](./media/image52.png)

20. 左側の「**Utils-Document Summary」をクリックします**。

![](./media/image53.png)

21. \[**Summarization\]** セクションで、\[**Basic Summary\]**
    ラジオボタンを選択します**。**

![](./media/image54.png)

22. \[Summarization**\]** ウィンドウの \[**Enter some text to
    summarize**\] セクションのメッセージ
    ボックスで、現在のテキストを次のように置き換え、\[**Summarize\]**
    ボタンをクリックします。

It’s been six months since we reinvented search with [the new AI-powered
Bing and
Edge](https://blogs.microsoft.com/blog/2023/02/07/reinventing-search-with-a-new-ai-powered-microsoft-bing-and-edge-your-copilot-for-the-web/).
In that short time, you’ve engaged in so many unique and creative ways;
to date we’ve seen over 1 billion chats and over 750 million images fill
the world of Bing! We’ve also seen nine consecutive quarters of growth
on Edge, meaning we’re more able than ever to bring our best-in-class AI
experiences to users across the web.

![](./media/image55.png)

23. 入力したテキストの概要を確認します。

![](./media/image56.png)

24. サマリーの結果を確認したら、\[**Clear summary\]**
    ボタンをクリックします。

![](./media/image57.png)

25. 次に、上にスクロールして、\[**Bullet
    Points\]**ラジオボタンを選択します。**Enter some text to
    summarize**セクションで、メッセージボックスに現在のテキストを次のように置き換えて、\[**Summarize**\]ボタンをクリックします。

Microsoft has made its Azure OpenAI Service generally available,
bringing the enterprise generative AI tools out of its invite-only
program. Now any customers who meet Microsoft’s standards can access the
professional versions of OpenAI’s large language model GPT-3.5 and the
related text-to-image tool DALL-E 2, computer programming assistant
Codex, and the popular ChatGPT chatbot interface for the LLM.

Microsoft launched the Azure OpenAI Service with an eye toward offering
businesses a way to develop apps without coding, write reports, and put
together marketing content. The scope has grown since then to encompass
new facets of the OpenAI’s models, including chat and visuals. Those
interested in the tools have to explain how they will use the AI tools
and agree to Microsoft’s ethical guidelines in their application for
access. The decision to widen the Azure OpenAI Service’s availability
arrives in tandem with Microsoft’s plans to integrate ChatGPT and DALL-E
into its Office suite, Bing search engine, and other consumer products.
Azure OpenAI Service followed earlier experiments to integrate GPT-3
into Microsoft projects like the low-code Power Apps programming tool
and the GitHub Copilot programming assistant.

![](./media/image58.png)

26. 概要の結果が箇条書きの形式で表示されます。

![](./media/image59.png)

27. 左側の \[**Utils-Conversation Data Extraction\] をクリックします**。

![](./media/image60.png)

28. **Conversation data extraction**ウィンドウで、\[**Execute tasks\]
    をクリックし、\[**OpenAI 結果**\] の下に応答を表示します**。

![](./media/image61.png)

29. エージェントとユーザー間の会話から抽出されたデータを確認します。

![](./media/image62.png)

## タスク 5: デプロイされたリソースとモデルの削除

1.  デプロイされたリソースを削除するには、**Azure portal のホーム**
    ページに移動し、 \[**Resource groups\] をクリックします**。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image63.png)

2.  \[リソース グループ\] ページで、リソースグループを選択します。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image64.png)

3.  **Resource groupの**ホーム
    ページで、すべてのリソースを選択し、**deleteをクリックします**

4.  右側に表示される**\[**リソースの削除\]ペインで、\[**削除を確認するために「delete」と入力し**、\[**Delete\]**ボタンをクリックします。

5.  **Delete confirmation**ダイアログボックスで、\[
    **Delete**\]ボタンをクリックします。

> ![コンピュータエラーのスクリーンショット
> 説明が自動的に生成される](./media/image65.png)

6.  ベルのアイコンをクリックすると、通知が表示されます

**概要**

Azure AI Studio に gpt-4 チャット モデルと text-embedding-ada-002
埋め込みモデルをデプロイし、カスタム
テンプレートを使用して必要なリソースをデプロイしました。aoaichatsearch-site
Web アプリに非構造化ドキュメントをアップロードし、チャット
セッションで正確な情報を抽出しました。サンプル
テキストから基本概要と箇条書き概要を生成し、会話からデータを抽出しました。ラボの最後に、Azure
OpenAI
リソースを効率的に管理するために、リソースとモデルを削除しました。

**重要な注意: リソース
グループは削除しないでください。削除すると、次のラボに進んだり、新しいリソース
グループを作成したりできなくなります。**

**Azure OpenAI Service (Azure-openai-testXX)
は削除しないでください。すべてのラボで同じサービスが使用されます。**
