**Introdução**

Este exemplo demonstra algumas abordagens para criar experiências
semelhantes ao ChatGPT em seus próprios dados usando o padrão Retrieval
Augmented Generation (RAG). Ele usa Azure OpenAI Service para acessar o
modelo ChatGPT (gpt-35-turbo) e Azure Cognitive Search para indexação e
recuperação de dados.

O repositório inclui dados de amostra, portanto, está pronto para ser
testado de ponta a ponta. Neste aplicativo de exemplo, usamos uma
empresa fictícia chamada Contoso Electronics, e a experiência permite
que seus funcionários façam perguntas sobre os benefícios, políticas
internas, bem como descrições de cargos e funções.

Este caso de uso mostra o processo de desenvolvimento de um aplicativo
de chat sofisticado usando o modelo Retrieval Augmented Generation (RAG)
na plataforma Azure. Ao usar Azure OpenAI Service e Azure Cognitive
Search, você criará um aplicativo de chat que pode responder a perguntas
de forma inteligente usando seus próprios dados. Este laboratório usa
uma empresa fictícia, a Contoso Electronics, como um estudo de caso para
demonstrar como criar uma experiência semelhante ao ChatGPT em dados
corporativos, abrangendo aspectos como benefícios de funcionários,
políticas internas e funções de trabalho.

![RAG Architecture](./media/image1.png)

**Objetivo**

- Instalar Azure CLI e Node.js em sua máquina local.

- Atribuir uma função de proprietário ao usuário.

- Instalar a extensão Dev Containers e configurar o ambiente de
  desenvolvimento.

- Implantar um aplicativo de chat no Azure e usá-lo para obter respostas
  de arquivos PDF.

- Excluir os recursos e modelos implantados.

## Tarefa 1: Instalar Azure CLI e definir o escopo da política para máquina local

1.  Na barra de pesquisa do Windows, digite **PowerShell**. Na caixa de
    diálogo **PowerShell**, navegue e clique em **Run as
    administrator**. Se você vir a caixa de diálogo - **Do you want to
    allow this app to make changes to your device?** - clique no botão
    **Yes**.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)

2.  Execute o seguinte comando para instalar o Azure CLI no the
    PowerShell

PowerShell copy

> **winget install microsoft.azd**

![A screen shot of a computer Description automatically
generated](./media/image3.png)

3.  Execute o comando abaixo para definir a política como
    **Unrestricted** e digite **A** quando solicitado a alterar a
    política de execução.

> **Set-ExecutionPolicy Unrestricted**
>
> ![A computer screen with white text Description automatically
> generated](./media/image4.png)

## Tarefa 2: Instalar Node.js

1.  Abra seu navegador, navegue até a barra de endereço, digite ou cole
    a seguinte URL: +++https://nodejs.org/en/download/+++, em seguida,
    pressione **Enter**.

![](./media/image5.png)

2.  Selecione e clique em **Windows Installer**.

![](./media/image6.png)

3.  O arquivo **Node-V** será baixado. Clique no arquivo baixado para
    configurar **Node.js**

![A screenshot of a computer Description automatically
generated](./media/image7.png)

4.  Na janela **Welcome to the Node.js Setup Wizard**, clique no botão
    **Next**.

![](./media/image8.png)

5.  Na janela **End-User License Agreement**, selecione o botão **I
    accept the terms in the License agreement** e clique no botão
    **Next**.

![A screenshot of a software setup Description automatically
generated](./media/image9.png)

6.  Na janela **Destination Folder**, clique no botão **Next**.

![A screenshot of a computer Description automatically
generated](./media/image10.png)

7.  Na janela **Custom Setup**, clique no botão **Next**.

![](./media/image11.png)

![](./media/image12.png)

8.  Na janela **Ready to install Node.js**, clique em **Install.**

![A screenshot of a software Description automatically
generated](./media/image13.png)

9.  Na janela **Completing the Node.js Setup Wizard**, clique no botão
    **Finish** para concluir o processo de instalação.

![A screenshot of a computer Description automatically
generated](./media/image14.png)

## Task 3: Recuperar o nome e o local do grupo de recursos

1.  Abra seu navegador, navegue até a barra de endereço e digite ou cole
    a seguinte URL: +++https://portal.azure.com/+++, e, em seguida,
    pressione **Enter**.

> ![A screenshot of a computer Description automatically
> generated](./media/image15.png)

2.  Na janela **Microsoft Azure**, use **User Credentials** para fazer
    login no Azure.

![](./media/image16.png)

3.  Em seguida, digite a senha e clique no botão **Sign in.**

> ![](./media/image17.png)

4.  Na janela **Stay signed in?**, clique no botão **Yes**.

> ![Graphical user interface, application Description automatically
> generated](./media/image18.png)

5.  Digite +++**Resource group+++** na barra de pesquisa e selecione
    **Resource groups**.

> ![](./media/image19.png)

6.  Clique no seu **Resource group** atribuído.

![](./media/image20.png)

7.  Na página **Resource group**, copie **resource group name and
    location** e cole-os em um bloco de notas e, em seguida, **salve** o
    bloco de notas para usar as informações nas próximas tarefas.

![](./media/image21.png)

## Tarefa 4: Criar o serviço de pesquisa de AI

1.  No portal do Azure, digite +++**AI search+++** na barra de pesquisa
    e selecione **AI Search**

![](./media/image22.png)

2.  Clique em + **Create**.

![](./media/image23.png)

3.  Selecione os valores abaixo e clique em **Review + Create**.

&nbsp;

1)  Subscription: **Your Azure subscription**.

2)  Resource group - **Selecione seu grupo de recursos existente**

3)  Service name - **aisearchXXXX(XXXXX pode ser o ID do laboratório)**

4)  Location : **Central US** /Localização perto de você

5)  Pricing tier: Standard

![](./media/image24.png)

4.  Clique em **Create** agora.

![](./media/image25.png)

5.  Aguarde a implementação e clique em **Go to resource**.

> ![A screenshot of a computer Description automatically
> generated](./media/image26.png)
>
> ![](./media/image27.png)

6.  Na página **Overveiw** de **AI Search**, No painel de navegação do
    lado esquerdo, em **Settings**, selecione **Semantic ranker**

![](./media/image28.png)

7.  Na guia **Semantic ranker,** selecione **Standard** e clique em
    **Select Plan.**

> ![](./media/image29.png)

8.  Selecione **Yes**

> ![](./media/image30.png)

9.  Você verá uma notificação:**Successfully updated semantic ranker to
    standard plan.**

> ![](./media/image31.png)

10. Abra um bloco de notas e anote o nome da AI Search, nome e
    localização do grupo de recursos. Vamos usá-los mais tarde para nos
    comunicarmos com o serviço.

> ![](./media/image32.png)

## Tarefa 5: Executar o Docker

1.  Na caixa de pesquisa do Windows, digite Docker e clique em **Docker
    Desktop**.

![](./media/image33.png)

2.  Execute o Docker Desktop.

![](./media/image34.png)

## **Tarefa 6: Instalar a extensão Dev Containers**

1.  Na caixa de pesquisa do Windows, digite Visual Studio e clique em
    **Visual Studio Code**.

> ![](./media/image35.png)

2.  Abra seu navegador, navegue até a barra de endereço, digite ou cole
    a seguinte URL:
    +++https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers+++
    em seguida, pressione **Enter**.

> ![A screenshot of a computer Description automatically
> generated](./media/image36.png)

3.  Na página Dev Containers, selecione no botão **Install**

![](./media/image37.png)

4.  A caixa de diálogo **Visual Studio Code is required to install this
    extension.** é exibida, clique no botão **Continue**.

![](./media/image38.png)

5.  A caixa de diálogo **This site is trying to open Visual Studio
    Code.** é exibida, clique no botão **Open**

![](./media/image39.png)

6.  No Visual Studio, clique no botão **Install** em **Dev Containers**.

![](./media/image40.png)

![A screenshot of a computer Description automatically
generated](./media/image41.png)

## Tarefa 7: Ambiente de desenvolvimento aberto

1.  Abra seu navegador, navegue até a barra de endereço, digite ou cole
    a seguinte URL:

+++<https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo>+++
em seguida, pressione **Enter**.

![A white background with black text Description automatically
generated](./media/image42.png)

2.  A caixa de diálogo **This site is trying to open Visual Studio
    Code.** é exibida, clique no botão **Open**

> ![](./media/image43.png)

3.  A caixa de diálogo **Allow ‘Dev Containers’ extension to open this
    URI?** é exibida, clique no botão **Open**

![](./media/image44.png)

4.  A Caixa de diálogo **Cloning a repository in a Dev Container may
    execute arbitrary code.** é exibida, clique no botão **Got It**

> ![](./media/image45.png)

5.  Iniciar o Dev Container levará de 13 a 15 minutos. Após a
    implementação, pressione **Enter**.

![](./media/image46.png)

6.  Pressione qualquer tecla para fechar o terminal.

> ![A screenshot of a computer Description automatically
> generated](./media/image47.png)

## Tarefa 8: Implemntar o aplicativo de chat no Azure

1.  Entre no Azure com o Azure Developer CLI. Execute o seguinte comando
    no Terminal:

> BashCopy
>
> **azd auth login**
>
> ![](./media/image48.png)

2.  O navegador padrão é aberto para entrar. Entrar com sua conta de
    assinatura do Azure.

![](./media/image49.png)

> ![](./media/image50.png)

3.  Feche o navegador.

> ![A screenshot of a computer Description automatically
> generated](./media/image51.png)

4.  Depois de fazer login, os detalhes do login do Azure são preenchidos
    no terminal.

> ![A screenshot of a computer Description automatically
> generated](./media/image52.png)

5.  Crie um novo ambiente azd. Execute o seguinte comando no Terminal:

Copy

**azd env new**

6.  Insira o novo nome do ambiente como +++**chatapprag+++**

![](./media/image53.png)

> ![A screenshot of a computer Description automatically
> generated](./media/image54.png)

7.  Atribua o grupo de recursos do Azure existente. Execute o seguinte
    comando no Terminal:

> azd env set AZURE_RESOURCE_GROUP {Name of existing resource group}
>
> azd env set AZURE_LOCATION {Location of existing resource group}
>
> ![](./media/image55.png)

8.  Atribua o serviço existente de Azure AI Search. Execute o seguinte
    comando no Terminal:

> +++azd env set AZURE_SEARCH_SERVICE {Name of existing Azure AI Search
> service}+++
>
> +++azd env set AZURE_SEARCH_SERVICE_RESOURCE_GROUP {Name of existing
> resource group with ACS service}+++
>
> +++azd env set AZURE_SEARCH_SERVICE_LOCATION {Location of existing
> service}+++
>
> +++azd env set AZURE_SEARCH_SERVICE_SKU {Name of SKU}+++
>
> ![](./media/image56.png)

9.  Verifique os recursos existentes atribuídos, selecione Azure e
    escolha o arquivo **.env**

> ![](./media/image57.png)

10. Crie um novo ambiente azd:

> shellCopy
>
> **azd up**
>
> ![A screenshot of a computer Description automatically
> generated](./media/image58.png)

11. Selecione sua assinatura do Azure

> ![A screenshot of a computer Description automatically
> generated](./media/image59.png)

12. Quando solicitado, **Enter a value for the
    ‘documentIntelligenceResourceGroupLocation’ infrastructure
    parameter** selecione **West US2.**

> ![A screenshot of a computer Description automatically
> generated](./media/image60.png)

13. Quando solicitado, **Enter a value for the
    ‘openAiResourceGroupLocation’ infrastructure parameter** selecione
    **France Central .**

> ![A screenshot of a computer Description automatically
> generated](./media/image61.png)

14. Aguarde até que o aplicativo seja implementado. Pode levar **de 35 a
    40** minutos para que a implementação seja concluída.

> ![A screenshot of a computer Description automatically
> generated](./media/image62.png)
>
> ![](./media/image63.png)
>
> ![](./media/image64.png)
>
> ![](./media/image65.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image66.png)

15. Depois que o aplicativo for implementado com êxito, você verá uma
    URL impressa no console. Clique nesse URL para interagir com o
    aplicativo em seu navegador. Ele terá a seguinte aparência:

> ![](./media/image67.png)

16. Abra seu navegador, navegue até a barra de endereço, cole o link.
    Agora, o grupo de recursos será aberto em um novo navegador.

![A screenshot of a computer Description automatically
generated](./media/image68.png)

![A screenshot of a computer Description automatically
generated](./media/image69.png)

## Tarefa 9: Verificar os recursos implementados no portal do Azure

1.  Selecione **Resource groups**

> ![](./media/image70.png)

2.  Clique no seu **Resource group** atribuído.

![](./media/image71.png)

3.  Certifique-se de que os recursos abaixo foram implementados com
    sucesso:

- Azure App Service

- Azure Application Insights

- Container App

- Container registry

- Azure OpenAI

- Azure Document Intelligence

- Azure Search Service

- Azure Storage Account

- Azure Speech Service

![](./media/image72.png)

![](./media/image73.png)

4.  No grupo de recursos e clique em **AI Search service.**

> ![](./media/image74.png)

5.  Certifique-se de que os índices sejam implementados com sucesso.

> ![](./media/image75.png)

6.  Volte para o grupo de recursos e clique em **Storage account**

> ![](./media/image76.png)

7.  No menu de navegação à esquerda, clique em **Containers**,
    certifique-se de que os dados sejam implantados com sucesso.

> ![](./media/image77.png)

## Tarefa 10: Usar o aplicativo de chat para obter respostas de arquivos PDF

1.  Aguarde a conclusão da implementação do aplicativo web.

> ![](./media/image78.png)

2.  Na página do aplicativo da web **GPT + Eneterprise data |Sample**,
    digite o seguinte texto e clique no ícone **Submit** conforme
    mostrado na imagem abaixo.

> **What happens in a performance review?**

![](./media/image79.png)

![A screenshot of a computer Description automatically
generated](./media/image80.png)

3.  Na resposta, selecione uma **citação**.

![](./media/image81.png)

4.  No painel direito, use as guias para entender como a resposta foi
    gerada.

[TABLE]

![](./media/image82.png)

![](./media/image83.png)

![](./media/image84.png)

5.  Selecione novamente a guia escolhida para fechar o painel.

6.  A inteligência do chat é determinada pelo modelo OpenAI e pelas
    configurações usadas para interagir com o modelo.

7.  Selecione **Developer settings**.

![](./media/image85.png)

![](./media/image86.png)

[TABLE]

8.  Marque a caixa de seleção **Suggest follow-up questions** e faça a
    mesma pergunta novamente.

![](./media/image87.png)

9.  Digite o texto a seguir e clique no ícone **Submit**, conforme
    mostrado na imagem abaixo.

> What happens in a performance review?

![](./media/image88.png)

10. O chat retornou perguntas de acompanhamento sugeridas, como as
    seguintes:

![](./media/image89.png)

11. Na guia **Settings**, desmarque**Use semantic ranker for
    retrieval**.

![](./media/image90.png)

![](./media/image91.png)

12. Digite o texto a seguir e clique no ícone **Submit**, conforme
    mostrado na imagem abaixo.

> What happens in a performance review?

![](./media/image92.png)

![](./media/image93.png)

## Tarefa 11: Excluir os recursos

1.  Para excluir o Grupo de recursos, digite **Resource groups** na
    barra de pesquisa do portal do Azure, navegue e clique em **Resource
    groups** em **Services**.

> ![A screenshot of a computer Description automatically
> generated](./media/image94.png)

2.  Clique no grupo de recursos de aplicativo web de exemplo.

> ![](./media/image95.png)

3.  Na página inicial do grupo de recursos, selecione **todos os
    recursos.**

![](./media/image96.png)

4.  Selecione **Delete**

![](./media/image97.png)

![](./media/image98.png)

**Resumo**

Neste laboratório, você aprendeu a configurar e implementar um
aplicativo de chat inteligente usando o pacote de ferramentas e serviços
do Azure. Começando com a instalação de ferramentas essenciais como
Azure CLI e Node.js, você configurou seu ambiente de desenvolvimento
usando Dev Containers no Visual Studio Code. Você implementou um
aplicativo de chat que utiliza Azure OpenAI e Azure Cognitive Search
para responder a perguntas de arquivos PDF. Por fim, você excluiu os
recursos implementados para gerenciar recursos com eficiência. Essa
experiência prática o equipou com as habilidades para desenvolver e
gerenciar aplicativos de bate-papo inteligentes usando o modelo
Retrieval Augmented Generation no Azure.
