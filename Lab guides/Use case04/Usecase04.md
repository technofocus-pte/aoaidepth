# Caso d'uso 04 - Creazione di un'app di chat (con .NET) con Azure OpenAI Service e RAG

Questo esempio illustra alcuni approcci per la creazione di esperienze
simili a ChatGPT sui propri dati utilizzando il modello Retrieval
Augmented Generation. Usa Azure OpenAI Service per accedere al modello
ChatGPT (gpt-4o-mini) e Azure AI Search per l'indicizzazione e il
recupero dei dati.

Il repository include dati di esempio in modo che sia pronto per essere
provato end-to-end. In questa applicazione di esempio viene utilizzata
una società fittizia denominata Contoso Electronics e l'esperienza
consente ai dipendenti di porre domande sui benefit, sui criteri
interni, nonché sulle descrizioni delle mansioni e sui ruoli.

![Un diagramma di un processo informatico Descrizione generata
automaticamente](./media/image1.png)

- Interfacce Voice Chat, Chat e Q&A

- Esplora varie opzioni per aiutare gli utenti a valutare l'affidabilità
  delle risposte con citazioni, tracciamento del contenuto della fonte,
  ecc.

- Mostra i possibili approcci per la preparazione dei dati, la
  costruzione di prompt e l'orchestrazione dell'interazione tra il
  modello (ChatGPT) e il recupero dati (Azure AI Search)

- Impostazioni direttamente nell'esperienza utente per modificare il
  comportamento e sperimentare le opzioni

**Tecnologie chiave usate**: Azure OpenAI Service, modello ChatGPT
(gpt-4o-mini) e Azure AI Search

**Durata stimata:** 40 minuti

# Esercizio 1 : Distribuire l'applicazione e testarla dal browser

## Attività 1: Ambiente di sviluppo aperto

1.  Aprire il browser, andare alla barra degli indirizzi, digitare o
    incollare il seguente URL:
    +++https://github.com/technofocus-pte/azure-search-openai-demo-csharp.git+++
    e accedere con il tuo account Github.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image2.png)

2.  Fare clic su **Fork**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image3.png)

3.  Inserire il nome del repository e quindi fare clic su **Create
    fork**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image4.png)

4.  Cliccare su **Code -\> Codespaces -\> +**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

5.  Attendere la configurazione dell'ambiente. Ci vogliono 5-10 minuti.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image6.png)

## Attività 2: Effettuare il provisioning dei servizi necessari per creare e distribuire l'app di chat in Azure

1.  Eseguire il seguente comando sul Terminale. Copiare il codice e
    premere **Enter**.

> +++azd auth login+++
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image7.png)

2.  Si apre il browser predefinito per inserire un codice. Inserire il
    codice copiato e fare clic su **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image8.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  Accedere con le credenziali di Azure.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image10.png)

![Uno screenshot di un errore del computer Descrizione generata
automaticamente](./media/image11.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image12.png)

4.  Tornare alla scheda **Github Codespace**. Eseguire il comando
    seguente per inizializzare l'ambiente del progetto nella directory
    corrente. Inserire il nome dell'ambiente come +++**chatragXXX+++** e
    premere **Enter**.

> Nota : il nome dell'ambiente deve essere univoco

+++azd env new+++ 

![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image13.png)

5.  Eseguire il comando seguente per effettuare il provisioning dei
    servizi in Azure, compilare il contenitore.

> +++azd env set AZURE_RESOURCE_GROUP ResourceGroup1+++ 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image14.png)

6.  Eseguire azd up: verrà effettuato il provisioning delle risorse di
    Azure e verrà distribuito l'esempio in tali risorse, inclusa la
    compilazione dell'indice di ricerca in base ai file trovati nella
    cartella ./data.

> **+++azd up+++**
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

7.  Selezionare i valori seguenti.

- **Select an Azure Subscription to use**: selezionare la sottoscrizione

- **Select an Azure location to use : East us2/west us2** (a volte, East
  US potrebbe non essere disponibile, scegliere la località dall'elenco
  indicato di seguito).

- Selezionare il gruppo di risorse esistente: il tuo gruppo di risorse
  esistente (ad esempio: **ResourceGroup1 )**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image16.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

7.  Attendere il completamento del provisioning della risorsa. Questo
    processo richiederà 5-10 minuti per creare tutte le risorse
    necessarie.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image18.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image19.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image20.png)

8.  Dopo che l'applicazione è stata distribuita correttamente, viene
    visualizzato un URL nel terminale. Copiare l' **URL**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image21.png)

9.  Fare clic sul pulsante **Open**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image22.png)

10. Apre l'app in una nuova scheda.

> ![](./media/image23.png)

11. Aprire un browser, passare a <https://portal.azure.com> e accedere
    con l'account della sottoscrizione di Azure.

12. Nella home page fare clic su **Resource Groups**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image24.png)

13. Fare clic sul gruppo di risorse.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image25.png)

14. Assicurarsi che la risorsa seguente sia stata distribuita
    correttamente

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image26.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image27.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image28.png)

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image29.png)

15. Nel gruppo di risorse e fare clic sul nome della risorsa **Azure
    OpenAI**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image30.png)

16. Nella finestra **Azure OpenAI**, fare clic su **Overview** nel menu
    di navigazione a sinistra, quindi nella scheda **Get Started**, fare
    clic sul pulsante **Go to Azure OpenAI Studio** per aprire **Azure
    OpenAI Studio** in un nuovo browser.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image31.png)

17. Assicurati che **gpt-4o-mini**, **text-embedding-ada-002** sia
    distribuito correttamente.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image32.png)

18. Nel gruppo di risorse e fare clic sul nome risorsa **storage
    account**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image33.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image34.png)

19. Ora aprire l'URL in un browser

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image23.png)

20. Cliccare su **Chat**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image35.png)

21. Nella pagina dell'app Web **Blazor OpenAI**, inserire il seguente
    testo e fare clic sull'icona **Submit** come mostrato nell'immagine
    sottostante.

> **+++What is included in my Northwind Health Plus plan that is not in
> standard?+++** 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image36.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image37.png)

22. Nella pagina dell'app Web **Blazor OpenAI**, inserire il seguente
    testo e fare clic sull'icona **Submit** come mostrato nell'immagine
    sottostante.

> **+++Can I use out-of-network providers?+++**
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image38.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image39.png)

23. Nella pagina dell'app Web **Blazor OpenAI**, inserire il seguente
    testo e fare clic sull'icona **Submit** come mostrato nell'immagine
    sottostante.

> **+++Are there any exclusions or restrictions?+++**
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image40.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image41.png)

24. Nella pagina dell'app Web **Blazor OpenAI**, inserire il seguente
    testo e fare clic sull'icona **Submit** come mostrato nell'immagine
    sottostante.

> **+++What does a Product Manager do?+++** 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image42.png)

25. Fare clic su **Documents.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image43.png)

## **Compito 3 : Pulire tutte le risorse**

1.  Tornare al **Azure portal -\> Resource group-\> Resource group
    name.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image44.png)

2.  Selezionare tutte le risorse e poi cliccare su **Delete** come
    mostrato nell'immagine sottostante. (**NON ELIMINARE il** gruppo di
    risorse)

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image45.png)

3.  Digitare **delete** nella casella di testo e quindi fare clic su
    **Delete**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image46.png)

4.  Confermare l'eliminazione cliccando su **Delete**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image47.png)

5.  Tornare alla scheda del portale Github e aggiornare la pagina.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image48.png)

6.  Fare clic su **Code**, selezionare il ramo creato per questo lab e
    fare clic su **Delete**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image49.png)

7.  Confermare l'eliminazione del ramo facendo clic sul pulsante
    **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

**Sommario:**

Questo caso d'uso ti ha insegnato, distribuendo un'applicazione di chat
per il modello di Retrieval Augmented Generation in esecuzione su Azure,
utilizzando Azure AI Search per il recupero e Azure OpenAI e LangChain
modelli linguistici di grandi dimensioni (LLM) per potenziare le
esperienze in stile ChatGPT e Q&A
