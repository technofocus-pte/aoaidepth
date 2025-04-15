# Caso d'uso 10- Creazione di un'app Web e di un bot agente virtuale con dati personalizzati utilizzando Azure OpenAI Service

**Introduzione:**

Azure OpenAI sui dati funziona con i potenti modelli linguistici ChatGPT
(gpt-35-turbo) e GPT-4 di OpenAI, consentendo loro di fornire risposte
basate sui dati. È possibile accedere ad Azure OpenAI sui dati usando
un'API REST o l'interfaccia basata sul Web in Azure OpenAI Studio per
creare una soluzione che si connette ai dati per abilitare un'esperienza
di chat migliorata.

Una delle funzionalità principali di Azure OpenAI sui dati è la capacità
di recuperare e utilizzare i dati in modo da migliorare l'output del
modello. Azure OpenAI sui dati, insieme a Azure Cognitive Search,
determina quali dati recuperare dall'origine dati designata in base
all'input dell'utente e alla cronologia delle conversazioni fornita.
Questi dati vengono quindi aumentati e reinviati come prompt al modello
OpenAI, con le informazioni recuperate aggiunte al prompt originale.
Anche se i dati recuperati vengono aggiunti al prompt, l'input
risultante viene comunque elaborato dal modello come qualsiasi altro
prompt. Una volta recuperati i dati e inviato il prompt al modello, il
modello utilizza queste informazioni per fornire un completamento.

**Obiettivi**

- Per creare un account di archiviazione, un contenitore e un servizio
  di Azure cognitive search nel portale di Azure.

- Per distribuire gpt-3-turbo e il modello incorporato in Azure AI
  Studio e per aggiungere dati in Chat Playground.

- Per testare la configurazione dell'assistente in Chat playground
  inviando query nella sessione di chat.

- Per avviare un copilot e avviare una conversazione con il bot

- Per avviare una nuova app e avviare una conversazione con l'app
  copilot.

- Per eliminare gpt-3-turbo e il modello incorporato, l'account di
  archiviazione di Azure, il Cognitive search service e la nuova app
  Web.

## Esercizio 1- Creare un Azure Storage Account e Azure cognitive Search usando il portale

### Attività 1: Creare una risorsa Azure OpenAI

1.  Aprire il browser, andare alla barra degli indirizzi e digitare o
    incollare il seguente URL:+++<https://portal.azure.com/+++>, quindi
    premere il pulsante **Enter**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  Nella finestra **Microsoft Azure,** usare **User Credentials** per
    accedere ad Azure.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

3.  Quindi, inserire la password e fare clic sul pulsante **Sign in**.

![A screenshot of a login box AI-generated content may be
incorrect.](./media/image3.png)

4.  Nella ** **finestra **Stay signed in?**, fare clic sul pulsante
    **Yes**.

5.  Nella home page del portale di Azure, fare clic sul **menu del
    portale di Azure** rappresentato da tre barre orizzontali sul lato
    sinistro della barra dei comandi di Microsoft Azure, come illustrato
    nell'immagine seguente.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

6.  Navigare e fare clic su **+ Create a resource. **

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

7.  Nella pagina **Create a resource**, nella barra di ricerca **Search
    services and marketplace,** digitare **Azure OpenAI**, quindi
    premere il pulsante **Enter**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

8.  Nella pagina **Marketplace** passare alla sezione **Azure OpenAI**,
    fare clic sull'elenco a discesa del pulsante **Create**, quindi
    selezionare **Azure OpenAI** come illustrato nell'immagine. (Nel
    caso in cui tu abbia già cliccato sul pulsante **Azure OpenAI**,
    quindi fare clic sul pulsante **Create **nella pagina **Azure
    OpenAI**).

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

9.  Nella finestra **Create Azure OpenAI**, nella scheda **Basics**,
    immettere i dettagli seguenti e fare clic sul pulsante **Next**.

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image8.png)

10. Nella scheda **Network**, lasciare tutti i pulsanti di opzione nello
    stato predefinito e fare clic sul pulsante **Next**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

11. Nella scheda **Tag**, lasciare tutti i campi nello stato predefinito
    e fare clic sul pulsante **Next**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

12. Nella scheda **Review+submit**, una volta superata la convalida,
    fare clic sul pulsante **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

13. Attendere il completamento della distribuzione. L'implementazione
    richiederà circa 2-3 minuti.

14. Nella finestra **Microsoft.CognitiveServicesOpenAI**, al termine
    della distribuzione, fare clic sul pulsante **Go to resource**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

### Attività 2: Creare un Azure Storage Account usando il portale

1.  Accedere alla pagina +++<https://portal.azure.com/+++>

2.  Fare clic sul **menu del portale**, quindi selezionare **+ Create a
    resource**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

3.  Nella casella di ricerca  **Create a resource**, digitare **Storage
    account** e quindi fare clic su **storage account**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

4.  Nella pagina **Marketplace,** fare clic sulla sezione **Storage
    account**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

5.  Nella finestra **Storage account,** fare clic sul pulsante
    **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

6.  Nella finestra **Create a storage account**, nella scheda
    **Basics**, immettere i dettagli seguenti per creare un account di
    archiviazione e quindi fare clic su **Review**

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

7.  Nella scheda **Review**, fare clic sul pulsante **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

8.  Questo nuovo account di archiviazione di Azure è ora configurato per
    ospitare i dati per un Azure Data Lake. Fare clic sul pulsante **Go
    to resource**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

9.  Dopo la distribuzione dell'account, le opzioni relative ad Azure
    Data Lake sono disponibili nella pagina **Overview**. Nel riquadro
    di navigazione a sinistra, andare alla sezione **Data storage**,
    quindi fare clic su **Containers**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

10. Sulla pagina** azureopenaistorageXX | Containers**, fare clic
    su** +Container.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

11. Nel riquadro **New container** visualizzato sul lato destro,
    immettere il **nome** del contenitore come +++**source**+++ e fare
    clic sul pulsante **Create**.

![A screenshot of a phone AI-generated content may be
incorrect.](./media/image22.png)

12. Sulla pagina **azureopenaistorageXX | Containers**, selezionare il
    contenitore **source**\*\*.\*\*

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

13. Nella pagina **source container**, fare clic sul pulsante
    **Upload**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

14. Nel riquadro ** Upload blob,** fare clic su **Browse for file**,
    passare al percorso **C:\Labfiles** e selezionare
    **TF-AzureOpenAI.pdf**, quindi fare clic sul pulsante **Open**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

! \[\](./media/image50.png)

15. Nel riquadro ** Upload blob,** fare clic sul pulsante **Upload**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

16. Verrà visualizzata una notifica: **Successfully uploaded blob**
    quando il caricamento ha esito positivo.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

### Attività 3: Creare un servizio di AzureAI Search nel portale 

1.  Sulla pagina **azureopenaistorageXX | Containers**, fare clic su
    **Home** per tornare alla home page del portale di Azure.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

2.  Nella home page del portale di Azure, fare clic su **+ Create
    Resource**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

3.  Nella barra di ricerca **Create a resource page,** digitare **Azure
    AI Search** e fare clic su ** azure ai search** visualizzata.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

4.  Fare clic sulla sezione **azure ai search**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

5.  Nella pagina **Azure AI Search,** fare clic sul pulsante **Create**.

6.  ! \[\](./media/image58.png)

7.  Nella pagina **Create a search service**, fornire le seguenti
    informazioni e fare clic sul pulsante ** Review+create**.

[TABLE]

> ![A screenshot of a search service AI-generated content may be
> incorrect.](./media/image33.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image34.png)

8.  Una volta superata la convalida, fare clic sul pulsante **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

9.  Al termine della distribuzione, fare clic sul pulsante **Go to
    resource**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

10. Nella pagina Panoramica di **mysearchserviceXX**. Nel riquadro di
    spostamento a sinistra, nella sezione **Settings**, selezionare
    **Semantic ranker**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

11. Nella scheda **Semantic ranker,** selezionare il riquadro
    **Standard** e fare clic su ** Select plan.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

12. Vedrai una notifica - **Successfully updated semantic ranker to free
    plan**

## Esercizio-2: Aggiungere i dati con Azure OpenAI Studio 

### Attività 1: Distribuire gpt-35-turbo e modelli incorporati in Azure AI Studio

1.  Tornare al portale di Azure e cercare Azure OpenAI e selezionarlo.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

2.  Selezionare il tuo servizio **Azure OpenAI** .

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

3.  Nella finestra **AzureOpenAI,** fare clic su **Overview **nel menu
    di spostamento a sinistra, quindi fare clic sul pulsante ** Explore
    Azure AI Foundry portal** per accedere al **portale di Azure AI
    Foundry** in un nuovo browser

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

4.  In Homepage di  **Azure AI Foundry** |**Azure OpenAI Studio,**
    selezionare **Deployment ** dal menu di spostamento a sinistra.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image43.png)

5.  Nella finestra **Deployments, **visualizzare **+Deploy model** e
    selezionare **Deploy base model.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image44.png)

6.  Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **gpt-4**, quindi fare clic sul pulsante **Confirm**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image45.png)

7.  Nella finestra di dialogo **Deploy model**, inserire i seguenti
    dettagli e fare clic sul pulsante **Create**.

    - Selezionare il modello: **gpt-35-turbo**

    - Deployment Name: inserire **gpt-35-turbo**

    - Selezionare **Standard** come **Deployment type**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image46.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image47.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image48.png)

8.  Nella finestra **Deployments, **visualizzare **+Deploy model** e
    selezionare **Deploy base model.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image49.png)

9.  Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **text-embedding-ada-002,** quindi fare clic sul
    pulsante **Confirm**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

10. Nella finestra di dialogo **Deploy model**, in **Deployment name**
    immettere

> +++text-embedding-ada-002+++, selezionare il **tipo Standard** come
> **Deployment** e fare clic sul pulsante **Deploy.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image51.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image52.png)

11. In Home page del ** Azure AI Foundry |Azure OpenAI Service**, nella
    sezione **Playgrounds,** fare clic su **Chat**.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image53.png)

12. Nel riquadro **Chat playground**, menu a discesa** Add your data** e
    selezionare **+Add a data source**

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image54.png)

### Attività 2: Aggiungere i dati usando Azure OpenAI Studio

1.  Nella pagina **Select or add data source,** fare clic sull'elenco a
    discesa in ** Select or add data source**, quindi spostarsi e fare
    clic su **Azure Blob Storage**.

2.  Nella pagina ** Select or add data source**, in **Select or add data
    source**, immettere i dettagli seguenti e selezionare **Next.**

[TABLE]

3.  Selezionare la casella di controllo - **Add vector search to this
    search resource**.

4.  Selezionare un modello di incorporamento come
    **text-embedding-ada-002**, quindi fare clic sul pulsante **Next**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image55.png)

***Nota**: nel caso in cui si verifichi un errore: **Can‘t manage CORS
on this resource. Please select another storage resource**, quindi
sincronizzare l'ora della VM, come indicato nell'attività \#1.*

5.  Nella pagina **Add data**, nella scheda **Data management **a
    discesa il tipo di ricerca e selezionare **Hybrid+semantic.**

6.  Selezionare **chunk size** come **1024 (predefinito),** Quindi, fare
    clic su **Next.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

7.  Nel riquadro **Data connection**, selezionare la **API key **e fare
    clic sul pulsante **Next**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

8.  Nel riquadro ** Review and Finish**, rivedere i dettagli che hai
    inserito e fare clic sul pulsante **Save and close**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image58.png)

9.  I dati verranno aggiunti nel tuo **Chat Playground**. Ci vorranno
    circa 4-5 minuti.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image59.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image60.png)

### 

### Compito 3: Esplorare il completamento del testo nel Chat Playground

1.  Nella sezione **Chat session**, inserire il seguente messaggio nella
    casella di testo **User message** e fare clic sull'icona **Send**.

> CodeCopy 
>
> What is Azure OpenAI Service?

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image61.png)

![A screenshot of a chat box AI-generated content may be
incorrect.](./media/image62.png)

2.  Nella sezione **Chat session**, selezionare il collegamento dei
    riferimenti e osservare i dettagli del documento di ricerca sul lato
    destro della pagina.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image63.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image64.png)

## Esercizio 3: Distribuire un'app Web con dati personalizzati

### Attività 1: Distribuire un'app Web

1.  In Home page del **Azure AI Foundry |Azure OpenAI Service**,
    **riquadro** **Chat playground,** menu a discesa **Deploy**, quindi
    navigare e fare clic su ** as web app**.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image65.png)

2.  Nella finestra **Deploy to a web app,** selezionare il pulsante di
    opzione **Create a new web app** e immettere i dettagli seguenti:

[TABLE]

3.  Selezionare la casella di controllo **Enable chat history in the web
    app**

4.  Fare clic sul pulsante **Deploy.**

Nota : La distribuzione richiede 5-10 minuti

![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image66.png)

5.  Per controllare lo stato della distribuzione, fare clic su
    **Deployments **e selezionare **App deployment.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image67.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image68.png)

6.  Attendere il completamento della distribuzione. L'implementazione
    richiederà circa **10-15** minuti.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image69.png)

7.  Fare clic sull'applicazione web.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image70.png)

8.  Attendi 10 minuti, in modo che la configurazione dell'autenticazione
    possa essere applicata correttamente all'app.

9.  Dopo 10 minuti, fare clic sul pulsante **Refresh**.

10. Nella finestra di dialogo **Permissions requested**, fare clic sul
    pulsante **Accept** 

![A screenshot of a computer application AI-generated content may be
incorrect.](./media/image71.png)

11. A questo punto, l'app Web si aprirà in un nuovo browser.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image72.png)

12. Nella pagina dell' app Web di **Azure AI,** immettere il testo
    seguente e fare clic sull'**icona Submit** come illustrato
    nell'immagine seguente.

**CodeCopy** 

 

How do I get access to Azure OpenAI?  

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image74.png) ![A screenshot of a computer
AI-generated content may be incorrect.](./media/image75.png)

13. Allo stesso modo, incollare il seguente testo nella casella di testo
    e fare clic sull' icona **Send**.

**CodeCopy** 

**+++What is the expiry date of GPT-35-Turbo version 0301 and GPT-4
version 0314?+++** 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image76.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image77.png)

14. Aggiornare la pagina webapp e fare clic su ** Show chat history**.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image78.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image79.png)

15. Nella cronologia chat, fare clic su ** Accessing Azure OpenAI**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image80.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image81.png)

## Esercizio 4: Creare un'app Copilot con dati personalizzati

### Attività 1: Creare un chatbot con dati personalizzati

1.  In **Azure AI Foundry |Azure AI Studio Chat playground,** in **Add
    your data** selezionare **Remove data source**.

![A screenshot of a chat play AI-generated content may be
incorrect.](./media/image82.png)

2.  Nel riquadro **Chat playground**, menu a discesa **Add your data** e
    selezionare ** +Add a data source**

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image54.png)

3.  Nella pagina **Add data**, in** Select or add data source**,
    immettere i dettagli seguenti e selezionare **Next.**

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image83.png)
>
> ***Nota**: nel caso in cui si verifichi un errore: **Can‘t manage CORS
> on this resource. Please select another storage resource**, quindi
> sincronizzare l'ora della VM, come indicato nell'attività \#1.*

4.  Nella pagina **Add data**, nella scheda ** Data management ** a
    discesa il tipo di ricerca e selezionare **Keyword,** selezionare la
    dimensione del blocco come **1024 (impostazione predefinita)**
    Quindi, fare clic su **Next.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image84.png)

5.  Nel riquadro **Data connection**, selezionare **API key** e fare
    clic sul pulsante **Next**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

6.  Nel riquadro **Review and Finish,** esaminare i dettagli immessi e
    fare clic sul pulsante **Save and close**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image85.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image86.png) ![A screenshot of a chat AI-generated
content may be incorrect.](./media/image87.png)

7.  I dati verranno aggiunti nel tuo Chat Playground. Ci vorranno circa
    4-5 minuti.

### Attività 2: Creare un copilot con dati personalizzati da Azure OpenAI

1.  Accedere a +++<https://copilotstudio.microsoft.com/>+++ usando le
    credenziali di accesso di Azure.

2.  Una volta effettuato l'accesso, nella pagina Benvenuto in Microsoft
    Copilot Studio, selezionare il tuo Paese e fare clic su **Start free
    trial.**

![A person sitting at a computer AI-generated content may be
incorrect.](./media/image88.png)

3.  Viene visualizzata la home page di Copilot.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image89.png)

4.  Selezionare **Agents** nel riquadro a sinistra. E poi clicca su **+
    New agent**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image90.png)

5.  Selezionare **Skip to configure**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image91.png)

6.  Nella pagina **Create a copilot**, inserire il **nome** come
    +++**CopilotforAOAI**+++ e fare clic su **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image92.png)

7.  Cliccare su **Topics -\> System -\> Conversational boosting.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image93.png)

8.  Fare clic su **Edit **in ** Data sources** del nodo **Create
    generative answers**. Selezionare **Classic data** nel riquadro
    **Properties **che si apre.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image94.png)

9.  In **Azure OpenAI Services on your data,** fare clic su **Connection
    properties**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image95.png)

10. In questo modo viene aggiunta la connessione al servizio Azure
    OpenAI e viene aperto il riquadro delle proprietà della connessione.

11. Nel riquadro **Connection Properties**, in **General -\>
    Configuration,** immettere i dettagli seguenti

> Deployment – +++gpt-4 +++
>
> Api version – Selezionare latest version
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image96.png)

12. Nella scheda **Model data**, fare clic su **+ Add **in Data sources,
    quindi aggiungere i dettagli seguenti.

Index name - +++copilot-index+++

Content data – +++ content+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image97.png)

13. Fare clic su **Save**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image98.png)

**Attività 3: Mettere alla prova il tuo Copilot**

1.  Fare clic su **Test** per aprire il riquadro Test your Copilot.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image99.png)

2.  Digitare +++What is Azure OpenAI?+++ e fare clic su **Send**.

![A screenshot of a phone AI-generated content may be
incorrect.](./media/image100.png)

3.  Si riceverà la risposta dai dati caricati nella **risorsa Azure
    OpenAI**. Si noti anche che il messaggio **Surfaced with Azure
    OpenAI** sotto la risposta.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image101.png)

**Attività 4: Eliminare le risorse**

1.  Per eliminare l'account di archiviazione, passare alla home page del
    portale di Azure, digitare **Resource groups** nella barra di
    ricerca del portale di Azure, spostarsi e fare clic su **Resource
    groups** in **Services**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image102.png)

2.  Fare clic sul gruppo di risorse assegnato.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image103.png)

3.  Selezionare attentamente tutte le risorse che hai creato.

![A screenshot of a group AI-generated content may be
incorrect.](./media/image104.png)

4.  Nella pagina Gruppo di risorse passare alla barra dei comandi e fare
    clic su **Delete**.

**Nota importante**: non fare clic su **Delete resource group**. Se non
vedi l' opzione **Delete **nella barra dei comandi, fare clic sui
puntini di sospensione orizzontali.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image105.png)

5.  Nel riquadro** Delete Resources** che appare sul lato destro,
    inserire **delete** e fare clic sul pulsante **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image106.png)

6.  Nella finestra di dialogo** Delete confirmation**, fare clic sul
    pulsante D**elete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image107.png)

7.  Fare clic sull'icona a forma di campana, vedrai la notifica -
    **Executed delete command on 4 selected items. **

**Sommario**

Sono stati creati un account di archiviazione, un contenitore e un
servizio cognitivo di Azure nel portale di Azure, quindi è stato
distribuito il modello gpt-3-turbo in Azure AI Studio. Hai aggiunto dati
in Chat Playground e testato la configurazione dell'assistente inviando
query in una sessione di chat. Quindi, hai avviato una nuova app e hai
iniziato la conversazione con il chatbot. Sono stati eliminati il
modello gpt-3-turbo, l'account di archiviazione di Azure, il servizio di
ricerca cognitiva e la nuova app Web per gestire in modo efficace ed
efficiente le risorse di Azure OpenAI.
