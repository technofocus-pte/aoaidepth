# 用例 12 - 在 Azure AI Content Safety Studio 中使用內容安全審核文本和圖像

**介紹**

Azure AI 內容安全可檢測應用程式和服務中有害的使用者生成和 AI
生成的內容。Azure AI 內容安全包括文本和圖像
API，可用於檢測有害材料。Microsoft Azure
還有一個互動式內容安全工作室，允許您查看、流覽和試用用於檢測不同模式中的有害內容的示例代碼。

內容過濾軟體可以説明您的應用程式遵守法規或為您的用戶維護預期的環境。

Azure AI 內容安全工作室是一種線上工具，旨在使用尖端的內容審核 ML
模型處理可能具有攻擊性、風險或不良內容。它提供範本和自訂工作流，使用戶能夠選擇和構建自己的內容審核系統。使用者可以上傳自己的內容，也可以使用提供的示例內容進行試用。

在 Content Safety Studio 中，可以使用以下 Azure AI 內容安全服務功能：

- **審核文本內容：**使用文本審核工具，您可以輕鬆地對文本內容運行測試。無論您是想測試單個句子還是整個資料集，此工具都提供了一個使用者友好的介面，讓您可以直接在門戶中評估測試結果。

- **審核圖像內容：**使用圖像審核工具，您可以輕鬆地對圖像運行測試，以確保它們符合您的內容標準。

- **監控線上活動：** 強大的監控頁面可讓您輕鬆跟蹤不同模式的審核 API
  使用情況和趨勢。使用此功能，您可以訪問詳細的回應資訊，包括類別和嚴重性分佈、延遲、錯誤和阻止清單檢測。此資訊為您提供了內容審核性能的完整概覽，使您能夠優化工作流程並確保您的內容始終按照您的確切規範進行審核。

**目的**

- 部署 Azure AI 內容安全資源。

- 創建 Azure AI 資源並探索內容安全。

- 在 Azure AI Studio 中設置 Azure AI
  資源並探索內容安全功能，強調文本和圖像審核。

## **任務 1：創建 Azure AI 內容安全資源**

1.  打開流覽器，導航到地址欄，鍵入或粘貼以下
    URL：https://portal.azure.com/，然後按 **Enter** 按鈕。

> ![](./media/image1.png)

2.  在 **Sign in** 視窗中，輸入 **用戶名** 並按一下 **Next** 按鈕。

![](./media/image2.png)

3.  然後，輸入密碼並按一下 **Sign in** 按鈕。

> ![A screenshot of a login box Description automatically
> generated](./media/image3.png)

4.  在 **Stay signed in?** 視窗中，按一下 **Yes** 按鈕。

> ![A screenshot of a computer Description automatically
> generated](./media/image4.png)

5.  在 Azure 門戶主頁中，按一下 **Azure 門戶功能表**，該功能表由
    Microsoft Azure 命令列左側的三個水準條表示，如下圖所示。

> ![A screenshot of a computer Description automatically
> generated](./media/image5.png)

6.  導航並按一下 **+ Create a resource**。

> ![A screenshot of a computer Description automatically
> generated](./media/image6.png)

7.  在 **Marketplace** 頁面的 **Search services and marketplace**
    搜索欄中，鍵入**Azure AI Content Safety**，然後按 **Enter** 按鈕。
    然後，導航到 **Azure AI Content Safety**
    ，按一下創建按鈕下拉式功能表，然後選擇 **Azure AI Content Safety**
    ，如下圖所示。

> ![](./media/image7.png)
>
> ![](./media/image8.png)

8.  在 **Create Azure OpenAI** 視窗的 **Basics**
    選項卡下，輸入以下詳細資訊，然後按一下 **Review+create**按鈕。

[TABLE]

> ![](./media/image9.png)

9.  在 **Review+submit** 選項卡中，驗證通過後，按一下 **Create** 按鈕。

> ![](./media/image10.png)

10. 等待部署完成。部署大約需要 2-3 分鐘。

11. 在 **Microsoft.CognitiveServicesContentSafety**
    視窗中，部署完成後，按一下 **Go to resource** 按鈕。

![](./media/image11.png)

![](./media/image12.png)

![](./media/image13.png)

## 任務 2：分析文本內容

1.  在 **Content Safety** 頁面中，導航到 **Moderate text content**
    模組，然後按一下 **Try it out** 連結。

![](./media/image14.png)

2.  在“**Settings** ”窗格中，選擇 **AOAI-ContentSafetyXX**
    並按一下“**Use resource**”。

![](./media/image15.png)

3.  在 **Content Safety** 頁面中，導航到 **Moderate text content**
    模組，然後按一下 **Try it out** 連結。

![](./media/image14.png)

4.  在 **Run a simple test** 選項卡下，選擇 **Safe content** tile
    （安全內容磁貼），如下圖所示。

![](./media/image16.png)

5.  或者，您可以使用 **Configure filters** （配置篩檢程式）
    選項卡中的滑動控制項來修改每個類別的允許或禁止的嚴重性級別。然後，按一下
    **Run test** 按鈕。

![](./media/image17.png)

![](./media/image18.png)

6.  向下滾動以查看結果。該服務返回檢測到的所有類別、每個類別的嚴重性級別（0-安全、2-低、4-中等、6-高）以及二進位
    **Allowed** 或 **Reject** 判斷。結果基於您配置的篩選條件。

![](./media/image19.png)

7.  向下滾動並按一下 **View
    Code**（查看代碼）按鈕，如下圖所示，查看並複製示例代碼，其中包括嚴重性篩選、阻止清單和審核功能的配置。然後，您可以在自己的終端部署代碼。

![](./media/image20.png)

![A screenshot of a computer program Description automatically
generated](./media/image21.png)

## 任務 3：檢測用戶輸入攻擊

1.  返回**Content Safety Studio**

![](./media/image22.png)

2.  在 **Content Safety** 頁面的 **Explore safety solutions for Gen-AI**
    下，導航到 **Prompt Shields** 磁貼，按一下 **Try it out** 連結。

![](./media/image23.png)

3.  在 “**Set up sample** ” 下，選擇 “**Safe content**
    ”磁貼，如下圖所示。

![](./media/image24.png)

4.  或者，您可以使用 **Prompt shields** （提示盾牌）
    選項卡中的滑動控制項來修改每個類別的允許或禁止的嚴重性級別。然後，按一下
    **Run test** 按鈕。

![](./media/image25.png)

8.  向下滾動並按一下 **View
    Code**（查看代碼）按鈕，如下圖所示，查看並複製示例代碼，其中包括嚴重性篩選、阻止清單和審核功能的配置。然後，您可以在自己的終端部署代碼。

![](./media/image26.png)

![](./media/image27.png)

5.  在 “**Set up sample**” 選項卡下，選擇 “**User prompt attack
    content**” 磁貼，然後按一下 “**Run test** ”，如下圖所示。

![](./media/image28.png)

![A screenshot of a computer Description automatically
generated](./media/image29.png)

## 任務 4：分析圖像內容

1.  在 Prompt Shields 窗格下，按一下**Back**

![](./media/image30.png)

2.  在“**Content Safety** ”頁面中，導航到“**Moderate image content**
    ”模組，然後按一下“**Try it out**”連結。

![](./media/image31.png)

3.  在 Select a sample or upload your own
    section（選擇示例或上傳您自己的部分）下，導航並按一下 **Browse for a
    file** （流覽檔） 連結。

![](./media/image32.png)

**注意：** 圖像提交的最大大小為 4 MB，圖像尺寸必須介於 50 x 50 圖元和
2,048 x 2,048 圖元之間。圖像可以是 JPEG、PNG、GIF、BMP、TIFF 或 WEBP
格式。

4.  導航到 **C：\Labfiles** 位置並選擇 **car-accident** 圖像，然後按一下
    **Open** 按鈕。

![](./media/image33.png)

5.  或者，您可以使用 **Configure filters** （配置篩檢程式）
    選項卡中的滑動控制項來修改每個類別的允許或禁止的嚴重性級別。

6.  按一下 **Run test** 按鈕。

![](./media/image34.png)

7.  向下滾動以查看測試結果。該服務返回檢測到的所有類別、每個類別的嚴重性級別（0-安全、2-低、4-中、6-高）以及二進位
    **Accept** 或 **Reject** 判斷。結果基於您配置的篩選條件

![](./media/image35.png)

8.  向下滾動並按一下 **View
    Code**（查看代碼）按鈕，如下圖所示，查看並複製示例代碼，其中包括嚴重性篩選、阻止清單和審核功能的配置。然後，您可以在自己的終端部署代碼。

![](./media/image36.png)

![](./media/image37.png)

## 任務 5：刪除資源組

1.  導航到 Azure 門戶主頁，在 Azure 門戶搜索欄中鍵入“**Resource groups**
    ”，導航並按一下“**Services**”下的“**Resource groups**”。

> ![A screenshot of a computer Description automatically
> generated](./media/image38.png)

2.  按一下您為 Azure AI 資源提供的資源組。

> ![](./media/image39.png)

3.  在 **Resource group** （資源組） 主頁中，選擇**delete resource
    group**

![](./media/image40.png)

4.  在右側顯示的 **Delete Resources** 窗格中，導航到 **Enter “resource
    group name” 以確認刪除**欄位，然後按一下 **Delete** 按鈕。

![](./media/image41.png)

5.  在 **Delete confirmation** 對話方塊中，按一下 **Delete** 按鈕。

> ![A screenshot of a computer error Description automatically
> generated](./media/image42.png)

6.  按一下鈴鐺圖示，您將看到通知 –**Deleted resource group AOAI-RG89.**

![A screenshot of a computer Description automatically
generated](./media/image43.png)

**總結**

在本實驗室中，你已為 Azure AI 內容安全工作室創建並配置了 Azure
資源，特別關注文本和圖像的內容審核、探索文本和圖像內容審核功能。在本實驗中，您學習了如何在
Azure 環境中實現內容審核功能。
