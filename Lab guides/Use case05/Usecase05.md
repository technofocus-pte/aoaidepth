**Caso d'uso 05 - Distribuzione e test di una Conversational AI Solution
con Azure RAG Accelerator**

**Introduzione**

L' acceleratore di soluzioni *Chat with your data* è uno strumento
potente che combina le funzionalità di Azure AI Search and Large
Language Models (LLMs) per creare un'esperienza di ricerca
conversazionale. Questo acceleratore di soluzioni usa un modello GPT di
Azure OpenAI e un indice di Azure AI Search generato dai dati, integrato
in un'applicazione Web per fornire un'interfaccia in linguaggio
naturale, inclusa la funzionalità di riconoscimento vocale, per le query
di ricerca. Gli utenti possono trascinare e rilasciare i file, puntare
all'archiviazione e occuparsi della configurazione tecnica per
trasformare i documenti. È disponibile un'app Web che gli utenti possono
creare nel proprio abbonamento con sicurezza e autenticazione.

I dati di esempio illustrano come questo acceleratore potrebbe essere
utilizzato nel settore dei servizi finanziari (FSI).

In questo scenario, un consulente finanziario si sta preparando per un
incontro con un potenziale cliente che ha espresso interesse per
Emerging Markets Funds di Woodgrove Investments. Il consulente si
prepara per l'incontro aggiornando la propria comprensione degli
obiettivi generali del fondo dei mercati emergenti e dei rischi
associati.

Ora che il consulente finanziario è più informato sui Emerging Markets
Funds di Woodgrove, è meglio attrezzato per rispondere alle domande su
questo fondo da parte dei suoi clienti.

Nota: alcuni dei dati di esempio inclusi in questo acceleratore sono
stati generati utilizzando l'intelligenza artificiale e sono solo a
scopo illustrativo.

In questo caso d'uso, si distribuirà e si testerà Conversational AI
Solution usando l'acceleratore Azure RAG (Retrieval-Augmented
Generation). Questa soluzione sfrutta le potenti funzionalità di
intelligenza artificiale di Azure, tra cui Azure OpenAI e Azure AI
Search, per creare un'esperienza di ricerca conversazionale avanzata.
Entro la fine di questo laboratorio, disporrai di un'applicazione Web
completamente funzionale che utilizza l'elaborazione del linguaggio
naturale per interagire e interrogare i tuoi dati. I passaggi pratici ti
guideranno attraverso l'implementazione dell'infrastruttura necessaria,
la verifica delle risorse, il test della soluzione e la pulizia
dell'ambiente.

![Schermata di un diagramma del computer I contenuti generati
dall'intelligenza artificiale potrebbero non essere
corretti.](./media/image1.png)

**Obiettivi**

- Per distribuire l'infrastruttura necessaria da un modello
  personalizzato nel portale di Azure.

- Per verificare che tutte le risorse di Azure necessarie siano state
  distribuite correttamente.

- Per testare la funzionalità della soluzione distribuita caricando ed
  elaborando documenti e interagendo con l'applicazione Web.

- Per eliminare le risorse e i modelli distribuiti.

**Attività 1: Distribuire l'infrastruttura dal modello**

1.  Aprire il browser, andare alla barra degli indirizzi e digitare o
    incollare il seguente
    UR:+++[www.portal.azure.com/+++then](http://www.portal.azure.com/+++then)
    premere il pulsante **Enter**.

2.  Nella finestra di **Microsoft Azure**, inserire le tue credenziali
    di **Sign-in** e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image2.png)

3.  Quindi, inserire la password e fare clic sul pulsante **Sign
    in\*\*.\*\***

> ![Uno screenshot di una casella di accesso I contenuti generati
> dall'intelligenza artificiale potrebbero non essere
> corretti.](./media/image3.png)

4.  Nella finestra **Stay signed in?**, fare clic sul pulsante **Yes**.

> ![Uno screenshot dello schermo di un computer I contenuti generati
> dall'intelligenza artificiale potrebbero non essere
> corretti.](./media/image4.png)

5.  Aprire un nuovo browser e immettere l'URL seguente nella barra degli
    indirizzi:
    +++<https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json+++>
    per aprire il portale di Azure.

6.  Nella finestra **Custom deployment**, nella scheda **Basics**,
    immettere i dettagli seguenti per distribuire il modello
    personalizzato e quindi fare clic su ** Review + create.**

[TABLE]

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image5.png)

7.  Nella scheda **Review + create**, una volta superata la convalida,
    fare clic sul pulsante **Create**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image6.png)

8.  Attendere il completamento della distribuzione. L'implementazione
    richiederà circa 17-19 minuti.

9.  Fare clic sul pulsante **Go to Subscription**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image7.png)

**Attività 2: Verificare le risorse distribuite nel portale di Azure**

1.  Nella home page, fare clic su ** Resource Groups**.

> ![Uno screenshot dello schermo di un computer I contenuti generati
> dall'intelligenza artificiale potrebbero non essere
> corretti.](./media/image8.png)

2.  Fare clic sul nome del gruppo di risorse **rg-RAGSolutionXX**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image9.png)

3.  Assicurarsi che la risorsa seguente sia stata distribuita
    correttamente nell'area Stati Uniti orientali

- Azure App Service 

&nbsp;

- Azure Application Insights 

&nbsp;

- Azure Bot 

&nbsp;

- Azure OpenAI 

&nbsp;

- Azure Document Intelligence 

&nbsp;

- Azure Function App 

&nbsp;

- Azure Search Service 

&nbsp;

- Azure Storage Account 

&nbsp;

- Azure Speech Service 

&nbsp;

- Azure Database for PostgreSQL - Flexible Server 

&nbsp;

- Key vault 

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image10.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png) ![Uno screenshot di un computer I
contenuti generati dall'intelligenza artificiale potrebbero non essere
corretti.](./media/image12.png)

**Attività 3: Test della distribuzione**

1.  Nel gruppo di risorse e fare clic sulla nome della risorsa **Web-**
    {RESOURCE_TOKEN} - **admin-docker**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image13.png)

2.  Passare al sito di amministrazione
    [https://web-{RESOURCE_TOKEN}-admin.azurewebsites.net/]()

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image14.png)
>
> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image15.png)

3.  Nella pagina ** Chat with your data Solution Accelerator,** dal menu
    di spostamento a sinistra selezionare **Ingest Data.**

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image16.png)

4.  Nel riquadro **Add documents Batch**, fare clic su **Browse file** e
    passare a **C:\Labfiles \data** location e selezionare **tutti i
    file,** quindi fare clic sul pulsante **Open**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image17.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image18.png)

5.  Per caricare i file ci vorranno 1-2 minuti

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image19.png)

6.  Fare clic su **Reprocess all documents in the Azure Storage
    account.**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image20.png)

![Uno screenshot di una chat I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image21.png)

7.  Nella pagina **Chat with your data Solution Accelerator**, dal menu
    di spostamento a sinistra selezionare **Configuration **e
    selezionare la casella di controllo - **Enable post-answering
    prompt.**

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image22.png)

8.  Nel riquadro di configurazione , fare clic su **Save
    configuration.**

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image23.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image24.png)

9.  Tornare alla pagina del gruppo di risorse e fare clic sul nome del
    **Storage account**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image25.png)

10. Dal menu di navigazione a sinistra, fare clic su **Containers.**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image26.png)

11. Nella pagina **Containers**, selezionare **documents**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image27.png)

12. Assicurarsi che tutti i file vengano distribuiti correttamente

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image28.png)

13. Tornare alla pagina del gruppo di risorse

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image29.png)

14. Nella pagina del gruppo di risorse, selezionare Servizio app come
    **web-{RESOURCE_TOKEN}-docker**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image30.png)

15. Dal menu comprimibile a sinistra in **Settings**, selezionare
    **Authentication ** ![Uno screenshot di un computer I contenuti
    generati dall'intelligenza artificiale potrebbero non essere
    corretti.](./media/image31.png)

16. Fare clic su **Add identify provider** ![Uno screenshot di un
    computer I contenuti generati dall'intelligenza artificiale
    potrebbero non essere corretti.](./media/image32.png)

17. Selezionare Microsoft come provider di identità, aggiornare il nome
    come web-XXXXX-docker-new. Selezionare durata Client secret
    expiration su 90 giorni, quindi fare clic su **Next:
    Permissions**.![Uno screenshot di un computer I contenuti generati
    dall'intelligenza artificiale potrebbero non essere
    corretti.](./media/image33.png)

18. Fare clic su **Add permission**. Scorrere verso il basso nell'elenco
    per espandere **Application** e selezionare
    **Application.ReadWrite.All**. Quindi fare clic su **Update
    permission**.

> ![Uno screenshot dello schermo di un computer I contenuti generati
> dall'intelligenza artificiale potrebbero non essere
> corretti.](./media/image34.png)

19. Fare clic su **Add**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image35.png)

20. Fare clic sulla pagina **Overview** dell'app. Attendere il
    caricamento della pagina e poi cliccare su **Restart**. Confermare
    il riavvio cliccando su **Yes** ![Uno screenshot di un computer I
    contenuti generati dall'intelligenza artificiale potrebbero non
    essere corretti.](./media/image36.png) ![Uno screenshot di un
    computer I contenuti generati dall'intelligenza artificiale
    potrebbero non essere corretti.](./media/image37.png)

21. Nella pagina **Overview** di Web App, andare alla barra dei comandi
    e fare clic su **Browse**, ti porterà all'applicazione web.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image38.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image39.png)

22. Nella pagina di  **Azure AI** web app, immettere il testo seguente e
    fare clic sull'icona **Submit** come illustrato nell'immagine
    seguente.

+++Describe in more detail the risks from market volatility+++

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image40.png) 

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image41.png)

17. Nella sezione ** Chat session**, selezionare il collegamento dei
    riferimenti e osservare i dettagli del documento di ricerca sul lato
    destro della pagina.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image42.png)

18. Nella pagina dell'app Web di **Azure AI** immettere il testo
    seguente e fare clic sull'icona **Submit** come illustrato
    nell'immagine seguente.

+++How does Woodgrove Financial handle payroll taxes for employees
outside the U.S.?+++

![Uno screenshot di una chat I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image43.png) ![Uno
screenshot di una chat I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image44.png)

19. Nella pagina dell'app Web di **Azure AI** immettere il testo
    seguente e fare clic sull'icona **Submit** come illustrato
    nell'immagine seguente.

+++What is FORM 10-K and explain?+++

![Uno screenshot di una chat I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image45.png)

**Attività 4: Eliminare la risorsa Azure OpenAI**

1.  Per Azure OpenAI resource, digitare **Resource groups** nella barra
    di ricerca del portale Azure, navigare e fare clic su **Resource
    groups** in **Services**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image46.png)

2.  Fare clic sul gruppo di risorse.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image9.png)

3.  In una pagina di **overview** del gruppo di risorse, selezionare
     **Delete resource group**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image47.png)

4.  Nel riquadro **Delete Resources** visualizzato sul lato destro,
    immettere **il nome del gruppo di risorse** e fare clic sul pulsante
    **Delete**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image48.png)

5.  Nella finestra di dialogo di **Delete confirmation**, fare clic sul
    pulsante **Delete**.

![Uno screenshot di un errore del computer I contenuti generati
dall'intelligenza artificiale potrebbero non essere
corretti.](./media/image49.png)

**Sommario**:

Questo lab offre esperienza pratica nella distribuzione di una
Conversational AI Solution usando Azure RAG Accelerator. Il lab è stato
avviato distribuendo l'infrastruttura necessaria usando un modello
personalizzato. Dopo aver verificato la corretta distribuzione di varie
risorse di Azure, è stata testata la soluzione caricando documenti e
usando l'applicazione Web per eseguire query e recuperare informazioni.
Infine, è stato eliminato il gruppo di risorse per gestire le risorse in
modo efficiente. Questo laboratorio ha dimostrato come migliorare
l'interazione e il recupero dei dati utilizzando tecnologie di
intelligenza artificiale avanzate.
