**Lab 07: Implementazione di domande e risposte utilizzando la risposta
semantica**

**Introduzione**

Una semplice applicazione web per una ricerca di documenti abilitata a
OpenAI. Questo repository usa il servizio Azure OpenAI per la creazione
di vettori di incorporamento dai documenti. Per rispondere alla domanda
di un utente, recupera il documento più pertinente e quindi utilizza
GPT-3 per estrarre la risposta corrispondente alla domanda.

![Architettura](./media/image1.png)

**Obiettivi**

- Per distribuire modelli di chat e incorporamento in Azure AI Studio.

- Per usare un modello personalizzato per la distribuzione delle risorse
  necessarie, ad esempio il servizio app, il servizio di ricerca, il
  riconoscimento modulo e così via.

- Per distribuire l'app Web aoaichatsearch-site ed eseguire la ricerca
  di documenti, il riepilogo del testo e l'estrazione dei dati di
  conversazione abilitati per Azure OpenAI.

- Per eliminare le risorse e i modelli distribuiti.

## **Attività 1: Creare una risorsa Azure OpenAI**

1.  Nella home page del portale di Azure fare clic sul **menu del
    portale di Azure** rappresentato da tre barre orizzontali sul lato
    sinistro della barra dei comandi di Microsoft Azure, come illustrato
    nell'immagine seguente.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image2.png)

2.  Navigare e fare clic su **+ Create a resource**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image3.png)

3.  Nella pagina **Create a resource**, nella barra di ricerca **Search
    services and marketplace,** digitare **Azure OpenAI**, quindi
    premere il pulsante **Enter**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image4.png)

4.  Nella pagina **Marketplace,** passare alla sezione **Azure OpenAI**,
    fare clic sull'elenco a discesa del pulsante **Create**, quindi
    selezionare **Azure OpenAI** come illustrato nell'immagine. (Nel
    caso in cui tu abbia già cliccato sul pulsante **Azure OpenAI**,
    quindi fare clic sul pulsante **Create** nella pagina **Azure
    OpenAI**).

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

5.  Nella finestra **Create Azure OpenAI**, nella scheda **Basics**,
    immettere i dettagli seguenti e fare clic sul pulsante **Next**.

[TABLE]

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image6.png)

6.  Nella scheda **Network**, lasciare tutti i pulsanti di opzione nello
    stato predefinito e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image7.png)

7.  Nella scheda **Tag**, lasciare tutti i campi nello stato predefinito
    e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image8.png)

8.  Nella scheda **Review+submit**, una volta superata la convalida,
    fare clic sul pulsante **Create**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image9.png)

9.  Attendere il completamento della distribuzione. L'implementazione
    richiederà circa **2-3** minuti.

10. Nella finestra **Microsoft.CognitiveServicesOpenAI**, al termine
    della distribuzione, fare clic sul pulsante **Go to resource**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image10.png)

11. Nella finestra **Azure-open-testXX | Model deployments**, passare
    alla sezione **Resource Management** e fare clic su **Keys and
    Endpoints**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

12. Nella pagina **Keys and Endpoints,** copiare i valori **KEY1, KEY
    2** ed **Endpoint** e incollarli in un blocco note come illustrato
    nell'immagine seguente, quindi **salvare** il blocco note per usare
    le informazioni nel lab successivo.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image12.png)

## **Attività 2: Distribuire il modello Chat e il modello di incorporamento**

1.  Nella pagina **Azure-openai-testXX** fare clic su **Overview** nel
    menu di spostamento a sinistra, scorrere verso il basso e fare clic
    sul pulsante **Explore Azure AI Foundry portal** come illustrato
    nell'immagine seguente.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)

2.  Attendere l'avvio di Azure OpenAI Studio.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image14.png)

3.  Nella Homepage di **Azure AI Foundry** |**Azure OpenAI Studio,**
    selezionare **Deployment** dal menu di spostamento a sinistra**.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image15.png)

4.  Nella finestra **Deployments,** visualizzare **+Deploy model** e
    selezionare **Deploy base model.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image16.png)

5.  Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **gpt-4**, quindi fare clic sul pulsante **Confirm**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

6.  Selezionare **Model version** come **0125-Preview,** nel campo
    **Deployment type** come **Standard, Deployment name field**,
    immettere **gpt-4** e fare clic sul pulsante **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image18.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image19.png)

7.  Nella finestra **Deployments,** visualizzare **+Deploy model** e
    selezionare **Deploy base model.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image20.png)

8.  Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **text-embedding-ada-002,** quindi fare clic sul
    pulsante **Confirm**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

9.  Nella finestra di dialogo **Deploy model**, in **Deployment name,**
    immettere +++**text-embedding-ada-002+++,** selezionare **Standard**
    come **Deployment type** e fare clic sul pulsante **Deploy.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image23.png)

## **Attività 3: Distribuire in Azure (WebApp + Batch Processing) con Azure Cognitive Search**

1.  Aprire il browser edge, andare alla barra degli indirizzi e digitare
    o incollare il seguente URL:
    <https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fruoccofabrizio%2Fazure-open-ai-embeddings-qna%2Fmain%2Finfrastructure%2Fdeployment_ACS.json>
    quindi premere il pulsante **Enter**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

2.  Nella finestra **Custom deployment**, nella scheda **Basics**,
    immettere i dettagli seguenti per distribuire il modello
    personalizzato e quindi fare clic su **Review + create.**

[TABLE]

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

3.  Nella scheda **Review + create**, una volta superata la convalida,
    fare clic sul pulsante **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

4.  Attendere il completamento della distribuzione. L'implementazione
    richiederà circa 15-17 minuti.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image28.png)

5.  Fare clic sul pulsante **Go to resource group**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image29.png)

## **Attività 4: Ricerca di documenti abilitata per Azure OpenAI tramite l'applicazione Web**

1.  Nella finestra del gruppo di risorse **aoaiXXX-RG**, nella scheda
    **Resources**, passare al **App Service - aoaaichatsearch-site** e
    fare clic su di esso.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

2.  Nella pagina di **Overview** dell'app Web **aoaichatsearch-site**,
    andare alla barra dei comandi e fare clic su **Browse**, ti porterà
    all'applicazione web.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

3.  Attendere il completamento della distribuzione dell'applicazione
    Web. L'implementazione richiederà circa **10-15** minuti.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image32.png)

4.  Nella home page dell'applicazione Web, per verificare lo stato delle
    distribuzioni, fare clic sul pulsante **Check deployments** in
    Microsoft.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image33.png)

5.  Per verificare lo stato della distribuzione, potrebbero essere
    necessari circa 5-6 minuti.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image34.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

6.  Nella home page dell'app Web, navigare e fare clic su **Add
    Document** sul lato sinistro per aggiungere i dati.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

7.  Nel riquadro **Add Document**, fare clic sul pulsante **Browse
    files** per caricare i documenti che devono essere aggiunti alla
    knowledge base.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

8.  Passare al percorso **C:\Labfiles\Contoso Electronics** nella
    macchina virtuale e selezionare **Benefit_Options.pdf,** quindi fare
    clic sul pulsante **Open**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

9.  Fare di nuovo clic su **Browse files,** passare al percorso
    **C:\Labfiles\Contoso Electronics** nella macchina virtuale e
    selezionare **employee_handbook.pdf**, quindi fare clic sul pulsante
    **Open**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

10. Allo stesso modo, aggiungere
    **Northwind_Health_Plus_Benefits_Details.pdf** e
    **Northwind_Standard_Benefits_Details.pdf**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

11. I dati caricati verranno aggiunti alla knowledge base e l'operazione
    richiederà circa 5-7 minuti.

12. Fare clic su **Document Management** per verificare se i file sono
    stati caricati correttamente o meno.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image43.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image44.png)

13. Fare clic su **Index Management** per verificare i file, le chiavi e
    l'origine.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

14. Quindi, fare clic su **Chat.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

15. Nella sezione **Chat session**, inserire il seguente prompt, quindi
    premere il pulsante **Enter** e visualizzare la risposta.

**You**: **what is the employee's portion of the healthcare cost from
each paycheck in Contoso Electronics** 

![A close-up of a computer screen AI-generated content may be
incorrect.](./media/image47.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

16. Nella sezione **Chat session**, fare clic sul pulsante **Clear
    chat**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

17. Nella sezione **Chat session**, inserire il seguente prompt, quindi
    premere il pulsante **Enter** e visualizzare la risposta.

**You**: **How do I file a complaint or appeal with Northwind Health
Plus?**

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image50.png)

18. Nella sezione **Chat session**, fare clic sul pulsante **Clear
    chat**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image51.png)

19. Nella sezione **Chat session**, inserire il seguente prompt. quindi
    premere il pulsante **Enter** e visualizzare la risposta.

**You**: **Does my plan covers my eye exams?**

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image52.png)

20. Fare clic su **Utils-Document Summary** sul lato sinistro.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image53.png)

21. Nella sezione **Summarization**, selezionare il pulsante di opzione
    **Basic Summary.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image54.png)

22. Nella finestra **Summarization**, nella sezione **Enter some text to
    summarize**, nella finestra del messaggio, sostituire il testo
    corrente con il seguente, quindi fare clic sul pulsante
    **Summarize**.

It’s been six months since we reinvented search with [*the new
AI-powered Bing and
Edge*](https://blogs.microsoft.com/blog/2023/02/07/reinventing-search-with-a-new-ai-powered-microsoft-bing-and-edge-your-copilot-for-the-web/).
In that short time, you’ve engaged in so many unique and creative ways;
to date we’ve seen over 1 billion chats and over 750 million images fill
the world of Bing! We’ve also seen nine consecutive quarters of growth
on Edge, meaning we’re more able than ever to bring our best-in-class AI
experiences to users across the web. 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image55.png)

23. Controllare il riepilogo del testo che hai inserito.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

24. Dopo aver esaminato il risultato del riepilogo, fare clic sul
    pulsante **Clear summary**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

25. Ora scorrere verso l'alto e selezionare il pulsante di opzione
    **Bullet Points**. Nellla sezione **Enter some text to summarize**,
    nella casella del messaggio, sostituire il testo corrente con il
    seguente e quindi fare clic sul pulsante **Summarize**.

Microsoft has made its Azure OpenAI Service generally available,
bringing the enterprise generative AI tools out of its invite-only
program. Now any customers who meet Microsoft’s standards can access the
professional versions of OpenAI’s large language model GPT-3.5 and the
related text-to-image tool DALL-E 2, computer programming assistant
Codex, and the popular ChatGPT chatbot interface for the LLM. 

Microsoft launched the Azure OpenAI Service with an eye toward offering
businesses a way to develop apps without coding, write reports, and put
together marketing content. The scope has grown since then to encompass
new facets of the OpenAI’s models, including chat and visuals. Those
interested in the tools have to explain how they will use the AI tools
and agree to Microsoft’s ethical guidelines in their application for
access. The decision to widen the Azure OpenAI Service’s availability
arrives in tandem with Microsoft’s plans to integrate ChatGPT and DALL-E
into its Office suite, Bing search engine, and other consumer products.
Azure OpenAI Service followed earlier experiments to integrate GPT-3
into Microsoft projects like the low-code Power Apps programming tool
and the GitHub Copilot programming assistant. 

 

![A close up of a text AI-generated content may be
incorrect.](./media/image58.png)

26. Vedrai i risultati di riepilogo sotto forma di punti elenco.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image59.png)

27. Fare clic su **Utils-Conversation Data Extraction** sul lato
    sinistro.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image60.png)

28. Nel riquadro **Conversation data extraction**, fare clic su
    **Execute tasks** e visualizzare la risposta in **OpenAI result**.

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image61.png)

29. Esaminare i dati estratti dalla conversazione tra l'agente e
    l'utente.

![A screenshot of a message AI-generated content may be
incorrect.](./media/image62.png)

## Attività 5: Eliminazione delle risorse e dei modelli distribuiti

1.  Per eliminare le risorse distribuite, passare alla pagina **Azure
    portal home**, fare clic su **Resource groups**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image63.png)

2.  Nella pagina **Resource groups**, selezionare il gruppo di risorse.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image64.png)

3.  Nella home page di **Resource group** selezionare tutte le risorse e
    fare clic su **Delete.**

4.  Nel riquadro **Delete Resources,** visualizzato sul lato destro,
    andare su **Enter “delete” to confirm deletion**, quindi fare clic
    sul pulsante **Delete**.

5.  Nella finestra di dialogo **Delete confirmation**, fare clic sul
    pulsante **Delete**.

> ![Uno screenshot di un errore del computer Descrizione generata
> automaticamente](./media/image65.png)

6.  Cliccare sull'icona della campana, vedrai la notifica

**Sommario**

Il modello di chat gpt-4 e il modello di incorporamento
text-embedding-ada-002 sono stati distribuiti in Azure AI Studio, quindi
sono state distribuite le risorse necessarie usando un modello
personalizzato. Hai caricato documenti non strutturati nell'app Web
aoaichatsearch-site e hai estratto le informazioni precise in una
sessione di chat. Hai generato un riepilogo di base e punti elenco da
testi di esempio, quindi hai estratto i dati da una conversazione. Al
termine del lab sono state eliminate le risorse e i modelli per gestire
in modo efficiente le risorse di Azure OpenAI.

**Nota importante: Non eliminare il gruppo di risorse. Se eliminato, non
sarà possibile procedere con il lab successivo o creare un nuovo gruppo
di risorse.**

**Non eliminare il Azure OpenAI Service (Azure-openai-testXX). Lo stesso
servizio sarà utilizzato in tutti i laboratori.**
