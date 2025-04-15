**Caso d'uso 01 - Analisi delle tendenze della moda con GPT-4 Turbo e
Vision su Azure OpenAI**

**Introduzione:**

GPT-4 Turbo con Visione nel servizio Azure OpenAI è ora disponibile in
anteprima pubblica. GPT-4 Turbo with Vision è un grande modello
multimodale (LMM) sviluppato da OpenAI in grado di analizzare le
immagini e fornire risposte testuali alle domande su di esse. Incorpora
sia l'elaborazione del linguaggio naturale che la comprensione visiva.
Con la modalità avanzata, è possibile usare le funzionalità di Visione
artificiale di Azure per generare informazioni dettagliate aggiuntive
dalle immagini

**Obiettivo:**

- Per distribuire le risorse di Azure OpenAI e configurarle.

- Per distribuire un modello Azure OpenAI specifico, ad esempio GPT-4
  Vision.

- Configurare l'ambiente di sviluppo con Python, Jupyter Notebook e le
  librerie necessarie.

- Questo caso d'uso è correlato ai casi d'uso della moda. Questi
  potrebbero riguardare l'analisi delle immagini, la generazione di
  testo o altre attività di intelligenza artificiale.

## Attività 0: Comprendere la macchina virtuale e le credenziali

In questa attività, identificheremo e comprenderemo le credenziali che
utilizzeremo in tutto il laboratorio.

1.  La Scheda **Instructions **tiene la guida del laboratorio con le
    istruzioni da seguire durante il laboratorio.

2.  La scheda **Resources **contiene le credenziali necessarie per
    l'esecuzione del lab.

    - **URL**: URL del portale di Azure

    - **Subscription**: questo è l'ID dell'abbonamento assegnato
      all'utente

    - **Username**: l'ID utente con cui è necessario accedere ai servizi
      di Azure.

    - **Password**: password per l'account di accesso di Azure.
      Chiamiamo questo nome utente e password come credenziali di
      accesso di Azure. Useremo questi crediti ogni volta che
      menzioniamo le credenziali di accesso di Azure.

    - **Resource Group**: il **gruppo di risorse** assegnato all'utente.

\[! Avviso\] **Importante:** assicurarsi di creare tutte le risorse in
questo gruppo di risorse

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image1.png)

3.  La scheda **Help **contiene le informazioni di supporto. Il valore
    **ID** è **Lab instance ID** che verrà utilizzato durante
    l'esecuzione del lab.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)

## Attività 1 : Registrare il fornitore di servizi

1.  Aprire un browser, andare a +++https://portal.azure.com+++ e
    accedere con il tuo account Cloud Slice qui sotto.

> Username: [*+++@lab.CloudPortalCredential*](mailto:+++@lab.CloudPortalCredential)(User1).Username+++ 
>
> Password: [*+++@lab.CloudPortalCredential(User1).Password*](mailto:+++@lab.CloudPortalCredential(User1).Password)+++ 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image3.png)
>
> ![Uno screenshot di una casella di accesso Descrizione generata
> automaticamente](./media/image4.png)

2.  Fare clic sul riquadro **Subscriptions**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image5.png)

3.  Fare clic sul nome dell'abbonamento.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image6.png)

4.  Espandere Impostazioni dal menu di navigazione a sinistra. Fare clic
    su **Resource providers**, immettere
    +++**Microsoft.AlertsManagement+++** e selezionare i,t, quindi fare
    clic su **Register**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image7.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image8.png)

5.  Fare clic su** Resource providers**, immettere
    +++**Microsoft.DBforPostgreSQL+++** e selezionare i,t, quindi fare
    clic su **Register**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image9.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image10.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image11.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image12.png)

6.  Ripetere i passaggi \#10 e \#11 per registrare Resource providers
    seguenti.

- Microsoft.Search

- Microsoft.Web

- Microsoft.ManagedIdentity

## **Attività 2: Creare una risorsa Azure OpenAI**

1.  Nel portale di Azure fare clic sul **menu del portale**
    rappresentato da tre barre orizzontali nell'angolo superiore
    sinistro della pagina, come illustrato nell'immagine seguente.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image13.png)

2.  Navigare e fare clic su **+ Create a resource**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image14.png)

3.  Nella pagina **Create a resource**, nella barra di ricerca di
    **Search services and marketplace,** digitare **Azure OpenAI**,
    quindi premere il pulsante **Enter**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image15.png)

4.  Nella pagina **Marketplace,** passare al riquadro **Azure OpenAI**,
    fare clic sul pulsante V accanto a **Create**, quindi spostarsi e
    fare clic su **Azure OpenAI** come illustrato nell'immagine
    seguente.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image16.png)

5.  Nella finestra **Create Azure OpenAI**, nella scheda **Basics**,
    immettere i dettagli seguenti e fare clic sul pulsante **Next**.

    1.  **Subscription**: selezionare l'abbonamento assegnato

    2.  **Resource group:** selezionare il gruppo di risorse assegnato

    3.  **Region**: per questo lab si userà un modello **gpt-4-vision**.
        Questo modello è attualmente disponibile solo in [alcune
        regioni](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models).
        Selezionare una regione da questo elenco, In questo laboratorio
        **Sweden Central** sta utilizzando per questa risorsa.

    4.  **Name**: **aoai-gpt4-visionXXXXX** (XXXXX può essere Lab
        instant ID)

    5.  **Pricing tier**: selezionare **Standard S0**

> **Nota**: per trovare l'ID istantaneo del tuo laboratorio, selezionare
> 'Help' e copiare l'ID istantaneo.
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image17.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image18.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image19.png)

6.  Nella scheda **Network**, lasciare tutti i pulsanti di opzione nello
    stato predefinito e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image20.png)

7.  Nella scheda **Tag**, lasciare tutti i campi nello stato predefinito
    e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image21.png)

8.  Nella scheda **Review + submit**, una volta superata la convalida,
    fare clic sul pulsante **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

9.  Attendere il completamento della distribuzione. L'implementazione
    richiederà circa 2-3 minuti.

10. Nella finestra **Microsoft.CognitiveServicesOpenAI**, al termine
    della distribuzione, fare clic sul pulsante **Go to resource**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)

11. Fare clic su **Keys and Endpoints** dal menu di spostamento a
    sinistra, quindi copiare il valore dell'endpoint in un blocco note
    in **AzureAI ENDPOINT** e la chiave in una variabile **AzureAIKey**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image24.png)

12. Nella finestra **aoai-gpt4-visionXX** fare clic su **Overview** nel
    menu di spostamento a sinistra, scorrere verso il basso fino al
    **Get Started** e fare clic sul pulsante **Go to AzureOpenAI
    Studio** come illustrato nell'immagine seguente per aprire **Azure
    OpenAI Studio** in un nuovo browser.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

## **Attività 3: Distribuzione di un modello Azure OpenAI gpt-4-vision**

1.  Nel homepage di **Azure AI Foundry | Azure Open AI Service**,
    passare alla sezione **Components** e fare clic su **Deployments**.

2.  Nella finestra **Deployments,** visualizzare il **+Deploy model** e
    selezionare **Deploy base model.  **

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

3.  Nella finestra di dialogo **Select a model**, navigare e selezionare
    attentamente **gpt-4**, quindi fare clic sul pulsante **Confirm**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

4.  Nella finestra di dialogo **Deploy model gpt-4,** nel campo
    **Deployment name**, assicurarsi che **gpt-4** selezioni il tipo di
    distribuzione come **Standard** e selezionare Modello ersion come
    Vision- preview. Quindi fare clic sul pulsante **Deploy**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

## Attività 4: GPT-4 Turbo con demo Vision

1.  Nella casella di ricerca di Windows, digitare Visual Studio, quindi
    fare clic su **Visual Studio Code**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image30.png)

2.  Nell'editor di **Visual Studio Code** , fare clic su **File**,
    quindi navigare e fare clic su **Open Folder**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image31.png)

3.  Navigare e selezionare la cartella **GPT4V-Fashion** da
    **C:\LabFiles** e fare clic sul pulsante **Select Folder**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

4.  Se viene visualizzata una finestra di dialogo: **Do you trust the
    authors of the files in this folder?,** quindi fare clic su **Yes, I
    trust the author**.

![Uno screenshot di un computer Descrizione generata automaticamente con
confidenza media](./media/image33.png)

5.  Nell'elenco a discesa di Visual Studio Code **Gpt** **4V-FASHION,**
    fare clic sul file **azure.env**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

1.  Aggiornare i parametri, sostituire **Azure OpenAI Endpoint, Azure
    OpenAI Key(**i valori che hai salvato nel tuo blocco note nell'
    **attività 1)** e salvare il file.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

2.  Nell'elenco a discesa di Visual Studio Code GPT **4V-FASHION** e
    selezionare **GPT-4 with Vision demo with Azure Open AI - Fashion
    usecase.ipynb** notebook.

> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image36.png)

3.  Nella pagina principale dell'editor di Visual Studio Code, scorrere
    verso il basso fino all'intestazione dei **install requirements** ed
    eseguire la prima cella. Se viene richiesto di selezionare
    l'ambiente, selezionare **Python Environments** come mostrato
    nell'immagine.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image37.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image38.png)

4.  Se viene richiesto di selezionare il percorso, selezionare il
    percorso **Python version 3.11.5** come mostrato nell'immagine.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image39.png)

5.  Se viene visualizzata una finestra di dialogo di avviso di sicurezza
    di Windows, fare clic su **Allow access**.

> ![](./media/image40.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image41.png)
>
> ![](./media/image42.png)
>
> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image43.png)

6.  Per riavviare il kernel Jupyter, fare clic sul pulsante **Restart**.

> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image44.png)

7.  Per importare le librerie, selezionare la **4a** cella. Quindi,
    eseguire la cella facendo clic sull' icona **start**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image45.png)

8.  Selezionare la **5a** cella. Quindi, eseguire la cella facendo clic
    sull'icona **start**.

> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image46.png)

9.  Per controllare le versioni del sistema OpenAI, selezionare la
    **6a**, 7a, 8a e 9a cella. Quindi, eseguire la cella facendo clic
    sull'icona **start**.

> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image47.png)

10. Per caricare i valori di configurazione, selezionare ed eseguire la
    **10a**, 11a e 12a cella facendo clic sul pulsante **Play**.

> ![Uno screenshot di un programma per computer Descrizione generata
> automaticamente](./media/image48.png)

11. Definire una funzione di supporto per creare incorporamenti,
    selezionare ed eseguire la 13° e la 14a cella facendo clic sul
    pulsante **Play**.

> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image49.png)
>
> ![A screen shot of a computer program AI-generated content may be
> incorrect.](./media/image50.png)

12. Per eseguire l'esempio, selezionare ed eseguire la 15a e la 16a
    cella facendo clic sul pulsante **Play**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image51.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image52.png)

13. Per eseguire l'esempio, selezionare ed eseguire la **17a, 18a**
    cella facendo clic sul pulsante **Play**.

> ![](./media/image53.png)
>
> ![A screenshot of a computer program AI-generated content may be
> incorrect.](./media/image54.png)

14. Per eseguire l'esempio, selezionare ed eseguire la **19a, 20a**
    cella facendo clic sul pulsante **Play**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image55.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image56.png)

15. Per eseguire l'esempio, selezionare ed eseguire la **21a e la 22a**
    cella facendo clic sul pulsante **Play**.

> ![](./media/image57.png)
>
> ![](./media/image58.png)

16. Per eseguire l'esempio, selezionare ed eseguire le celle **23a,
    24a** facendo clic sul pulsante **Play**.

> ![A box on a table AI-generated content may be
> incorrect.](./media/image59.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image60.png)

17. Per eseguire l'esempio, selezionare ed eseguire la **25a,** la
    **26a** cella facendo clic sul pulsante **Play**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image61.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image62.png)

18. Per eseguire l'esempio, selezionare ed eseguire la **27a e la 28a**
    cella facendo clic sul pulsante **Play**.

> ![](./media/image63.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image64.png)

19. Per eseguire l'esempio, selezionare ed eseguire la **27a e la 28a**
    cella facendo clic sul pulsante **Play**.

> ![A screenshot of a person AI-generated content may be
> incorrect.](./media/image65.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image66.png)

20. Per generare WebApp, selezionare ed eseguire la **29a** cella
    facendo clic sul pulsante **Play**.

> ![A screen shot of a computer program AI-generated content may be
> incorrect.](./media/image67.png)

21. Per generare la WebApp, selezionare ed eseguire la **30esima** cella
    cliccando sul pulsante **Play**.

> ![A screen shot of a computer AI-generated content may be
> incorrect.](./media/image68.png)

22. Dopo che l'applicazione è stata distribuita correttamente, viene
    visualizzato un URL nel terminale. Copiare l' **URL**

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image69.png)

23. Aprire il browser, andare alla barra degli indirizzi, incollare il
    link URL Publick. ![A screenshot of a computer AI-generated content
    may be incorrect.](./media/image70.png)

24. Aprire il browser, andare alla barra degli indirizzi, incollare il
    link dell'URL locale. Selezionare qualsiasi elemento

![A screenshot of a website AI-generated content may be
incorrect.](./media/image71.png)

25. Fare clic sul pulsante **Submit**.

> ![A screenshot of a watch AI-generated content may be
> incorrect.](./media/image72.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

## 

## Attività 5: Eliminare le risorse

1.  Per eliminare l'account di archiviazione, passare alla **home page
    di Azure portal**, fare clic su **Resource groups. **

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image74.png)

2.  Fare clic sul gruppo di risorse **ResourceGroup1**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image75.png)

3.  Nella home page del **Resource group,** selezionare **Delete
    resource group**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image76.png)

4.  Nel riquadro **Delete Resources** visualizzato sul lato destro,
    andare al campo **Enter “resource group name” to confirm deletion**,
    quindi fare clic sul pulsante **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image77.png)

5.  Nella finestra di dialogo **Delete confirmation**, fare clic sul
    pulsante **Delete**.

> ![A screenshot of a computer error AI-generated content may be
> incorrect.](./media/image78.png)

6.  Fare clic sull'icona a forma di campana, vedrai la notifica –
    **Deleted resource group AOAI-RG89.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image79.png)

**Sommario**

In questo laboratorio pratico, i partecipanti approfondiscono le
funzionalità avanzate di intelligenza artificiale usando Azure OpenAI. A
partire dalla configurazione delle risorse essenziali di Azure,
implementano modelli di intelligenza artificiale come GPT-4-vision. Il
laboratorio esplora in particolare come GPT-4, dotato di capacità di
visione, possa rivoluzionare le attività legate alla moda: si pensi al
riconoscimento delle immagini, ai consigli di stile personalizzati e
all'analisi delle tendenze.
