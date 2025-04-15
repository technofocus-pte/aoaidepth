# ユースケース 06 - PostgreSQL フレキシブル サーバーを使用して Azure Container Apps にチャットアプリをデプロイする

**目的：**

- Azure CLI、Node.js をインストールし、Azure サブスクリプション
  ロールを割り当て、Docker Desktop を起動し、Dev Containers
  拡張機能を使用して Visual Studio Code を有効にして、Windows
  上で開発環境を構成する。

- Azure で PostgreSQL と OpenAI を使用したカスタムチャット
  アプリケーションをデプロイしてテストします。

![コンピューターのスクリーンショット
AIが生成したコンテンツが正しくない可能性があります。](./media/image1.jpeg)

このユース ケースでは、包括的な開発環境を設定し、PostgreSQL
と統合されたチャット アプリケーションをデプロイして、Azure
でのデプロイを確認します。これには、Azure CLI、Docker、Visual Studio
Code などの重要なツールのインストール (ホスト env
で既に実行されています)、Azure でのユーザー ロールの構成、Azure
Developer CLI
を使用したアプリケーションのデプロイ、デプロイされたリソースとの対話が含まれ、機能を確認します。

**使用した主なテクノロジ** -- Python、FastAPI、Azure OpenAI
モデル、Azure Database for
PostgreSQL、azure-container-apps、ai-azd-templates。

**推定所要時間**-- 45 分

**ラボタイプ:** インストラクター主導

**前提条件:**

GitHub アカウント -- 自分の GitHub
ログイン資格情報を持っている必要があります。お持ちでない場合は、こちらから作成してください -
+++<https://github.com/signup?user_email=&source=form-home-signupobjectives+++>

**演習 1 :
アプリケーションをプロビジョニングし、デプロイし、ブラウザーからテストします**

## タスク 0: VM と資格情報を理解する

このタスクでは、ラボ全体で使用する資格情報を特定して理解します。

1.  **\[Instructions** **\]**
    タブには、ラボ全体に従うべき指示が記載されたラボ ガイドがあります。

2.  **\[Resources** \] タブには、ラボの実行に必要な資格情報があります。

    - **URL** – Azure portal の URL

    - **サブスクリプション** –
      これは、お客様に割り当てられたサブスクリプションの ID です

    - **ユーザー名** – Azure サービスにログインするために必要なユーザー
      ID。

    - **パスワード** – Azure
      ログインのパスワード。このユーザー名とパスワードを Azure
      ログイン資格情報と呼ぶことにします。これらのクレドは、Azure
      のログイン資格情報について言及するすべての場所で使用します。

    - **リソースグループ** – **自分に割り当てられた**リソースグループ。

\[!アラート\]**重要:**このリソースグループの下にすべてのリソースを作成してください

> ![コンピューターのスクリーンショット
> AIが生成したコンテンツが正しくない可能性があります。](./media/image2.png)

3.  **\[ヘルプ**\] タブには、サポート情報が表示されます。ここでの **ID**
    値は、 **ラボの実行中に使用される**ラボ インスタンス ID です。

> ![コンピューターのスクリーンショット
> AIが生成したコンテンツが正しくない可能性があります。](./media/image3.png)

## タスク 1 : サービス プロバイダーの登録

1.  ブラウザを開き、+++https://portal.azure.com++++に移動して、以下のクラウドスライスアカウントでサインインします。

> ユーザー名: <+++@lab.CloudPortalCredential>(User1).Username+++
>
> パスワード：<+++@lab.CloudPortalCredential(User1).Password>+++![コンピューターのスクリーンショット
> 説明が自動的に生成される](./media/image4.png)
>
> ![ログインボックスのスクリーンショット
> 説明が自動的に生成される](./media/image5.png)

2.  **Subscriptions** **タイル**をクリックします。

> ![コンピューターのスクリーンショット
> AIが生成したコンテンツが正しくない可能性があります。](./media/image6.png)

3.  subscription nameをクリックします。

> ![コンピューターのスクリーンショット
> AIが生成したコンテンツが正しくない可能性があります。](./media/image7.png)

4.  左側のナビゲーションメニューから\[設定\]を展開します。\[**Resource
    providers\]
    をクリックし**、「+++**Microsoft.AlertsManagement+++」**と入力して
    \[i,t\] を選択し、\[**Register**\] をクリックします。

![コンピューターのスクリーンショット
AIが生成したコンテンツが正しくない可能性があります。](./media/image8.png)

![コンピューターのスクリーンショット
AIが生成したコンテンツが正しくない可能性があります。](./media/image9.png)

5.  \[リソース プロバイダー**\]
    をクリックし**、「+++**Microsoft.DBforPostgreSQL+++**」と入力して
    \[i,t\] を選択し、\[**Register**\] をクリックします。

![コンピューターのスクリーンショット
AIが生成したコンテンツが正しくない可能性があります。](./media/image10.png)

![コンピューターのスクリーンショット
AIが生成したコンテンツが正しくない可能性があります。](./media/image11.png)

![コンピューターのスクリーンショット
AIが生成したコンテンツが正しくない可能性があります。](./media/image12.png)

![コンピューターのスクリーンショット
AIが生成したコンテンツが正しくない可能性があります。](./media/image13.png)

6.  手順 \#10 と \#11
    を繰り返して、次のリソースプロバイダーを登録します。

- Microsoft.Search

- Microsoft.Web

- Microsoft.ManagedIdentity

## タスク 2: 既存のリソース グループ名をコピーする

1.  ホーム ページで、\[**Resource groups** \] をクリックします。

![](./media/image14.png)

2.  作業するためのリソース
    グループが既に作成されていることを確認してください。このリソース・グループは絶対に削除しないでください。代わりに、リソース
    グループ内のリソースは削除できますが、リソース
    グループ自体は削除できません。

3.  リソース・グループ名をクリックします

![](./media/image15.png)

4.  リソース グループ名をコピーしてメモ帳に保存し、このリソース
    グループにすべてのリソースをデプロイするときに使用します

![](./media/image16.png)

## タスク 3 : Docker を実行する

1.  デスクトップで、**Docker Desktopをダブルクリックします**。

> ![コンピューターのスクリーンショット
> AIが生成したコンテンツが正しくない可能性があります。](./media/image17.png)

2.  Docker デスクトップを実行します。

> ![コンピューターのスクリーンショット
> AIが生成したコンテンツが正しくない可能性があります。](./media/image18.png)

## タスク4:オープンな開発環境

1.  ブラウザを開き、アドレスバーに移動し、次のURLを入力または貼り付けます:+++[https://github.com/technofocus-pte/rag-postgres-openai-python-CSTesting.git+++タブ](https://github.com/technofocus-pte/rag-postgres-openai-python-CSTesting.git+++%C2%A0tab)が開き、VisualStudioCodeで開くように求められます。\[**Open
    Visual Studio Code\] を選択します。**

> ![](./media/image19.jpeg)

2.  **fork** **をクリックして**
    リポジトリをフォークします。リポジトリに一意の名前を付け、\[**Create
    repo\]**ボタンをクリックします。

> ![](./media/image20.png)
>
> ![](./media/image21.png)

3.  Code -\> **Codespaces** -\> **Codespaces**+ **をクリックします。**

> ![](./media/image22.png)

4.  Codespaces
    環境が設定されるのを待ちます。完全にセットアップするには数分かかります

> ![](./media/image23.png)
>
> ![コンピューターのスクリーンショット
> AIが生成したコンテンツが正しくない可能性があります。](./media/image24.png)

## タスク 5: サービスをプロビジョニングし、アプリケーションを Azure にデプロイする

1.  ターミナルで次のコマンドを実行します。コピーするコードが生成されます。コードをコピーしてEnterキーを押します。

+++azd auth login+++

> ![](./media/image25.png)

2.  デフォルトのブラウザが開き、検証する生成されたコードを入力します。コードを入力し、\[**Next**\]
    をクリックします。

> ![](./media/image26.png)

3.  Azure の資格情報でサインインします。

> ![](./media/image27.png)

4.  Azure リソースの環境を作成するには、次の Azure Developer CLI
    コマンドを実行します。環境名を入力するように求められます。任意の名前を入力してEnterキーを押します(例:+++ragpgpy+++)

**注:**
環境を作成するときは、名前が小文字で構成されていることを確認してください。

> +++azd env new+++

![](./media/image28.png)

5.  次の Azure Developer CLI コマンドを実行して、Azure
    リソースをプロビジョニングし、コードをデプロイします。

+++azd provision+++

![](./media/image29.png)

6.  メッセージが表示されたら、**リソースを作成するサブスクリプション**を選択し、現在地に最も近いリージョンを選択します。このラボでは、**East
    US2** リージョンを選択しています。

![](./media/image30.png)

7.  「**Enter a value for the 'existingResourceGroupName' infrastructure
    parameter**:**」というプロンプトが表示されます。**タスク 1
    でコピーしたリソース グループを入力します (例:
    開発スライスに使用される
    \*\*ResourceGroup1)」。\*\*次の図に示すように、リソース
    セクションからリソース グループ名をコピーできます

![](./media/image31.png)

8.  プロンプトが表示されたら、**'openAILocation' インフラストラクチャ
    パラメータの値を入力し**、現在地に最も近いリージョンを選択します。このラボでは、**North
    Central US** **の**リージョンを選択しています

![](./media/image32.png)

9.  リソースのプロビジョニングには約 5 分から 10 分かかります。
    **プロンプトが表示されたら** \[**Yes** \] をクリックします。

![](./media/image33.png)

10. テンプレートがすべてのリソースを正常にプロビジョニングするまで待ちます。

![](./media/image34.png)

11. 次のコマンドを実行して、リソースグループを設定します

+++azd env set AZURE_RESOURCE_GROUP {your resource group
name}+++ ![](./media/image35.png)

12. 次のコマンドを実行して、アプリを Azure にデプロイします。

+++azd deploy+++

![](./media/image36.png)

13. デプロイが完了するまで待ちます。デプロイには \<5 かかります

![](./media/image37.png)

14. デプロイされた Web アプリ エンドポイントのリンクをクリックします。

![](./media/image38.png)

15. \[**Open\]をクリックします**。アプリで新しいタブが開きます

![](./media/image39.png)

16. アプリが開きます。

![](./media/image40.png)

**タスク 6: チャットアプリを使用してファイルから回答を取得する**

1.  **RAGデータベース内 |OpenAI + PoastgreSQL**
    Webアプリのページで、**Best shoe for
    hiking?** **をクリックしますか?**ボタンをクリックし、出力を観察します

![](./media/image41.png)

![](./media/image42.png)

2.  **clear chatをクリックします。**

![](./media/image43.png)

3.  **RAG on database |OpenAI + PoastgreSQL**
    Webアプリのページで、**Climbing gear cheaper than
    \\30** ボタンをクリックして、出力を観察します

![](./media/image44.png)

![](./media/image45.png)

4.  **clear chatをクリックします。**

**タスク 7: Azure portal でデプロイされたリソースを確認する**

1.  Azure portal の ホーム ページで、\[**Resource Groups\]
    をクリックします**。

![](./media/image46.png)

2.  リソース・グループ名をクリックします

![](./media/image47.png)

3.  以下のリソースが正常にデプロイされたことを確認します

    - Container App

    - Application Insights

    - Container Apps Environment

    - Log Analytics workspace

    - Azure OpenAI

    - Azure Database for PostgreSQL flexible server

    - Container registry

![](./media/image48.png)

4.  \[Azure OpenAI **リソース名**\] をクリックします。

![](./media/image49.png)

5.  **左側のナビゲーション メニューの \[Overview** **\] で、 \[**Azure
    AI Foundry ポータルに移動**\]
    をクリックし、新しいタブを選択して開きます。**

![](./media/image50.png)

6.  左側のナビゲーションメニューから **\[Shared resources -\>
    Deployments**\]
    をクリックし、**gpt-35-turbo**、**text-embedding-ada-002**
    が正常にデプロイされることを確認します

![](./media/image51.png)

**タスク 8 : すべてのリソースをクリーンアップする**

このサンプルで作成されたすべてのリソースをクリーンアップするには、次のようにします。

1.  **Azure portal -\> Resource group- \> Resource group
    nameに戻ります。**

![](./media/image52.png)

2.  すべてのリソースを選択し、下の画像に示すように\[Delete\]をクリックします。(リソース・グループを削除しないでください)

![](./media/image53.png)

3.  テキストボックスに「delete」と入力し、\[**Delete**\]をクリックします。

![](./media/image54.png)

4.  \[**Delete\]をクリックして削除を確認します**。

![](./media/image55.png)

5.  Githubポータルタブに戻り、ページを更新します。

![](./media/image56.png)

6.  \[コード\]
    をクリックし、このラボ用に作成したブランチを選択して、\[**Delete**\]
    をクリックします。

![](./media/image57.png)

7.  \[**Delete\]ボタンをクリックして、ブランチの削除を確認します** 。

![](./media/image58.png)

**概要:**このユース
ケースでは、クラウドベースのアプリケーションのデプロイと管理に焦点を当てて、PostgreSQL
と OpenAI を使用して Azure にチャット
アプリケーションをデプロイする手順を説明します。開発環境をセットアップし、必要なツール
(Azure CLI など) をインストールし、Azure Developer CLI を使用して Azure
リソースを構成し、アプリケーションを Azure Container Apps
にデプロイしました。
