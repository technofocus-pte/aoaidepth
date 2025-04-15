**Introduzione**

Questo esempio illustra alcuni approcci per la creazione di esperienze
simili a ChatGPT sui propri dati utilizzando il modello Retrieval
Augmented Generation. Usa il servizio Azure OpenAI per accedere al
modello ChatGPT (gpt-35-turbo) e Ricerca cognitiva di Azure per
l'indicizzazione e il recupero dei dati.

Il repository include dati di esempio in modo che sia pronto per essere
provato end-to-end. In questa applicazione di esempio viene utilizzata
una società fittizia denominata Contoso Electronics e l'esperienza
consente ai dipendenti di porre domande sui benefit, sui criteri
interni, nonché sulle descrizioni delle mansioni e sui ruoli.

Questo caso d'uso consente di sviluppare un'applicazione di chat
sofisticata usando il modello Retrieval Augmented Generation (RAG) sulla
piattaforma Azure. Sfruttando il servizio Azure OpenAI e Azure Cognitive
Search, creerai un'applicazione di chat in grado di rispondere in modo
intelligente alle domande usando i tuoi dati. Questo lab usa una società
fittizia, Contoso Electronics, come case study per dimostrare come
creare un'esperienza simile a ChatGPT sui dati aziendali, coprendo
aspetti quali i benefit per i dipendenti, i criteri interni e i ruoli
lavorativi.

![RAG Architettura](./media/image1.png)

**Obiettivo**

- Per installare Azure CLI e Node.js nel computer locale.

- Per assegnare un ruolo di owner all'utente.

- Per installare l'estensione Dev Containers e configurare l'ambiente di
  sviluppo.

- Per distribuire un'applicazione di chat in Azure e usarla per ottenere
  risposte dai file PDF.

- Per eliminare le risorse e i modelli distribuiti.

## Attività 1: Installare Azure Cli e impostare l'ambito dei criteri su Computer locale

1.  Nella barra di ricerca di Windows, digitare **PowerShell**. Nella
    finestra di dialogo di **PowerShell**, navigare e fare clic su **Run
    as administrator**. Se viene visualizzata la finestra di dialogo -
    **Do you want to allow this app to make changes to your device?**
    quindi fare clic sul pulsante **Yes**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image2.png)

2.  Eseguire il comando seguente per installare Azure Cli in PowerShell

PowerShell copy 

**winget install microsoft.azd**![Schermata di un computer Descrizione
generata automaticamente](./media/image3.png)

3.  Eseguire il comando seguente per impostare il criterio su
    **Unrestricted** e immettere **A** quando viene richiesto di
    modificare il criterio di esecuzione.

> **Set-ExecutionPolicy Unrestricted**
>
> ![Schermo di un computer con testo bianco Descrizione generata
> automaticamente](./media/image4.png)

## Attività 2: Installare Node.js

1.  Aprire il browser, andare alla barra degli indirizzi, digitare o
    incollare il seguente URL: +++https://nodejs.org/ it/download/+++,
    quindi premere il pulsante **Enter**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

2.  Selezionare e fare clic su **Windows Installer**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

3.  Il file **Node-V** verrà scaricato. Fare clic sul file scaricato per
    configurare **Node.js**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image7.png)

4.  Nella finestra **Welcome to the Node.js Setup Wizard**, fare clic
    sul pulsante **Next**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

5.  Nella finestra **End-User License Agreement**, selezionare **I
    accept the terms in the License agreement** e fare clic sul pulsante
    **Next**.

![Uno screenshot di una configurazione del software Descrizione generata
automaticamente](./media/image9.png)

6.  Nella finestra **Destination Folder**, fare clic sul pulsante
    **Next**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image10.png)

7.  Nella finestra **Custom Setup**, fare clic sul pulsante **Next**.

![](./media/image11.png)

![](./media/image12.png)

8.  Nella finestra **Ready to install Node.js**, fare clic su
    **Install.**

![Uno screenshot di un software Descrizione generata
automaticamente](./media/image13.png)

9.  Nella finestra **Completing the Node.js Setup Wizard window**, fare
    clic sul pulsante **Finish** per completare il processo di
    installazione.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image14.png)

## Attività 3: Recuperare il nome e la posizione del gruppo di risorse

1.  Aprire il browser, andare alla barra degli indirizzi e digitare o
    incollare il seguente URL: +++https://portal.azure.com/+++, quindi
    premere il pulsante **Enter**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image15.png)

2.  Nella finestra **Microsoft Azure,** usare le **User Credentials**
    per accedere ad Azure.

![](./media/image16.png)

3.  Quindi, inserire la password e fare clic sul pulsante **Sign in.**

> ![A screenshot of a login box AI-generated content may be
> incorrect.](./media/image17.png)

4.  Nella finestra **Stay signed in?**, fare clic sul pulsante **Yes**.

> ![Interfaccia utente grafica, applicazione Descrizione generata
> automaticamente](./media/image18.png)

5.  Digitare +++**Resource group+++** nella barra di ricerca e
    selezionare **Resource groups**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image19.png)

6.  Fare clic sul **Resource group** assegnato.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

7.  Nella pagina **Resource group,** copiare il **nome e la posizione
    del gruppo di risorse** e incollarli in un blocco note, quindi
    **salvare** il blocco note per usare le informazioni nelle attività
    future.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

## Attività 4: Creare il servizio AI Search

1.  Nel portale di Azure, digitare **+++AI search+++** nella barra di
    ricerca e selezionare **AI Search**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

2.  Fare clic su +**Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

3.  Selezionare i valori sottostanti e quindi fare clic su** Review +
    Create**.

&nbsp;

1)  Subscription: **la sottoscrizione di Azure**.

2)  Resource group: **selezionare il gruppo di risorse esistente**

3)  Service name - **aisearchXXXX(XXXXX può essere Lab instant ID)**

4)  Location: **Central US** /posizione vicino a te

5)  Pricing tier: Standard

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

4.  Cliccare su **Create**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

5.  Attendere la distribuzione e quindi fare clic su **Go to resource**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image26.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image27.png)

6.  Nella pagina **AI Search Overview**. Nel riquadro di spostamento a
    sinistra, nella sezione **Settings**, selezionare **Semantic
    ranker**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

7.  Nella scheda **Semantic ranker,** selezionare il riquadro
    **Standard** e fare clic su **Select plan.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image29.png)

8.  Selezionare **Yes**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image30.png)

9.  Verrà visualizzata una notifica - **Successfully updated semantic
    ranker to standard  plan**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image31.png)

10. Aprire un Blocco note e prendere nota del nome di AI Search, del
    nome del gruppo di risorse e della posizione. Lo utilizzeremo in
    seguito per comunicare al servizio

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image32.png)

## Attività 5: Eseguire il Docker

1.  Nella casella di ricerca di Windows, digitare Docker, quindi fare
    clic su **Docker Desktop**.

![](./media/image33.png)

2.  Eseguire il Docker Desktop.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

## **Attività 6: Installare l'estensione Dev Containers**

1.  Nella casella di ricerca di Windows, digitare **Visual Studio**,
    quindi fare clic su **Visual Studio Code**.

> ![](./media/image35.png)

2.  Aprire il browser, andare alla barra degli indirizzi, digitare o
    incollare il seguente URL:
    +++https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers+++,
    quindi premere il pulsante **Enter**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image36.png)

3.  Nella pagina **Dev Containers,** selezionare il pulsante
    **Install**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

4.  Per installare questa estensione viene visualizzata la finestra di
    dialogo Visual Studio Code, quindi fare clic sul pulsante
    **Continue**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

5.  Viene visualizzata la finestra di dialogo **This site is trying to
    open Visual Studio Code**, quindi fare clic sul pulsante **Open**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

6.  In Visual Studio, fare clic sul pulsante **Install** sotto il Dev
    container.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image41.png)

## Attività 7: Ambiente di sviluppo aperto

1.  Aprire il browser, andare alla barra degli indirizzi, digitare o
    incollare il seguente URL:

+++<https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo>+++,
quindi premere il pulsante **Enter**.

![Uno sfondo bianco con testo nero Descrizione generata
automaticamente](./media/image42.png)

2.  Viene visualizzata la finestra di dialogo **This site is trying to
    open Visual Studio Code**, quindi fare clic sul pulsante **Open**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image43.png)

3.  Viene visualizzata la finestra di dialogo **Allow ‘Dev Containers’
    extension to open this URI?,** quindi fare clic sul pulsante
    **Open**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image44.png)

4.  Viene visualizzata la finestra di dialogo **Cloning a repository in
    a Dev Container may execute arbitrary code**, quindi fare clic sul
    pulsante **Got It**

> ![](./media/image45.png)

5.  L'avvio del contenitore Dev richiederà 13-15 minuti. Dopo la
    distribuzione, premere **Enter**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

6.  Premere un tasto qualsiasi per chiudere il terminale

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image47.png)

## Attività 8: Distribuire l'app di chat in Azure

1.  Accedere ad Azure con Azure Developer CLI. Eseguire il seguente
    comando sul Terminale

> BashCopy 
>
> **azd auth login** 
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image48.png)

2.  Il browser predefinito si apre per accedere. Accedere con l'account
    della sottoscrizione di Azure.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

> ![A login screen with a red box and blue text AI-generated content may
> be incorrect.](./media/image50.png)

3.  Chiudere il browser

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image51.png)

4.  Una volta effettuato l'accesso, i dettagli dell'accesso Azure
    vengono popolati nel terminale.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image52.png)

5.  Creare un nuovo ambiente azd. Eseguire il seguente comando sul
    Terminale

> Copy 
>
> **azd env new** 

6.  Inserire il nome del nuovo ambiente come +++**chatapprag+++**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image53.png)

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image54.png)

7.  Assegnare il gruppo di risorse di Azure esistente. Eseguire il
    seguente comando nel Terminale

> azd env set AZURE_RESOURCE_GROUP {Name of existing resource group} 
>
>  
>
> azd env set AZURE_LOCATION {Location of existing resource group} 
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image55.png)

8.  Assegnare il servizio Azure AI Search esistente. Eseguire il
    seguente comando nel Terminale

> +++azd env set AZURE_SEARCH_SERVICE {Name of existing Azure AI Search
> service}+++ 
>
>  
>
> +++azd env set AZURE_SEARCH_SERVICE_RESOURCE_GROUP {Name of existing
> resource group with ACS service}+++ 
>
>  
>
> +++azd env set AZURE_SEARCH_SERVICE_LOCATION {Location of existing
> service}+++ 
>
>  
>
> +++azd env set AZURE_SEARCH_SERVICE_SKU {Name of SKU}+++ 
>
> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image56.png)

9.  Controllare le risorse esistenti assegnate, selezionare Azure e
    scegliere il file **.env**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image57.png)

10. Creare un nuovo ambiente azd:

> shellCopy 
>
> **azd up** 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image58.png)

11. Selezionare la tua sottoscrizione di Azure

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image59.png)

12. Quando richiesto, **Enter a value for the
    ‘documentIntelligenceResourceGroupLocation’ infrastructure
    parameter** e selezionare **West US2.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image60.png)

13. Quando richiesto, **enter a value for the
    ‘openAiResourceGroupLocation’ infrastructure parameter** selezionare
    **France Central.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image61.png)

14. Attendere fino a quando l'app non viene distribuita. Il
    completamento della distribuzione potrebbe richiedere **35-40**
    minuti.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image62.png)
>
> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image63.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image64.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image65.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image66.png)

15. Dopo che l'applicazione è stata distribuita correttamente, verrà
    visualizzato un URL stampato nella console. Fare clic su quell'URL
    per interagire con l'applicazione nel tuo browser. Sarà simile al
    seguente:

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image67.png)

16. Aprire il browser, andare alla barra degli indirizzi, incollare il
    link. A questo punto, il gruppo di risorse verrà aperto in un nuovo
    browser

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image68.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image69.png)

## Attività 9: Verificare le risorse distribuite nel portale di Azure

1.  Selezionare **Resource groups**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image70.png)

2.  Fare clic sul **Resource group** assegnato.

![](./media/image71.png)

3.  Assicurarsi che la risorsa seguente sia stata distribuita
    correttamente

- Azure App Service 

&nbsp;

- Azure Application Insights 

&nbsp;

- Container App 

&nbsp;

- Container registry 

&nbsp;

- Azure OpenAI 

&nbsp;

- Azure Document Intelligence 

&nbsp;

- Azure Search Service 

&nbsp;

- Azure Storage Account 

&nbsp;

- Azure Speech Service 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image72.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

4.  Nel gruppo di risorse e fare clic su **AI Search service.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image74.png)

5.  Assicurarsi che gli indici vengano distribuiti correttamente

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image75.png)

6.  Tornare a resorcegroup e fare clic su **Storage account.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image76.png)

7.  Dal menu di navigazione a sinistra, fare clic su **Containers**.
    Assicurati che i dati vengano distribuiti correttamente

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image77.png)

## Attività 10: Utilizzare l'app di chat per ottenere risposte dai file PDF

1.  Attendere il completamento della distribuzione dell'applicazione
    Web.

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image78.png)

2.  Nella pagina dell'app Web di **GPT+Eneterprise data |Sample**,
    immettere il testo seguente e fare clic sull' icona **Submit** come
    mostrato nell'immagine seguente.

> **What happens in a performence review?** 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image79.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image80.png)

3.  Dalla risposta, selezionare una **citazione**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image81.png)

4.  Nel riquadro di destra, usare le schede per capire come è stata
    generata la risposta.

[TABLE]

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image82.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image83.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image84.png)

5.  Selezionare nuovamente la scheda selezionata per chiudere il
    riquadro.

6.  L'intelligenza della chat è determinata dal modello OpenAI e dalle
    impostazioni utilizzate per interagire con il modello.

7.  Selezionare **Developer settings**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image85.png)

![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image86.png)

[TABLE]

8.  Selezionare la casella di controllo **Suggest follow-up questions**
    e porre di nuovo la stessa domanda.

![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image87.png)

9.  Inserire il seguente testo e fare clic sull' icona **Submit** come
    mostrato nell'immagine sottostante.

> What happens in a performance review? 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image88.png)

10. La chat ha restituito domande di follow-up suggerite come le
    seguenti

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image89.png)

11. Nella scheda **Settings**, deseleziona **Use semantic ranker for
    retrieval**.

![A screenshot of a phone AI-generated content may be
incorrect.](./media/image90.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image91.png)

12. Inserire il seguente testo e fare clic sull'icona **Submit** come
    mostrato nell'immagine sottostante.

> What happens in a performance review? 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image92.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image93.png)

## Attività 11: Eliminare le risorse

1.  Per eliminare Gruppo di risorse, digitare **Resource groups** nella
    barra di ricerca del portale di Azure, spostarsi e fare clic su
    **Resource groups** in **Services**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image94.png)

2.  Fare clic sul gruppo di risorse dell'app Web di esempio.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image95.png)

3.  Nella home page del gruppo di risorse, selezionare **all
    resources**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image96.png)

4.  Selezionare **Delete**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image97.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image98.png)

**Sommario**

In questo lab si è appreso come configurare e distribuire
un'applicazione di chat intelligente usando la suite di strumenti e
servizi di Azure. A partire dall'installazione di strumenti essenziali
come Azure CLI e Node.js, è stato configurato l'ambiente di sviluppo
usando Dev Containers in Visual Studio Code. È stata distribuita
un'applicazione di chat che usa Azure OpenAI e Azure Cognitive Search
per rispondere alle domande dai file PDF. Infine, sono state eliminate
le risorse distribuite per gestire in modo efficace le risorse. Questa
esperienza pratica ti ha fornito le competenze necessarie per sviluppare
e gestire applicazioni di chat intelligenti usando il modello di
generazione aumentata di recupero in Azure.
