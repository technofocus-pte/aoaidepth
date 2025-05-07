# Caso de uso 12 – Modere texto e imagens com segurança de conteúdo no Azure AI Content Safety Studio

**Introdução**

O Azure AI Content Safety detecta conteúdo nocivo gerado por usuários e
por AI em aplicativos e serviços. O Azure AI Content Safety inclui APIs
de texto e imagem que permitem detectar material nocivo. O Microsoft
Azure também possui um Content Safety Studio interativo que permite
visualizar, explorar e testar códigos de exemplo para detectar conteúdo
nocivo em diferentes modalidades.

O software de filtragem de conteúdo pode ajudar seu aplicativo a cumprir
regulamentações ou manter o ambiente pretendido para seus usuários.

[O Azure AI Content Safety
Studio](https://contentsafety.cognitive.azure.com/) é uma ferramenta
online projetada para lidar com conteúdo potencialmente ofensivo,
arriscado ou indesejado usando modelos de ML de moderação de conteúdo de
ponta. Ele fornece modelos e fluxos de trabalho personalizados,
permitindo que os usuários escolham e criem seu próprio sistema de
moderação de conteúdo. Os usuários podem carregar seu próprio conteúdo
ou experimentá-lo com o conteúdo de amostra fornecido.

No Content Safety Studio, os seguintes recursos do serviço Azure AI
Content Safety estão disponíveis:

- **Moderar conteúdo de texto** : com a ferramenta de moderação de
  texto, você pode facilmente executar testes em conteúdo de texto. Seja
  para testar uma única frase ou um conjunto de dados inteiro, esta
  ferramenta oferece uma interface amigável que permite avaliar os
  resultados dos testes diretamente no portal.

- **Moderar conteúdo de imagem** : com a ferramenta de moderação de
  imagem, você pode facilmente executar testes em imagens para garantir
  que elas atendam aos seus padrões de conteúdo.

- **Monitorar a atividade online** : a poderosa página de monitoramento
  permite que você acompanhe facilmente o uso e as tendências da API de
  moderação em diferentes modalidades. Com esse recurso, você pode
  acessar informações detalhadas sobre as respostas, incluindo
  distribuição por categoria e severidade, latência, erros e detecção de
  listas de bloqueio. Essas informações fornecem uma visão geral
  completa do desempenho da moderação do seu conteúdo, permitindo que
  você otimize seu fluxo de trabalho e garanta que seu conteúdo seja
  sempre moderado de acordo com suas especificações exatas.

**Objetivos**

- Implementar um recurso do Azure AI Content Safety.

- Criar um recurso de Azure AI e explorar o Content Safety.

- Configurar o recurso de **Azure AI** no **Azure AI Studio** e explorar
  os recursos de **segurança de conteúdo**, com ênfase na **moderação de
  texto e imagem**.

## **Tarefa 1: Criar recurso do Azure AI Content Safety**

1.  Abra seu navegador, navegue até a barra de endereço, digite ou cole
    o seguinte URL:
    [<https://portal.azure.com/>](https://portal.azure.com/) e pressione
    o botão **Enter** .

> ![](./media/image1.png)

2.  Na janela **Sign in**, digite o **Username** e clique no botão
    **Next**.

![](./media/image2.png)

3.  Em seguida, digite a senha e clique no botão **Sign.**

> ![A screenshot of a login box Description automatically
> generated](./media/image3.png)

4.  Na janela **Stay signed in?** clique no botão **Yes**.

> ![A screenshot of a computer Description automatically
> generated](./media/image4.png)

5.  Na página inicial do portal do Azure, clique no **Azure portal
    menu** representado por três barras horizontais no lado esquerdo da
    barra de comandos do Microsoft Azure, conforme mostrado na imagem
    abaixo.

> ![A screenshot of a computer Description automatically
> generated](./media/image5.png)

6.  Navegue e clique em **+ Create a resource**.

> ![A screenshot of a computer Description automatically
> generated](./media/image6.png)

7.  Na página **Marketplace,** na barra de pesquisa **de Search services
    and marketplace**, digite **Azure AI Content Safety** e pressione a
    tecla **Enter** . Em seguida, navegue até a seção **Azure AI Content
    Safety,** clique no menu suspenso do botão **Create** e selecione
    **Azure AI Content Safety,** conforme mostrado na imagem abaixo.

> ![](./media/image7.png)
>
> ![](./media/image8.png)

8.  Na janela **Create Azure OpenAI**, na aba **Basics**, insira os
    seguintes detalhes e clique no botão **Review+create**.

[TABLE]

> ![](./media/image9.png)

9.  Na aba **Review+submit**, depois que a validação for aprovada,
    clique no botão **Create**.

> ![](./media/image10.png)

10. Aguarde a conclusão da implementação, o que pode levar de 2 a 3
    minutos.

11. Na janela **Microsoft.CognitiveServicesContentSafety**, após a
    conclusão da implementação, clique no botão **Go to resource**.

![](./media/image11.png)

![](./media/image12.png)

![](./media/image13.png)

## Tarefa 2: Analisar o conteúdo do texto

1.  Na página **Content Safety**, navegue até **Moderate text content**
    e clique no link **Try it out**.

![](./media/image14.png)

2.  No painel **Settings**, selecione **AOAI-ContentSafetyXX** e clique
    em **Use resource**.

![](./media/image15.png)

3.  Na página **Content Safety**, navegue até **Moderate text content**
    e clique no link **Try it out**.

![](./media/image14.png)

4.  Na aba **Run a simple test**, selecione **Safe content**, conforme
    mostrado na imagem abaixo.

![](./media/image16.png)

5.  Opcionalmente, você pode usar os controles deslizantes na aba
    **Configure filters** para modificar os níveis de severidade
    permitidos ou proibidos para cada categoria. Em seguida, clique no
    botão **Run test.**

![](./media/image17.png)

![](./media/image18.png)

6.  Role para baixo para visualizar os resultados. O serviço retorna
    todas as categorias detectadas, o nível de severidade de cada uma
    (0-Seguro, 2-Baixo, 4-Médio, 6-Alto) e um julgamento binário de
    **Allowed** ou **Reject** . O resultado é baseado nos filtros que
    você configurou.

![](./media/image19.png)

7.  Role para baixo e clique no botão **View Code**, conforme mostrado
    na imagem abaixo, para visualizar e copiar o código de exemplo, que
    inclui configuração para filtragem de severidade, listas de bloqueio
    e funções de moderação. Você poderá então implementar o código.

![](./media/image20.png)

![A screenshot of a computer program Description automatically
generated](./media/image21.png)

## Tarefa 3: Detectar ataques de entrada de usuário

1.  Voltar para o **Content Safety Studio**

![](./media/image22.png)

2.  Na página **Content Safety**, em **Explore safety solutions for
    Gen-AI,** navegue até **Prompt Shields** e clique no link **Try it
    out**.

![](./media/image23.png)

3.  Na aba **Set up sample**, selecione **Safe content,** conforme
    mostrado na imagem abaixo.

![](./media/image24.png)

4.  Opcionalmente, você pode usar os controles deslizantes na aba
    **Prompt shields** para modificar os níveis de severidade permitidos
    ou proibidos para cada categoria. Em seguida, clique no botão **Run
    test.**

![](./media/image25.png)

5.  Role para baixo e clique no botão **View Code**, conforme mostrado
    na imagem abaixo, para visualizar e copiar o código de exemplo, que
    inclui configuração para filtragem de severidade, listas de bloqueio
    e funções de moderação. Você pode então implementar o Código.

![](./media/image26.png)

![](./media/image27.png)

6.  Na aba **Set up sample**, selecione **User prompt attack content** e
    clique em **Run test,** conforme mostrado na imagem abaixo.

![](./media/image28.png)

![A screenshot of a computer Description automatically
generated](./media/image29.png)

## Tarefa 4: Analisar o conteúdo da imagem

1.  No painel Prompt Shields, clique em **Back**

![](./media/image30.png)

2.  Na página **Content Safety**, navegue até **Moderate image** e
    clique no link **Try it out**.

![](./media/image31.png)

3.  Na seção select a sample or upload your own, navegue e clique no
    link **Browse for a file**.

![](./media/image32.png)

**Observação** : O tamanho máximo para envio de imagens é de 4 MB, e as
dimensões das imagens devem estar entre 50 x 50 pixels e 2.048 x 2.048
pixels. As imagens podem estar nos formatos JPEG, PNG, GIF, BMP, TIFF ou
WEBP.

4.  Navegue até o local **C:\Labfiles** e selecione a imagem do
    **car-accident,** então clique no botão **Open**.

![](./media/image33.png)

5.  Opcionalmente, você pode usar controles deslizantes na aba
    **Configure filters** para modificar os níveis de severidade
    permitidos ou proibidos para cada categoria.

6.  Clique no botão **Run test**.

![](./media/image34.png)

7.  Role para baixo para visualizar os resultados do teste. O serviço
    retorna todas as categorias detectadas, o nível de severidade de
    cada uma (0-Seguro, 2-Baixo, 4-Médio, 6-Alto) e um julgamento
    binário de **Accept** ou **Reject**. O resultado é baseado nos
    filtros que você configurou.

![](./media/image35.png)

8.  Role para baixo e clique no botão **View Code**, conforme mostrado
    na imagem abaixo, para visualizar e copiar o código de exemplo, que
    inclui configuração para filtragem de severidade, listas de bloqueio
    e funções de moderação. Você poderá então implementar o código.

![](./media/image36.png)

![](./media/image37.png)

## Tarefa 5: Excluir o grupo de recursos

1.  Navegue até a página inicial do portal do Azure, digite **Resource
    groups** na barra de pesquisa do portal do Azure, navegue e clique
    em **Resource groups** em **Services**.

> ![A screenshot of a computer Description automatically
> generated](./media/image38.png)

2.  Clique no grupo de recursos que você tem para o recurso do Azure AI.

> ![](./media/image39.png)

3.  Na página inicial do **Resource group**, selecione **delete resource
    group**

![](./media/image40.png)

4.  No painel **Delete Resources** que aparece no lado direito, navegue
    até o campo **Enter “resource group name”** e, em seguida, clique no
    botão **Delete**.

![](./media/image41.png)

5.  Na caixa de diálogo **Delete confirmation**, clique no botão
    **Delete**.

> ![A screenshot of a computer error Description automatically
> generated](./media/image42.png)

6.  Clique no ícone do sino e você verá a notificação – **Deleted
    resource group AOAI-RG89.**

![A screenshot of a computer Description automatically
generated](./media/image43.png)

**Resumo**

Neste laboratório, você criou e configurou recursos do Azure para o
Azure AI Content Safety Studio, com foco específico na moderação de
conteúdo para texto e imagens, explorando as capacidades de moderação de
conteúdo de texto e imagem. Neste laboratório, você aprendeu como
implementar funcionalidades de moderação de conteúdo dentro do ambiente
Azure.
