**사용 사례 05 - Azure RAG Accelerator활용한 대화형 AI 솔루션 배포 및
테스트**

소개

*내 데이터와 대화하기(Chat with your data)* 솔루션 가속기는 Azure AI
Search와 대규모 언어 모델(LLMs)의 기능을 결합해, 대화형 검색 경험을
제공하는 강력한 도구입니다. 이 솔루션 가속기는 Azure OpenAI GPT 모델과
사용자의 데이터에서 생성된 Azure AI Search 인덱스를 활용하여, 웹
애플리케이션에 자연어 인터페이스를 제공합니다. 이에는 음성-텍스트 변환
기능을 포함하여, 검색 쿼리를 처리할 수 있습니다. 사용자는 파일을 드래그
앤 드롭하거나, 저장소를 지정하고, 문서 변환을 위한 기술적 설정을 할 수
있습니다. 사용자는 보안과 인증이 포함된 자신만의 구독 내에서 웹
애플리케이션을 생성할 수 있습니다.

샘플 데이터는 이 가속기가 금융 서비스 산업(FSI)에서 어떻게 활용될 수
있는지 보여줍니다.

이 시나리오에서는 금융 고문이 Woodgrove Investments의 신흥 시장 펀드에
관심을 보인 잠재 고객과의 회의를 준비하고 있습니다. 고문은 회의를
준비하면서 신흥 시장 펀드의 전반적인 목표와 관련된 위험에 대한 이해를
새롭게 합니다.

이제 금융 고문은 Woodgrove의 신흥 시장 펀드에 대해 더 잘 알게
되었으므로, 고객의 질문에 더 잘 대응할 준비가 되어 있습니다.

참고: 이 가속기와 함께 제공되는 일부 샘플 데이터는 AI를 사용하여
생성되었으며, 예시용으로만 제공됩니다.

이 사용 사례에서는 Azure RAG(검색 증강 생성) 가속기를 사용해 대화형 AI
솔루션을 배포하고 테스트하게 됩니다. 이 솔루션은 Azure OpenAI와 Azure AI
Search의 강력한 AI 기능을 활용하여 고급 대화형 검색 경험을 제공합니다.
이 실습을 마치면 자연어 처리를 사용하여 데이터를 쿼리하고 상호작용할 수
있는 완전한 기능을 갖춘 웹 애플리케이션을 만들 수 있습니다. 실습 단계는
필요한 인프라를 배포하고, 리소스를 검증하고, 솔루션을 테스트한 후 환경을
정리하는 과정을 안내합니다. ![A computer screen shot of a diagram
AI-generated content may be incorrect.](./media/image1.png)

**목표**

- 필요한 인프라를 Azure 포털에서 사용자 지정 템플릿 통해 배포

- 필요한 모든 Azure 리소스가 성공적으로 배포되었는지 확인

- 배포된 솔루션의 기능을 테스트하기 위해 문서를 업로드 및 처리하며 웹
  애플리케이션과 상호작용하기

- 배포된 리소스 및 모델 삭제

**작업 1: 템플릿에서 인프라 배포**

1.  브라우저를 열고 주소 표시줄로 이동한 후, 다음 URL을 입력 또는
    붙여넣고 **Enter** 버튼을 누르세요:
    +++[www.portal.azure.com/+++then](http://www.portal.azure.com/+++then) 

2.  **Microsoft Azure** 창에 **Sign-in** 자격 증명을 입력하고
    **Next** 버튼을 클릭하세요.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)

3.  이제 비밀번호를 입력하고 **Sign in** 버튼을 클릭하세요\*\*.\*\*

> ![A screenshot of a login box AI-generated content may be
> incorrect.](./media/image3.png)

4.  **Stay signed in?** 창에서 **Yes** 버튼을 클릭하세요.

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image4.png)

5.  새 브라우저를 열고 주소창에 다음 URL을 입력해 Azure Portal을 여세요:
    +++<https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json+++>.

6.  On **Custom deployment** 창의 **Basics** 탭에서 다음 정보를 입력해
    사용자 지정 템플릿을 배포한 후, **Review + create**를 클릭하세요.

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

7.  **Review + create** 탭에서유효성 검사(Validation)이
    통과(Passed)되면 **Create** 버튼을 클릭하세요.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image6.png)

8.  배포가 완료될 때까지 대기하세요. 완료까지 약 17~19분 정도
    소요됩니다.

9.  **Go to Subscription** 버튼을 클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

**작업 2: Azure 포털에서 배포된 리소스 확인**

1.  홈페이지에서 **Resource Groups**를 클릭하세요.

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image8.png)

2.  리소스 그룹 이름인 **rg-RAGSolutionXX**를 클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  아래 리소스가 East US 지역에 정상적으로 배포되었는지 확인하세요.

    - Azure App Service

    - Azure Application Insights

    - Azure Bot

    - Azure OpenAI

    - Azure Document Intelligence

    - Azure Function App

    - Azure Search Service

    - Azure Storage Account

    - Azure Speech Service

    - Azure Database for PostgreSQL - Flexible Server

    - Key vault

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

![](./media/image11.png) ![A screenshot of a computer AI-generated
content may be incorrect.](./media/image12.png)

**작업 3: 배포 테스트하기**

1.  리소스 그룹에서 **Web-** {RESOURCE_TOKEN} **- admin-docker** 리소스
    이름을 클릭하세요.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)

2.  다음 관리 사이트로 이동하세요:  

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

3.  **Chat with your data Solution Accelerator** 페이지의 왼쪽에 있는
    탐색 창에서 **Ingest Data**를 선택하세요.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image16.png)

4.  Add documents Batch 창에서 **Browse file**을 클릭하고 **C:\Labfiles
    \data**로 이동하여 **all files**을 선택한 후, **Open** 버튼을
    클릭하세요.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  파일을 업로드하는 데 1-2분이 소요됩니다.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

6.  **Reprocess all documents in the Azure Storage account**를
    클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image21.png)

7.  **Chat with your data Solution Accelerator** 페이지의 왼쪽 탐색
    메뉴에서 **Configuration**를 선택한 후, **Enable post-answering
    prompt 체크박스를** 선택하세요.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

8.  구성(configuration) 창에서 **Save configuration**를 클릭하세요.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

9.  리소스 그룹 페이지로 돌아가서 **Storage account** 이름을 클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

10. 왼쪽 탐색 메뉴에서 **Containers**를 클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

11. Containers 페이지에서 **documents**를 선택하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

12. 모든 파일이 성공적으로 배포되었는지 화인하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

13. 리소스 그룹 페이지로 돌아가세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

14. 리소스 그룹 페이지에서 App
    service을 **web-{RESOURCE_TOKEN}-docker**로 선택하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

15. Settings(설정) 아래의 축소 가능한 왼쪽 메뉴에서
    Authentication(인증)을 선택하세요.![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image31.png)

16. Add an identify provider를 클릭하세요.  ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image32.png)

17. Select Microsoft as the Identity provider로 Microsoft를 선택하고,
    Name을 web-XXXXX-docker-new로 업데이트하세요. Client secret
    expiration 기간을 90일로 선택한 후, Next: Permissions를
    클릭하세요. ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image33.png)

18. Add permission을 클릭하세요. 목록을 아래로 스크롤하여 Application을
    확장하고 Application.ReadWrite.All을 선택하세요. 그 후, Update
    permission을 클릭하세요. 

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image34.png)

19. 이제 Add버튼을 클릭하세요. 

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image35.png)

20. 앱의 Overview페이지를 클릭하세요. 페이지가 로드될 때까지 기다린 후,
    Restart을 클릭하세요. 다시 시작을 확인하려면 Yes를 클릭하세요. ![A
    screenshot of a computer AI-generated content may be
    incorrect.](./media/image36.png) ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image37.png)

21. Web App **Overview** 페이지에서 명령 표시줄로 이동하여 **Browse**를
    클릭하면 웹 애플리케이션으로 이동하게 됩니다.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image38.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

22. **Azure AI** 웹앱 페이지에서 다음 텍스트를 입력하고 아래 이미지와
    같이 **Submit icon**을 클릭하세요.

+++Describe in more detail the risks from market volatility+++ 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

17. **Chat session** 섹션에서 참조 링크를 선택한 후, 페이지 오른쪽에
    있는 검색 문서의 정보를 확인하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

18. **Azure AI** 웹 앱 페이시에서 다음 텍스트를 입력하고 아래 이미지와
    같이 **Submit icon**을 클릭하세요.

+++How does Woodgrove Financial handle payroll taxes for employees
outside the U.S.?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png) ![A screenshot of a chat AI-generated
content may be incorrect.](./media/image44.png)

19. **Azure AI** 웹 앱 페이시에서 다음 텍스트를 입력하고 아래 이미지와
    같이 **Submit icon**을 클릭하세요.

+++What is FORM 10-K and explain?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image45.png)

**작업 4: Azure OpenAI Resource 삭제하기**

1.  Azure OpenAI 리소스로 이동하기 위해 Azure 포털 검색 창에 **Resource
    groups**을 입력하고**Services** 에서 **Resource groups** 을 탐색한
    후 클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

2.  사용자의 리소스 그룹을 클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  리소스 그룹의 개요(overview) 페이지에서 **Delete resource group**을
    선택하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

4.  오른쪽에 표시되는 **Delete Resources** 창에서 **resource group
    name**을 입력하고 **Delete** 버튼을 클릭하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

5.  **Delete confirmation** 대화 상자에서 D**elete** 버튼을 클릭하세요.

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image49.png)

요약:

이 실습은 Azure RAG Accelerator를 사용해 대화형 AI 솔루션을 배포하는
실습 경험을 제공합니다. 실습은 사용자 지정된 템플릿을 사용해 필요한
인프라를 배포하는 것으로 시작되었습니다. 다양한 Azure 리소스의 성공적인
배포를 확인한 후, 문서를 업로드하고 웹 애플리케이션을 사용하여 쿼리를
실행하고 정보를 검색하는 방식으로 솔루션을 테스트했습니다. 마지막으로,
리소스를 효율적으로 관리하기 위해 리소스 그룹을 삭제했습니다. 이 실습은
고급 AI 기술을 사용하여 데이터 상호작용 및 검색을 향상시키는 방법을
보여주었습니다.
