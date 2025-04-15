# **Introduzione**

Azure OpenAI Assistant (anteprima) ti consente di creare assistenti di
intelligenza artificiale su misura per le tue esigenze tramite
istruzioni personalizzate e arricchiti da strumenti avanzati come
l'interprete di codice e funzioni personalizzate.

Questo lab è incentrato sulla configurazione e l'uso dei servizi Azure
OpenAI insieme all'integrazione di Bing Search per creare assistenti di
intelligenza artificiale sofisticati e framework multi-agente.
Distribuirai modelli di intelligenza artificiale, esplorerai le
funzionalità dell'assistente e implementerai interazioni multi-agente
per l'elaborazione di attività complesse.

**Obiettivo**

- Per creare una risorsa del Bing Search Service in Azure.

- Per distribuire le risorse di Azure OpenAI e configurarle.

- Per distribuire modelli specifici di Azure OpenAI, ad esempio GPT-4,
  GPT-4 Vision e DALL-E-3.

- Per esplorare e creare prototipi di assistenti di intelligenza
  artificiale usando Azure OpenAI Studio.

- Per implementare la chiamata di funzione con le API di ricerca Bing
  per migliorare le funzionalità dell'assistente.

- Per creare un framework multimodale e multi-agente usando l'API di
  Azure Assistant per attività di intelligenza artificiale
  collaborative.

- Per eliminare le risorse e i modelli distribuiti.

## **Attività 1: Creare una risorsa del Bing Search Service**

1.  Fare clic sul **Portal Menu**, quindi selezionare **+ Create a
    resource**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image1.png)

2.  Nella barra di ricerca della pagina **Create a resource**, digitare
    **Bing Search v7** e fare clic su **Bing Search v7** visualizzato.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image2.png)

3.  Fare clic sulla sezione **Bing Search v7**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

4.  Nella pagina **Create a search service**, fornire le seguenti
    informazioni e fare clic sul pulsante **Review+create**.

[TABLE]

![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image4.png)

![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image5.png)

5.  Una volta superata la convalida, fare clic sul pulsante **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

6.  Una volta completata la distribuzione, fare clic sul pulsante **Go
    to resource**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

7.  Nella finestra **bingsearchaoaiXX,** passare alla sezione **Resource
    management** e fare clic su **Keys and Endpoint**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image8.png)

8.  Nella pagina **Keys and Endpoints**, copiare **KEY1** (*è possibile
    utilizzare KEY1 o KEY2)* e **Endpoint** e incollarli in un blocco
    note (come mostrato nell'immagine), quindi **salvare** il blocco
    note per utilizzare le informazioni nelle attività future.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image9.png)

## **Attività 2: Creare una risorsa Azure OpenAI**

1.  Nella home page del portale di Azure, fare clic sul **menu del
    portale di Azure** rappresentato da tre barre orizzontali sul lato
    sinistro della barra dei comandi di Microsoft Azure, come illustrato
    nell'immagine seguente.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image10.png)

2.  Navigare e fare clic su **+ Create a resource. **

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image11.png)

3.  Nella pagina **Create a resource**, nella barra di ricerca dei
    **Search services and marketplace,** digitare **Azure OpenAI**,
    quindi premere il pulsante **Enter**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image12.png)

4.  Nella pagina **Marketplace,** passare alla sezione **Azure OpenAI**,
    fare clic sull'elenco a discesa del pulsante **Create**, quindi
    selezionare **Azure OpenAI** come illustrato nell'immagine. (Nel
    caso in cui tu abbia già cliccato sul pulsante **Azure OpenAI**,
    quindi fare clic sul pulsante **Create** nella pagina **Azure
    OpenAI**).

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image13.png)

[TABLE]

5.  Nella finestra **Create Azure OpenAI**, nella scheda **Basics**,
    immettere i dettagli seguenti e fare clic sul pulsante **Next**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)

6.  Nella scheda **Network**, lasciare tutti i pulsanti di opzione nello
    stato predefinito e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image15.png)

7.  Nella scheda **Tag**, lasciare tutti i campi nello stato predefinito
    e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image16.png)

8.  Nella scheda **Review+submit**, una volta superata la convalida,
    fare clic sul pulsante **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

9.  Attendere il completamento della distribuzione. L'implementazione
    richiederà circa **2-3** minuti.

10. Nella finestra **Microsoft.CognitiveServicesOpenAI**, al termine
    della distribuzione, fare clic sul pulsante **Go to resource**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image18.png)

11. Fare clic su **Keys and Endpoints** dal menu di spostamento a
    sinistra, quindi copiare il valore dell'endpoint in un blocco note
    in **AzureAI ENDPOINT** e la chiave in una variabile **AzureAIKey**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image19.png)

## Attività 3: Distribuzione di un modello Azure OpenAI

1.  Nella finestra **AzureOpenAI-AssistantsXX,** fare clic su
    **Overview** nel menu di spostamento a sinistra, fare clic sul
    pulsante **Explore Azure AI Foundry portal** per aprire **Azure AI
    Foundry Studio** in un nuovo browser

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image20.png)

2.  Nella finestra **Azure AI Foundary | Azure OpenAI Service,**
    selezionare **Deployment** dal menu di spostamento a sinistra**.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image21.png)

12. Nella finestra **Deployments,** visualizzare **+Deploy model** e
    selezionare **Deploy base model.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

13. Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **gpt-4**, quindi fare clic sul pulsante **Confirm**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)

3.  Nella finestra di dialogo **Deploy model**, inserire i seguenti
    dettagli e fare clic sul pulsante **Create**.

- Selezionare il modello: **gpt-4**

- Model Version**: 1106-Preview**

- Deployment Name: inserire **gpt-4**

- Selezionare **Advanced options** e selezionare il tipo **Standard**
  come **Deployment**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image26.png)

4.  Nella pagina **Deployments** fare clic su +**Create new
    deployment**.

5.  Nella finestra **Deployments,** visualizzare **+Deploy model** e
    selezionare **Deploy base model.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

14. Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **gpt-4**, quindi fare clic sul pulsante **Confirm**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image23.png)

6.  Nella finestra di dialogo  **Deploy model**, in **Select a model**
    fare clic sul campo a discesa selezionare **gpt-4**, in **Model
    version** selezionare **vision-preview** e in **Deployment name**
    immettere +++**gpt-4-vision+++.** Fare clic sul pulsante **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image27.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image28.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image29.png)

7.  Nella finestra **Deployments,** visualizzare **+Deploy model** e
    selezionare **Deploy base model.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

15. Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **dall-e-3**, quindi fare clic sul pulsante
    **Confirm**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image30.png)

8.  Nella finestra di dialogo **Deploy model**, in **Select a model**
    fare clic sul campo a discesa selezionare **dall-e-3**, in **Model
    version** selezionare **Auto-update to default** e in **Deployment
    name** immettere !!**Dall-e-3**!!**.** Fare clic sul pulsante
    **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image31.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image32.png)

## Attività 4: Esplorare il playground dell'assistente

1.  In Home page del **Azure AI Foundry |Azure OpenAI Service**, nella
    sezione **Playgrounds,** fare clic sul **Assistants playground**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image33.png)

2.  Nel pannello **Assistants playground**, selezionare **+Create an
    assistant**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

3.  Il playground degli assistenti ti consente di esplorare, prototipare
    e testare gli assistenti AI senza dover eseguire alcun codice. Da
    questa pagina è possibile iterare rapidamente e sperimentare nuove
    idee.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image35.png)

4.  Dal riquadro **Assistant setup** immettere i dettagli seguenti

- Assistant a name: +++**Math Assist+++**

- Instructions: Inserire le seguenti istruzioni +++**You are an AI
  assistant that can write code to help answer math questions+++**

- Deployment: **gpt-4**

- Selezionare l'interruttore che abilita **code interpreter** 

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image36.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image37.png)

5.  Dal riquadro **Assistant setup**, selezionare l'opzione **Select
    assistant **

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

6.  Nella scheda **Select an assistant**, selezionare **Math Assist** e
    fare clic sul pulsante **Select**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  Inserire una domanda a cui l'assistente deve rispondere: +++**I need
    to solve the equation 3x + 11 = 14. Can you help me?**+++

8.  Selezionare il pulsante R**un**.

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image40.png)

Anche se possiamo vedere che la risposta è corretta, per confermare che
il modello ha utilizzato l'interprete del codice per arrivare a questa
risposta e che il codice che ha scritto è valido piuttosto che ripetere
semplicemente una risposta dai dati di addestramento del modello,
porremo un'altra domanda.

9.  Inserire la domanda successiva: +++**Show me the code you ran to get
    this solution.+++**, Selezionare il pulsante ** Add and run**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

È inoltre possibile consultare i log nel pannello di destra per
confermare che è stato utilizzato l'interprete del codice e per
convalidare il codice eseguito per generare la risposta. È importante
ricordare che, sebbene l'interprete del codice fornisca al modello la
capacità di rispondere a domande matematiche più complesse convertendo
le domande in codice ed eseguendole in un ambiente Python sandbox, è
comunque necessario convalidare la risposta per confermare che il
modello abbia tradotto correttamente la domanda in una rappresentazione
valida nel codice.

## Attività 5: Chiamata della funzione degli assistenti con Bing Search

In questo notebook verrà illustrato come usare le API di Bing Search e
la chiamata di funzioni per mettere a terra i modelli Azure OpenAI sui
dati dal Web. Questo è un ottimo modo per fornire al modello l'accesso a
dati aggiornati dal Web.

Questo esempio sarà utile per gli sviluppatori e per i data scientist
che desiderano apprendere le funzionalità di chiamata delle funzioni e
la messa a terra basata sulla ricerca.

1.  Nella casella di ricerca di **Windows**, digitare **Visual Studio**,
    quindi fare clic su **Visual Studio Code**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image43.png)

2.  Nell'editor di **Visual Studio Code** , fare clic su **File**,
    quindi navigare e fare clic su **Open Folder**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image44.png)

3.  Navigare e selezionare la cartella **Assistants** da **C:\LabFiles**
    e fare clic sul pulsante **Select Folder**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

4.  Se viene visualizzata una finestra di dialogo: **Do you trust the
    authors of the files in this folder?**, quindi fare clic su **Yes, I
    trust the author**.

![Uno screenshot di un computer Descrizione generata automaticamente con
confidenza media](./media/image46.png)

5.  Nell'elenco a discesa di Visual Studio Code gli **ASSISTANTS**,
    sotto **function_calling** navigare e fare clic su
    **assistants_function_calling_with_bing_search.ipynb** notebook.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

6.  Nella pagina principale dell'editor di Visual Studio Code, scorrere
    verso il basso fino all'intestazione dei **install requirements** ed
    eseguire la prima cella. Se viene richiesto di selezionare
    l'ambiente, selezionare **Python Environments** come mostrato
    nell'immagine.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image49.png)

7.  Se viene richiesto di selezionare il percorso, selezionare il
    percorso **Python versione 3.12.2 (o versione successiva)** come
    mostrato nell'immagine.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

8.  Aggiornare i parametri, sostituire **Azure OpenAI Endpoint, Azure
    OpenAI Key (**i valori che hai salvato nel tuo blocco note
    nell'**attività 2), Bing search subscription key** con i valori che
    hai salvato nel tuo blocco note nell'**attività 1.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image51.png)

![Uno screenshot di un programma per computer Descrizione generata
automaticamente](./media/image52.png)

9.  Definire una funzione per chiamare le Bing Search APIs, selezionare
    la 3a e la 4a cella. Quindi, eseguire la cella facendo clic
    sull'icona **start**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image53.png)

![A screen shot of a computer AI-generated content may be
incorrect.](./media/image54.png)

10. Far funzionare le cose end-to-end, selezionare la 5a, 6a, 7a, 8a
    cella. Quindi, eseguire la cella facendo clic sull'icona **start**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image55.png)

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image56.png)

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image57.png)

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image58.png)

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image59.png)

## **Attività 6: Creazione di un framework multimodale multi-agente con Azure Assistant API**

Questo repository illustra il modello di creazione di un sistema
multi-agente usando l'API Azure OpenAI Assistant.

L'esempio fornito in questo notebook illustra come creare un framework
multi-agente con l'API di Azure Assistant e funge da guida completa per
gli sviluppatori che desiderano sfruttare le funzionalità di più agenti
di intelligenza artificiale che lavorano in concerto. Il punto cruciale
dell'articolo è mostrare come gli agenti possono comunicare e
collaborare per elaborare attività complesse, come la generazione e il
miglioramento delle immagini attraverso più iterazioni basate sull'input
dell'utente. Ciò è particolarmente rilevante per gli sviluppatori e gli
appassionati di tecnologia che sono interessati a esplorare le frontiere
dell'intelligenza artificiale generativa e dei sistemi multi-agente.

Prima di iniziare, è necessario avere una conoscenza di base
dell'intelligenza artificiale e un interesse per il modo in cui gli
agenti possono lavorare insieme per migliorare le funzionalità
dell'intelligenza artificiale. L'articolo non approfondisce la
programmazione; tuttavia, una conoscenza generale del funzionamento
delle API e del ruolo dell'IA nei sistemi automatizzati sarebbe utile
per comprendere i concetti presentati. Questo esempio è un invito agli
innovatori e agli sviluppatori che desiderano sperimentare sistemi di
intelligenza artificiale avanzati e potenzialmente integrarli in varie
soluzioni di settore.

1.  In Visual Studio Code, in **multi-agente**, navigare e fare clic sul
    file **.env**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image60.png)

2.  Nel file **.env** sostituire **Azure OpenAI Endpoint, Azure OpenAI
    Key (**i valori salvati nel blocco note nell'**attività 2), gpt4
    deployment name, DALLE3 deployment name and GPT 4 Vision deployment
    name** con i valori salvati nel blocco note nell'**attività 3**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image61.png)

3.  Fare clic su **File** e quindi su **Save**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image62.png)

4.  In Visual Studio Code, in **multi-agent**, passare e fare clic su
    **multi-agent.ipynb** notebook.

> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image63.png)

5.  Nella pagina principale dell'editor di Visual Studio Code, scorrere
    verso il basso fino all'intestazione dei **install requirements** ed
    eseguire la prima cella. Se viene richiesto di selezionare
    l'ambiente, selezionare **Python Environments** come mostrato
    nell'immagine.

6.  Se viene richiesto di selezionare il percorso, selezionare il
    percorso **Python versione 3.12.2 (o versione successiva)** come
    mostrato nell'immagine.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image64.png)

7.  Selezionare la 2a cella. Quindi, eseguire la cella facendo clic
    sull'icona **start**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image65.png)

![A screen shot of a computer program AI-generated content may be
incorrect.](./media/image66.png)

8.  Per generare immagini utilizzando un prompt per il modello Dalle-3.
    L'output è un file .jpg memorizzato nella directory locale degli
    utenti. Selezionare la 3a cella. Quindi, eseguire la cella facendo
    clic sull'icona **start**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image67.png)

9.  Inizializzare l'agente con la definizione descritta in precedenza.
    Selezionare la 4a cella. Quindi, eseguire la cella facendo clic
    sull' icona **start**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image68.png)

10. La funzione del generatore di immagini chiama il generatore di
    immagini Dalle-3 in base al prompt. Selezionare la 5a cella. Quindi,
    esegui la cella facendo clic sull'**icona di avvio**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image69.png)

11. L'agente Vision Assistant è responsabile dell'analisi delle
    immagini. L'output è un nuovo prompt che deve essere utilizzato
    dall'agente creatore di immagini. Selezionare la 6a cella. Quindi,
    eseguire la cella facendo clic sull'**icona di avvio**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image70.png)

12. Inizializzare l'agente con la definizione descritta in precedenza.
    Selezionare la 7a cella. Quindi, eseguire la cella facendo clic
    sull' **icona di avvio**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image71.png)

13. La funzione dell'assistente alla visione chiama l'analisi
    dell'immagine GPT4 Vision data un'immagine, eseguire la cella
    facendo clic sull'**icona di** **avvio**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image72.png)

14. Questo agente facilita la conversazione tra l'utente e altri agenti,
    garantendo il completamento con successo dell'attività, eseguire la
    cella facendo clic sull'**icona di avvio**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

15. Inizializzare l'agente con la definizione sopra descritta, eseguire
    la cella cliccando sull'**icona** di **avvio**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image74.png)

16. Questa funzione chiama l'API Assistant per generare un thread
    principale di comunicazione tra gli agenti elencati nella
    agents_threads, eseguire la cella facendo clic sull'**icona di
    avvio**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image75.png)

17. Questo agente facilita la conversazione tra l'utente e gli altri
    agenti, garantendo il completamento dell'attività. Eseguire la cella
    facendo clic sull' **icona di avvio**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image76.png)

![Uno screenshot di un programma per computer Descrizione generata
automaticamente](./media/image77.png)

18. Esempi di domande, inserire il +++Generate an image of a boat
    drifting in the water and analyze it and enhance the image+++.
    Eseguire la cella facendo clic sull' **icona di avvio**.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image78.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image79.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image80.png)

## Attività 7: Eliminare le risorse

1.  Per eliminare l'account di archiviazione, passare alla pagina home
    di **Azure portal**, fare clic su **Resource groups**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image81.png)

2.  Fare clic sul gruppo di risorse.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image82.png)

3.  Nella home page del **Resource group** selezionare le risorse e fare
    clic sul pulsante **Delete. **

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image83.png)

4.  Nel riquadro **Delete Resources,** visualizzato sul lato destro,
    andare a **Enter “Delete” to confirm deletion**, quindi fare clic
    sul pulsante **Delete**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image84.png)

5.  Nella finestra di dialogo **Delete confirmation**, fare clic sul
    pulsante **Delete**.

> ![Uno screenshot di un errore del computer Descrizione generata
> automaticamente](./media/image85.png)

6.  Fare clic sull'icona a forma di campana, vedrai la notifica –
    **Deleted resource group AOAI-RG89.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image86.png)

**Sommario**

Questo lab ha fornito un'esplorazione pratica delle funzionalità
avanzate di intelligenza artificiale usando Azure OpenAI e
l'integrazione di Bing Search. Per iniziare, configurare le risorse
essenziali di Azure e distribuire modelli di intelligenza artificiale,
ad esempio GPT-4 e DALL-E-3. Quindi, è stato usato Azure OpenAI Studio
per creare e testare assistenti di intelligenza artificiale in grado di
gestire attività complesse come la risoluzione di problemi matematici e
la generazione di immagini. È stata integrata la Bing Search per
recuperare dati in tempo reale per la messa a terra delle risposte
dell'intelligenza artificiale. Inoltre, hai imparato a creare un
framework multi-agente, che mostra come diversi agenti di intelligenza
artificiale possono collaborare per migliorare le prestazioni delle
attività. Alla fine, hai acquisito esperienza pratica
nell'implementazione, nel test e nell'ottimizzazione di soluzioni basate
sull'intelligenza artificiale che ti hanno preparato a sfruttare queste
tecnologie in varie applicazioni del mondo reale.
