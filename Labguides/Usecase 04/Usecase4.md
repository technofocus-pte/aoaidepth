# Caso de uso 04 – Criando um aplicativo de chat (usando .NET) usando Azure OpenAI Service e RAG

Este exemplo demonstra algumas abordagens para criar experiências
semelhantes ao ChatGPT em seus próprios dados usando o modelo Retrieval
Augmented Generation. Ele usa Azure OpenAI Service para acessar o modelo
ChatGPT (gpt-4o-mini), e Azure AI Search para indexação e recuperação de
dados.

O repositório inclui dados de exemplo para que esteja pronto para ser
testado de ponta a ponta. Neste aplicativo de exemplo, usamos uma
empresa fictícia chamada Contoso Electronics, e a experiência permite
que seus funcionários façam perguntas sobre os benefícios, políticas
internas, bem como descrições de cargos e funções.

![A diagram of a computer process Description automatically
generated](./media/image1.png)

- Interfaces de chat por voz, chat e perguntas e respostas

- Explora várias opções para ajudar os usuários a avaliar a
  confiabilidade das respostas com citações, rastreamento do conteúdo de
  origem, etc.

- Mostra possíveis abordagens para preparação de dados, construção
  imediata e orquestração de interação entre o modelo (ChatGPT) e o
  recuperador (Azure AI Search)

- Configurações diretamente na UX para ajustar o comportamento e
  experimentar opções

**Principais tecnologias utilizadas** -- Azure OpenAI Service, modelo
ChatGPT (gpt-4o-mini) e Azure AI Search

**Duração estimada -** 40 minutos

# Exercício 1: Implementar o aplicativo e testá-lo no navegador

## Tarefa 1: Ambiente de desenvolvimento aberto

1.  Abra seu navegador, navegue até a barra de endereço, digite ou cole
    a seguinte URL:
    +++https://github.com/technofocus-pte/azure-search-openai-demo-csharp.git+++
    e entre com sua conta do Github.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)

2.  Clique em **Fork**

> ![](./media/image3.png)

3.  Digite o nome do repositório e clique em **Create fork**

> ![](./media/image4.png)

4.  Clique em **Code -\> Codespaces -\> +**

> ![](./media/image5.png)

5.  Aguarde a configuração do ambiente. Leva de 5 a 10 minutos.

> ![A screenshot of a computer Description automatically
> generated](./media/image6.png)

## Tarefa 2: Provisionar os serviços necessários para criar e implementar o aplicativo de chat no Azure

1.  Execute o seguinte comando no Terminal. Copie o código e pressione
    Enter.

> +++azd auth login+++
>
> ![A screenshot of a computer Description automatically
> generated](./media/image7.png)

2.  O navegador padrão é aberto para inserir um código. Digite o código
    copiado e clique em **Next**

> ![A screenshot of a computer Description automatically
> generated](./media/image8.png)

![](./media/image9.png)

3.  Entre com suas credenciais do Azure.

![A screenshot of a computer Description automatically
generated](./media/image10.png)

![A screenshot of a computer error Description automatically
generated](./media/image11.png)

![A screenshot of a computer Description automatically
generated](./media/image12.png)

4.  Volte para a guia Github Codespace. Execute o comando abaixo para
    inicializar o ambiente do projeto no diretório atual. Insira o nome
    do ambiente como +++**chatragXXX+++** e pressione Enter.

> Nota: o nome do ambiente deve ser exclusivo
>
> +++azd env new+++

![](./media/image13.png)

5.  Execute o comando abaixo para provisionar os serviços para o Azure,
    crie o seu contêiner.

> +++azd env set AZURE_RESOURCE_GROUP ResourceGroup1+++
>
> ![A screenshot of a computer Description automatically
> generated](./media/image14.png)

6.  Executar azd up – isso provisionará recursos do Azure e implementará
    esse exemplo nesses recursos, incluindo a criação do índice de
    pesquisa com base nos arquivos encontrados na pasta ./data.

> **+++azd up+++**
>
> ![](./media/image15.png)

7.  Selecione os valores abaixo.

- **Select an Azure Subscription to use** : Selecione sua assinatura

- **Select an Azure location to use** : **East us2/west us2** (Às vezes,
  East US pode não estar disponível, escolha o local na lista mencionada
  abaixo.)

- Select existing resource group : Seu grupo de recursos existente (por
  exemplo :**ResourceGroup1 )**

> ![A screenshot of a computer Description automatically
> generated](./media/image16.png)
>
> ![](./media/image17.png)

7.  Aguarde até que o recurso seja provisionado completamente. Este
    processo levará de 5 a 10 minutos para criar todos os recursos
    necessários.

> ![A screenshot of a computer Description automatically
> generated](./media/image18.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image19.png)
>
> ![](./media/image20.png)

8.  Depois que o aplicativo for implementado com sucesso, você verá uma
    URL exibida no terminal. Copie a **URL**

> ![](./media/image21.png)

9.  Clique em **Open**

> ![A screenshot of a computer Description automatically
> generated](./media/image22.png)

10. Ele abre o aplicativo em uma nova guia.

> ![](./media/image23.png)

11. Abra um navegador, vá para <https://portal.azure.com> e entre com
    sua conta de assinatura do Azure.

12. Na página inicial, clique em **Resource groups**

> ![A screenshot of a computer Description automatically
> generated](./media/image24.png)

13. Clique no seu grupo de recursos.

> ![A screenshot of a computer Description automatically
> generated](./media/image25.png)

14. Certifique-se de que o recurso abaixo foi implementado com sucesso.

> ![A screenshot of a computer Description automatically
> generated](./media/image26.png)

![A screenshot of a computer Description automatically
generated](./media/image27.png)

![A screenshot of a computer Description automatically
generated](./media/image28.png)

> ![A screenshot of a computer Description automatically
> generated](./media/image29.png)

15. No grupo de recursos e clique no nome do recurso do **Azure
    OpenAI**.

> ![A screenshot of a computer Description automatically
> generated](./media/image30.png)

16. Na janela **Azure OpenAI**, clique em **Overview** no menu de
    navegação à esquerda, em seguida, na guia **Get Started**, clique no
    botão **Go to Azure OpenAI Studio** para abrir o **Azure OpenAI
    Studio** em um novo navegador.

> ![A screenshot of a computer Description automatically
> generated](./media/image31.png)

17. Certifique-se que **gpt-4o-mini**, **text-embedding-ada-002** foi
    implementado com sucesso .

> ![A screenshot of a computer Description automatically
> generated](./media/image32.png)

18. No grupo de recursos e clique no nome do recurso da **conta de
    armazenamento**.

> ![A screenshot of a computer Description automatically
> generated](./media/image33.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image34.png)

19. Agora abra a URL em um navegador

> ![A screenshot of a computer Description automatically
> generated](./media/image23.png)

20. Clique em **Chat**

> ![A screenshot of a computer Description automatically
> generated](./media/image35.png)

21. Na página do aplicativo da web **Blazor OpenAI**, digite o seguinte
    texto e clique no ícone **Submit** conforme mostrado na imagem
    abaixo.

> **+++What is included in my Northwind Health Plus plan that is not in
> standard?+++**
>
> ![A screenshot of a computer Description automatically
> generated](./media/image36.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image37.png)

22. Na página do aplicativo da web **Blazor OpenAI**, digite o seguinte
    texto e clique no ícone **Submit** conforme mostrado na imagem
    abaixo.

> **+++Can I use out-of-network providers?+++**
>
> ![A screenshot of a computer Description automatically
> generated](./media/image38.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image39.png)

23. Na página do aplicativo da web **Blazor OpenAI**, digite o seguinte
    texto e clique no ícone **Submit** conforme mostrado na imagem
    abaixo.

> **+++Are there any exclusions or restrictions?+++**
>
> ![A screenshot of a computer Description automatically
> generated](./media/image40.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image41.png)

24. Na página do aplicativo da web **Blazor OpenAI**, digite o seguinte
    texto e clique no ícone **Submit** conforme mostrado na imagem
    abaixo.

> **+++What does a Product Manager do?+++**
>
> ![A screenshot of a computer Description automatically
> generated](./media/image42.png)

25. Clique em **Documents**

> ![A screenshot of a computer Description automatically
> generated](./media/image43.png)

## **Tarefa 3: Limpar todos os recursos**

1.  Volte para **Azure portal -\> Resource group-\> Resource group
    name**

> ![A screenshot of a computer Description automatically
> generated](./media/image44.png)

2.  Selecione todos os recursos e clique em **Delete** conforme mostrado
    na imagem abaixo. (**NÃO EXCLUA** o grupo de recursos)

> ![](./media/image45.png)

3.  Digite delete na caixa de texto e clique em **Delete**

> ![](./media/image46.png)

4.  Confirme a exclusão clicando em **Delete**

> ![](./media/image47.png)

5.  Volte para a guia do portal do Github e atualize a página.

> ![](./media/image48.png)

6.  Clique em **Code**, selecione a ramificação criada para este
    laboratório e clique em **Delete**

> ![](./media/image49.png)

7.  Confirme a exclusão da ramificação clicando no botão **Delete**

![](./media/image50.png)

**Resumo:**

Este caso de uso ensiou você a implementar um aplicativo de chat para o
padrão Retrieval Augmented Generation executado no Azure, a usar Azure
AI Search para recuperação e Azure OpenAI and LangChain Large Language
Models (LLMs) para potencializar experiências no estilo ChatGPT e
perguntas e respostas.
