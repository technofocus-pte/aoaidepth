# ユース ケース 11 - Azure AI Foundry と検索の統合を使用したカスタム AI エージェントの作成

**所要時間: 45 分**

## 目的

このラボの目的は、Azure AI サービスと検索統合を使用して AI
を利用したエージェントを構築する方法を参加者にガイドすることです。参加者は、主要なコンポーネントを構成、統合、テストして、インテリジェントな情報検索とインタラクションが可能な機能エージェントを作成し、ユーザーエクスペリエンスと生産性を向上させる方法を学びます。

## 解決

このラボでは、Azure AI
サービスと高度な検索機能を統合して、堅牢でインテリジェントなソリューションを作成することに重点を置いています。AI
を活用したエージェントの構成、シームレスなデータ取得、コンテキストに応じた応答の提供に重点を置いています。AIと検索の統合を活用することで、ソリューションは、ワークフローの合理化、意思決定の改善、直感的で効率的なインタラクションによるユーザーエンゲージメントの強化を目指しています。

## タスク 1: Azure AI Search リソースを作成する

1.  Web ブラウザーで <https://portal.azure.com>で Azure portal を開き、
    Office 365 管理者の資格情報を使用してサインインします。

> ![](./media/image1.png)

2.  ホーム ページで、 **+ Create a resource** を選択し、**Azure AI
    Search** を検索します。次に **、次の設定で新しい Azure AI Search
    リソース**を作成します。

    - **サブスクリプション**: *Azure サブスクリプションを選択します。*

    - **リソースグループ**:*リソースグループを選択または作成し、ここでは**RG4OpenAIを選択します***

    - **サービス名**:
      *一意のサービス名を入力します。ここでは**、copilotXXXX
      という名前を付けます。***

    - ***ロケーション:
      次の地域のいずれかからランダムに選択し、ここでは**Canada
      East**を選択します***

      - Australia East

      &nbsp;

      - Canada East

      &nbsp;

      - East US

      &nbsp;

      - East US 2

      &nbsp;

      - France Central

      &nbsp;

      - Japan East

      &nbsp;

      - North Central US

      &nbsp;

      - Sweden Central

      &nbsp;

      - Switzerland

    - **価格レベル**: Standard

    - 「Review+create**」をクリックし、「Create**」をクリックします**。**

> ![](./media/image2.png)
>
> ![](./media/image3.png)
>
> ![](./media/image4.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image5.png)
>
> 後で、Azure AI Search リソースと同じリージョンに Azure AI Hub (Azure
> OpenAI サービスを含む) を作成します。Azure OpenAI
> リソースは、リージョンのクォータによってテナントレベルで制約されます。リストされているリージョンには、この演習で使用するモデルタイプのデフォルトのクォータが含まれています。リージョンをランダムに選択すると、他のユーザーとテナントを共有しているシナリオで、1
> つのリージョンがクォータ制限に達するリスクが軽減されます。演習の後半でクォータ制限に達した場合は、別のリージョンに別の
> Azure AI hubを作成することが必要になる可能性があります。

3.  Azure AI Search リソースのデプロイが完了するまで待ちます。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image6.png)

## タスク 2: Azure AI プロジェクトを作成する

1.  Web ブラウザーに、https://ai.azure.comでAzure [AI Foundry
    ポータル](https://ai.azure.com/)を開き、資格情報を使用してサインインします。

2.  ホーム ページで、 **\[+ Create project\] を選択します**。

> ![](./media/image7.png)

3.  **Create
    projectウィザードで**、プロジェクト名に**「ProjectXXXX**」と入力し、\[**Customize\]
    をクリックします**。

> ![](./media/image8.png)

4.  **\[Customize\] で**、Azure AI Search
    リソースに接続し、次の詳細を入力して \[**Next**\]
    を選択し、構成を確認します。

    - **ハブ名**: ***hubXXXX***

    - **Azure サブスクリプション**: ユーザーの*Azure サブスクリプション*

    - **リソース グループ**: **RG4OpenAI**

    - **ロケーション**: *Azure AI Search リソースと同じ場所 (**Canada
      East)***

    - **Azure AI Services または Azure OpenAI を接続する**: (新規)
      *選択したハブ名で自動入力*

    - **Azure AI Search の接続**: *Azure AI Search リソース
      **copilotXXXXを選択します***

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image9.png)

5.  \[**Next\] を選択し、\[Create\]**
    を選択し、プロセスが完了するまで待ちます。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image10.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image11.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image12.png)

## タスク 3: モデルのデプロイ

ソリューションを実装するには、次の 2 つのモデルが必要です：

- 効率的なインデックス作成と処理のためにテキストデータをベクトル化するための埋め込みモデル。

- データに基づいて質問に対する自然言語による回答を生成できるモデル。

1.  Azure AI Foundry ポータルのプロジェクトで、左側のナビゲーション
    ウィンドウの \[**My assets**\] で、 \[**Models + endpoints\]**
    ページを選択します。

> ![](./media/image13.png)

2.  \[**Manage deployments of your models and services page\]
    ページで、\[** **+ Deploy model\]** をクリックし、\[**Deploy base
    model\] を選択します。**

> ![](./media/image14.png)

3.  \[**Select a model**\] ページで、**text-embedding-ada-002**
    モデルを検索して選択し、\[**Confirm**\] をクリックします**。**

> ![](./media/image15.png)

4.  \[**Deploy model text-embedding-ada-002\] ペインで** \[**Customize\]
    をクリックし** 、モデルのデプロイ ウィザードに次の詳細を入力します。

> ![](./media/image16.png)

- **Deployment name**: text-embedding-ada-002

- **Deployment type**: Standard

- **Model version**: *Select the default version*

- **AI resource**: *Select the resource created previously*

- **Tokens per Minute Rate Limit (thousands)**: 5K

- **Content filter**: DefaultV2

- **Enable dynamic quota**: Disabled

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image17.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image18.png)

5.  前の手順を繰り返して、 **デプロイ名が gpt-35-turbo-16k の
    gpt-35-turbo-16k モデルを**デプロイします。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image19.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image20.png)
>
> **注**: TPM (Tokens Per Minute)
> を減らすと、使用しているサブスクリプションで使用可能なクォータを過剰に使用しないようにするのに役立ちます。この演習で使用するデータには
> 5,000 TPM で十分です。

## タスク 4: プロジェクトにデータを追加する

Copilotのデータは、架空の旅行代理店である *Margie's Travel* の PDF
形式の旅行パンフレットのセットで構成されています。それらをプロジェクトに追加しましょう。

1.  システムの C:\Lab ファイルにある **brochures**
    という名前のフォルダに移動します。

2.  Azure AI Foundry ポータルのプロジェクトで、左側のナビゲーション
    ウィンドウの \[**My assets**\] で、 \[**Data + indexes** **\]**
    ページを選択します。

> ![](./media/image21.png)

3.  \[+ **New data\] を選択します**。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image22.png)

4.  **Add your
    data** ウィザードで、ドロップダウンメニューを展開して「**Upload
    files/folders」を選択します**。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image23.png)

5.  \[**Upload folder** **\] を選択し**
    、**brochures** フォルダーを選択します。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image24.png)

6.  画面で \[**Next\] を選択します** 。

> ![](./media/image25.png)

7.  フォルダがアップロードされるのを待ち、いくつかの.pdfファイルが含まれていることに注意してください。

8.  次のページのname and
    finishで、データ名を**data0212として入力**し、\[**Create**\]をクリックします**。**

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image26.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image27.png)

## タスク 5: データのインデックスを作成する

プロジェクトにデータソースを追加したので、それを使用して Azure AI Search
リソースにインデックスを作成できます。

1.  Azure AI Foundry ポータルのプロジェクトで、左側のナビゲーション
    ウィンドウの \[**My assets**\] で、 \[**Data + indexes\]**
    ページを選択します。

> ![](./media/image28.png)

2.  \[**Indexes\]**
    タブで、次の設定で新しいインデックスを追加し、\[**Next**\]
    を選択します。

    - **ソースロケーション**:

      - **Data source**: Data in Azure AI Studio

        - ***brochures** のデータソースを選択します- **dataXXXX***

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image29.png)

- 以下のオプションとしてインデックスを構成し、\[**Next**\] を選択します
  **。**

  - **Azure AI Search service**: *Azure AI Search リソースへの
    **AzureAISearch**接続を選択します*

  - **Vector index**: brochures-index

  - **Virtual machine**: Auto select

> ![](./media/image30.png)

- 以下のように検索設定を構成し、\[**Next**\]を選択し、\[レビュー\]ウィンドウで\[**Create
  Vector Index\]をクリックします**。

  - **Vector settings**: Add vector search to this search resource

  &nbsp;

  - **Azure OpenAI connection**: *ハブの既定の Azure OpenAI
    リソースを選択します。*

> ![検索設定のスクリーンショット
> 説明が自動的に生成される](./media/image31.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image32.png)

3.  インデックス作成プロセスが完了するまで待ちます
    (数分かかる場合があります)。インデックス作成操作は、次のジョブで構成されます。

    - テキストトークンを解読し、チャンクし、パンフレットデータに埋め込みます。

    - Azure AI Search インデックスを作成します。

    - インデックスデータを登録します。

![コンピューターのスクリーンショット
説明が自動的に生成される](./media/image33.png)

![](./media/image34.png)

## タスク 6: インデックスをテストする

RAGベースのプロンプトフローでインデックスを使用する前に、インデックスを使用してgenerative
AIの応答に影響を与えることができることを確認しましょう。

1.  左側のナビゲーション ウィンドウで、\[**Playgrounds\]
    ページを選択し、\[Chat Playground\]** を選択します。

> ![](./media/image35.png)

2.  \[チャット\] ページの \[セットアップ\]
    ウィンドウで、**gpt-35-turbo-16k**
    モデルのデプロイが選択されていることを確認します。次に、メインのチャットセッションパネルで、プロンプト「**Where
    can I stay in New York?」を送信します。**

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image36.png)

3.  応答を確認します。これは、インデックスからのデータを含まないモデルからの一般的な回答である必要があります。

4.  \[設定\] ウィンドウで、\[**Add your data** \]
    フィールドを展開し、**brochures-index**
    プロジェクトインデックスを追加して、**hybrid (vector +
    keyword)** 検索タイプを選択します。

> ![チャットのスクリーンショット
> 説明が自動的に生成される](./media/image37.png)
>
> **注**:
> 一部のユーザーは、新しく作成したインデックスをすぐに使用できなくなります。通常はブラウザを更新すると役立ちますが、インデックスが見つからないという問題がまだ発生している場合は、インデックスが認識されるまで待つ必要があるかもしれません。

5.  インデックスが追加され、チャット
    セッションが再開されたら、プロンプト**Where can I stay in New
    York?**を再送信します

> ![チャットのスクリーンショット
> 説明が自動的に生成される](./media/image38.png)

6.  インデックス内のデータに基づく応答を確認します。

## タスク 7: プロンプト・フローでインデックスを使用する

ベクター インデックスは Azure AI Foundry
プロジェクトに保存されているため、プロンプトフローで簡単に使用できます。

1.  Azure AI Foundry
    ポータルのプロジェクトで、左側のナビゲーションウィンドウの \[**Build
    and customize\] で** \[**Prompt flow\]
    ページ**を選択し、\[**+Create\] をクリックします。**

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image39.png)

2.  ギャラリーで **Multi-Round Q&A on Your Data
    サンプルをコピーして、新しいプロンプト フローを作成します**
    。このサンプルのクローンを **brochure-flow
    という名前のフォルダーに保存します**。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image40.png)
>
> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image41.png)
>
> 注: アクセス許可エラーの場合は、2
> 分後に新しい名前で再試行すると、フローが複製されます。
>
> ![](./media/image42.png)

3.  プロンプトフロー デザイナー
    ページが開いたら、**brochure-flow**を確認します。グラフは次の画像のようになります:

> ![](./media/image43.png)

![プロンプトフローグラフのスクリーンショット](./media/image44.png)

> 使用しているサンプルのプロンプトフローは、ユーザーがチャットインターフェイスにテキスト入力を繰り返し送信できるチャットアプリケーションのプロンプトロジックを実装します。会話履歴は保持され、各イテレーションのコンテキストに含まれます。プロンプト・フローは、一連のツールをオーケストレーションして
> 、次のことを行います：

- チャット入力に履歴を追加して、コンテキスト化された形式の質問の形式でプロンプトを定義します。

- インデックスと、質問に基づいて独自に選択したクエリの種類を使用してコンテキストを取得します。

- インデックスから取得したデータを使用してプロンプト
  コンテキストを生成し、質問を補強します。

- システムメッセージを追加し、チャット履歴を構造化して、プロンプトバリアントを作成します。

- プロンプトを言語モデルに送信して、自然言語応答を生成します。

4.  \[**Start compute session** **\]** ボタンを使用して
    、フローのランタイムコンピューティングを開始します。

> ランタイムが開始されるまで待ちます。これにより、プロンプトフローのコンピューティングコンテキストが提供されます。待機中に、\[**Flow**\]
> タブで、フロー内のツールのセクションを確認します。
>
> ![](./media/image45.png)

5.  \[**Inputs\]**
    セクションで、入力に次のものが含まれていることを確認します：

    - **chat_history**

    - **chat_input**

このサンプルの既定のチャット履歴には、AI に関する会話が含まれています。

![](./media/image46.png)

6.  \[**Outputs\]**
    セクションで、出力に次のものが含まれていることを確認します。

    - 値 ${chat_with_context.output} の **chat_output**

> ![](./media/image47.png)

7.  **modify_query_with_history**セクションで、次の設定を選択します(他の設定はそのままにします)。

    - **Connection: *The default Azure OpenAI resource for your AI
      hub***

    - **Api: chat**

    - **deployment_name: gpt-35-turbo-16k**

    - **response_format: {“type”:”text”}**![](./media/image48.png)

8.  コンピューティング セッションが開始されるのを待ってから、**lookup**
    セクションで次のパラメーター値を設定します。

    - **mlindex_content**: *Select the empty field to open the Generate
      pane*

      - **index_type**: Registered Index

      &nbsp;

      - **mlindex_asset_id**: brochures-index:1

    - **queries**: ${modify_query_with_history.output}

    - **query_type**: Hybrid (vector + keyword)

    - **top_k**: 2

> ![](./media/image49.png)
>
> ![](./media/image50.png)

9.  \[**generate_prompt_context**\] セクションで Python
    スクリプトを確認し、このツール**のinputs** に次のパラメーターが含まれていることを確認します。

    - **search_result** *(object)*: ${lookup.output}

> ![](./media/image51.png)

10. Prompt_variants セクションで Python スクリプトを確認し、
    このツールの入力に次のパラメーターが含まれていることを確認します。

    - **コンテキスト** *(文字列):* ${generate_prompt_context.output}

    - **chat_history** *(文字列):* ${inputs.chat_history}

    - **chat_input** *(文字列):* ${inputs.chat_input}

> ![](./media/image52.png)

11. **chat_with_context**セクションで、次の設定を選択します(他の設定はそのままにします)。

    - **Connection**: Default_AzureOpenAI

    - **Api**: Chat

    - **deployment_name**: gpt-35-turbo-16k

    - **response_format**: {“type”:”text”}

次に、
このツールの**inputs** に次のパラメーターが含まれていることを確認します。

- **prompt_text** *(string)*: ${Prompt_variants.output}

> ![](./media/image53.png)

12. ツールバーの \[**Save**\]
    ボタンを使用して、プロンプトフローのツールに加えた変更を保存します。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image54.png)

13. ツールバーで、\[**Chat**\] を選択します。チャット
    ウィンドウが開き、サンプルの会話履歴と、サンプル値に基づいて既に入力された入力が表示されます。これらは無視できます。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image55.png)

14. チャットウィンドウで、デフォルトの入力を「**Where can I stay in
    London?**をクリックして送信します。

> ![](./media/image56.png)

15. インデックス内のデータに基づく応答を確認します。

16. フロー内の各ツールの出力を確認します。

> ![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image57.png)

17. チャットペインで、「**What can I do
    there?」という質問を入力します。**

18. インデックス内のデータに基づくレスポンスを確認し、チャット履歴を考慮に入れます(「there」は「in
    London」と理解されます)。

> ![](./media/image58.png)

19. フロー内の各ツールの出力を確認し、フロー内の各ツールがその入力に対してどのように動作したかに注目して、コンテキスト化されたプロンプトを準備し、適切な応答を取得します。

## タスク8:チャレンジ

Azure AI Foundry
ポータルで構築されたCopilotで独自のデータを統合する方法を理解したところで、さらに詳しく見ていきましょう。

Azure AI Foundry
ポータルを使用して新しいデータソースを追加し、インデックスを作成し、インデックス付けされたデータをプロンプトフローに統合してみてください。試すことができるデータセットには、次のようなものがあります：

- コンピューターにある(研究)記事のコレクション。

- 過去のカンファレンスのプレゼンテーションのセットです。

できるだけ機知に富んでデータソースを作成し、プロンプトフローに統合してください。新しいプロンプトフローを試して、選択したデータセットによってのみ回答できるプロンプトを送信してください。

## タスク 9: クリーンアップ

不要な Azure
のコストとリソースの使用率を回避するには、この演習でデプロイしたリソースを削除する必要があります。

Azure AI Foundry の探索が完了したら、 https://portal.azure.com で [Azure
portal](https://portal.azure.com/) に戻り、必要に応じて Azure
資格情報を使用してサインインします。次に、Azure AI Search と Azure AI
リソースをプロビジョニングしたリソース
グループ内のリソースを削除します。
