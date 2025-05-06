**Caso de uso 05 - Implementando e testando uma solução de AI
conversacional com o Azure RAG Accelerator**

**Introdução**

O acelerador *de soluções de chat com seus dados* é uma ferramenta
poderosa que combina os recursos de Azure AI Search e Large Language
Models (LLMs) para criar uma experiência de pesquisa conversacional.
Esse acelerador de solução usa um modelo Azure OpenAI GPT e um índice do
Azure AI Search gerado a partir de seus dados, que é integrado a um
aplicativo web para fornecer uma interface de linguagem natural,
incluindo a funcionalidade de conversão de fala em texto, para consultas
de pesquisa. Os usuários podem arrastar e soltar arquivos, apontar para
o armazenamento e cuidar da configuração técnica para transformar
documentos. Existe um aplicativo da web que os usuários podem criar em
sua própria assinatura com segurança e autenticação.

Os dados de amostra ilustram como esse acelerador pode ser usado na
Financial Services Industry (FSI).

Neste cenário, um consultor financeiro está se preparando para uma
reunião com um potencial cliente que demonstrou interesse nos Fundos de
Mercados Emergentes da Woodgrove Investments. O consultor se prepara
para a reunião revisando seu entendimento sobre os objetivos gerais dos
fundos de mercados emergentes e os riscos associados.

Agora que o consultor financeiro está mais informado sobre os Fundos de
Mercados Emergentes da Woodgrove, ele está mais bem preparado para
responder às perguntas do cliente sobre esse fundo.

Observação: Alguns dos dados de exemplo incluídos neste acelerador foram
gerados usando AI e são apenas para fins ilustrativos.

 Neste caso de uso, você irá implantar e testar uma Solução de AI
Conversacional utilizando o Azure RAG (Retrieval-Augmented Generation)
Accelerator. Essa solução aproveita os poderosos recursos de AI da
Azure, incluindo o Azure OpenAI e o Azure AI Search, para criar uma
experiência avançada de busca conversacional. Ao final deste
laboratório, você terá uma aplicação web totalmente funcional que
utiliza processamento de linguagem natural para interagir com seus dados
e consultá-los. Os passos práticos irão guiá-lo pela implementação da
infraestrutura necessária, verificação dos recursos, teste da solução e
limpeza do ambiente. ![A computer screen shot of a diagram AI-generated
content may be incorrect.](./media/image1.png)

**Objectives**

- Implementar a infraestrutura necessária a partir de um modelo
  personalizado no portal do Azure.

- Verificar se todos os recursos do Azure necessários foram
  implementados com sucesso.

- Testar a funcionalidade da solução implementada, fazendo upload e
  processamento de documentos e interagindo com a aplicação web.

- Excluir os recursos e modelos implementados.

**Tarefa 1: Implementar a infraestrutura a partir do modelo**

1.  Abra o seu navegador, vá até a barra de endereços e digite ou cole o
    seguinte
    URL:+++[www.portal.azure.com/+++then](http://www.portal.azure.com/+++then)
    pressione o botão **Enter**.

2.  Na Janela **Microsoft Azure**, insira suas credenciais **Sign-in**,
    e clique no botão **Next**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)

3.  Em seguida, insira a senha e clique no botão **Sign in** \*\*.\*\*

> ![A screenshot of a login box AI-generated content may be
> incorrect.](./media/image3.png)

4.  Na janela **Stay signed in?**, clique no botão **Yes**.

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image4.png)

5.  **Abra um novo navegador** e insira o seguinte URL na barra de
    endereços:
    +++<https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json+++> para
    abrir o portal do Azure.

6.  Na janela **Custom deployment**, sob a aba **Basics**, insira os
    seguintes detalhes para implementar o modelo personalizado e depois
    clique em **Review + create**.

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

7.  Na aba **Review + create**, quando a validação for aprovada, clique
    no botão **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image6.png)

8.  Aguarde a conclusão da implementação. A implementação levará cerca
    de 17 a 19 minutos.

9.  Clique no botão **Go to Subscription**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

**Tarefa 2: Verificar os recursos implementados no portal do Azure**

1.  Na página inicial, clique em **Resource Groups**.

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image8.png)

2.  Clique no nome de seu grupo de recursos **rg-RAGSolutionXX**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  Certifique-se de que os recursos abaixo foram implementados com
    sucesso na região East US

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

**Tarefa 3: Testar a implementação**

1.  No grupo de recursos e clique em **Web-** {RESOURCE_TOKEN} **-
    admin-docker** nome do recurso.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)

2.  Navegue até o site de administração 

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

3.  Na página **Chat with your data Solution Accelerator**, no menu de
    navegação esquerdo, selecione **Ingest Data.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image16.png)

4.  No painel Add documents Batch, clique em **Browse file** e navegue
    até o local **C:\Labfiles \data** e selecione **all files** e, em
    seguida clique no botão **Open**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  O carregamento de arquivos levará de 1 a 2 minutos

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

6.  Clique em **Reprocess all documents em Azure Storage account.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image21.png)

7.  Na página **Chat with your data Solution Accelerator**, no menu de
    navegação esquerdo, selecione **Configuration** e marque a **check
    box- Enable post-answering prompt.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

8.  No painel de configuração, clique em **Save configuration.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

9.  Volte para página resource group e clique no nome **the Storage
    account**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

10. No menu de navegação esquerdo, clique em **Containers.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

11. Na página Containers, selecione **documents**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

12. Certifique-se de que todos os arquivos sejam implementados com êxito

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

13. Volte para a página do resource group

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

14. Na página resource group, selecione serviço de aplicativo
    como **web-{RESOURCE_TOKEN}-docker**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

15. No menu suspenso à esquerda, em Settings, selecione
    Authentication ![A screenshot of a computer AI-generated content may
    be incorrect.](./media/image31.png)

16. Clique em Add identify provider ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image32.png)

17. Selecione Microsoft como o Identity provider, atualize o nome como
    web-XXXXX-docker-new. Selecione a duração do vencimento do Client
    secret como 90 days e então clique Next: Permissions. ![A screenshot
    of a computer AI-generated content may be
    incorrect.](./media/image33.png)

18. Clique em Add permission. Role a lista para baixo para expandir
    Application e selecione Application.ReadWrite.All. Em seguida,
    clique em Update permission. 

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image34.png)

19. Clique em Add. 

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image35.png)

20. Clique na página Overview do aplicativo. Aguarde o carregamento da
    página e, em seguida, clique em Restart. Confirme a reinicialização
    clicando em yes![A screenshot of a computer AI-generated content may
    be incorrect.](./media/image36.png) ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image37.png)

21. Na página Web App **Overview**, navegue até a barra de comando e
    clique em **Browse**, que o levará ao aplicativo Web.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image38.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

22. Na página do aplicativo Web do **Azure AI**, digite o seguinte texto
    e clique no ícone **Submit** conforme mostrado na imagem abaixo.

+++Describe in more detail the risks from market volatility+++ 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

23. Na seção de **Chat session**, selecione o link de referências e
    observe os detalhes do documento pesquisado no lado direito da
    página.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

24. Na página do aplicativo Web do **Azure AI**, digite o seguinte texto
    e clique no ícone **Submit,** conforme mostrado na imagem abaixo.

+++How does Woodgrove Financial handle payroll taxes for employees
outside the U.S.?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png) ![A screenshot of a chat AI-generated
content may be incorrect.](./media/image44.png)

25. Na página do aplicativo Web do **Azure AI**, digite o seguinte texto
    e clique no ícone **Submit,** conforme mostrado na imagem abaixo.

+++What is FORM 10-K and explain?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image45.png)

**Tarefa 4: Excluir o recurso do Azure OpenAI**

1.  Para o recurso Azure OpenAI, digite **Resource groups** na barra de
    pesquisa do portal do Azure, navegue e clique em **Resource groups**
    em **Services**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

2.  Clique em seu grupo de recursos.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  Em uma página overview do grupo de recursos, selecione **Delete
    resource group**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

4.  No painel **Delete Resources**, exibido no lado direito, digite o
    **nome do grupo de recursos** e clique no botão **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

5.  Na caixa de diálogo **Delete confirmation**, clique no botão
    D**elete**.

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image49.png)

**Resumo**:

Este laboratório oferece experiência prática na implementação de uma
solução de AI conversacional usando o Azure RAG Accelerator. Você
iniciou o laboratório implementando a infraestrutura necessária usando
um modelo personalizado. Depois de verificar a implementação
bem-sucedida de vários recursos do Azure, você testou a solução fazendo
upload de documentos e usando o aplicativo Web para realizar consultas e
recuperar informações. Por fim, você excluiu o grupo de recursos para
gerenciar os recursos com eficiência. Este laboratório demonstrou como
aprimorar a interação e a recuperação de dados usando tecnologias
avançadas de AI.
