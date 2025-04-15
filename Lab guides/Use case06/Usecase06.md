# Caso d'uso 06 - Distribuzione dell'app di chat in Azure Container Apps con PostgreSQL Flexible Server

**Obiettivo:**

- Per configurare l'ambiente di sviluppo in Windows installando Azure
  CLI, Node.js, assegnando ruoli di sottoscrizione di Azure, avviando
  Docker Desktop e abilitando Visual Studio Code con l'estensione Dev
  Containers.

- Per distribuire e testare Custom Chat Application con PostgreSQL e
  OpenAI in Azure.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image1.jpeg)

In questo caso d'uso, si configurerà un ambiente di sviluppo completo,
si distribuirà un'applicazione di chat integrata con PostgreSQL e si
verificherà la distribuzione in Azure. Ciò comporta l'installazione di
strumenti essenziali come Azure CLI, Docker e Visual Studio Code
(l'abbiamo già fatto per te su host env), la configurazione dei ruoli
utente in Azure, la distribuzione dell'applicazione utilizzando Azure
Developer CLI e l'interazione con le risorse distribuite per garantire
la funzionalità.

**Tecnologie chiave usate**: Python, FastAPI, modelli Azure OpenAI,
Azure Database per PostgreSQL e azure-container-apps,ai-azd-templates.

**Durata stimata**: 45 minuti

**Tipo di laboratorio:** Guidato dall'istruttore

**Prerequisiti:**

Account GitHub: è necessario che tu abbia le tue credenziali di accesso
a GitHub. Se non ne hai, creane uno da qui -
+++<https://github.com/signup?user_email=&source=form-home-signupobjectives+++>

**Esercizio 1 : Provisioning, distribuzione dell'applicazione e test dal
browser**

## Attività 0: Comprendere la macchina virtuale e le credenziali

In questa attività, identificheremo e comprenderemo le credenziali che
utilizzeremo in tutto il laboratorio.

1.  Scheda **Instructions **tiene la guida del laboratorio con le
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

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image2.png)

3.  La scheda **Help **contiene le informazioni di supporto. Il valore
    **ID** è  **Lab instance ID** che verrà utilizzato durante
    l'esecuzione del lab.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image3.png)

## 

## Attività 1: Registrare il Service provider 

1.  Aprire un browser, andare a +++https://portal.azure.com+++ e
    accedere con il tuo account Cloud Slice qui sotto.

> Username: [*+++@lab.CloudPortalCredential*](mailto:+++@lab.CloudPortalCredential)(User1).Username+++ 
>
> Password: [*+++@lab.CloudPortalCredential(User1).Password*](mailto:+++@lab.CloudPortalCredential(User1).Password)+++ 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image4.png)
>
> ![Uno screenshot di una casella di accesso Descrizione generata
> automaticamente](./media/image5.png)

2.  Fare clic sul riquadro **Subscriptions**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image6.png)

3.  Fare clic sul nome dell'abbonamento.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image7.png)

4.  Espandere **Settings** dal menu di navigazione a sinistra. Fare clic
    su **Resource providers**, immettere
    +++**Microsoft.AlertsManagement+++** e selezionare i,t, e quindi
    fare clic su **Register**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image8.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image9.png)

5.  Fare clic su **Resource providers**, immettere
    +++**Microsoft.DBforPostgreSQL+++** e selezionare i,t, e quindi fare
    clic su **Register**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image10.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image11.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image12.png)

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image13.png)

6.  Ripetere i passaggi \#10 e \#11 per registrare i provider di risorse
    seguenti.

- Microsoft.Search

- Microsoft.Web

- Microsoft.ManagedIdentity

## Attività 2: Copiare il nome del gruppo di risorse esistente

1.  Nella home page, fare clic sul riquadro **Resource groups**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

2.  Assicurarsi di avere già un gruppo di risorse creato per il lavoro.
    Non eliminare mai questo gruppo di risorse. È invece possibile
    eliminare le risorse all'interno del gruppo di risorse, ma non il
    gruppo di risorse stesso.

3.  Fare clic sul nome del gruppo di risorse

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

4.  Copiare il nome del gruppo di risorse e salvarlo in Blocco note per
    usarlo per la distribuzione di tutte le risorse in questo gruppo di
    risorse

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

## Attività 3: Eseguire Docker

1.  Sul desktop, fare doppio clic su **Docker Desktop**.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image17.png)

2.  Eseguire il Docker Desktop.

> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image18.png)

## Compito 4 : Ambiente di sviluppo aperto

1.  Aprire il browser, passare alla barra degli indirizzi, digitare o
    incollare l'URL seguente:
    +++[https://github.com/technofocus-pte/rag-postgres-openai-python-CSTesting.git+++
    si](https://github.com/technofocus-pte/rag-postgres-openai-python-CSTesting.git+++%C2%A0tab)
    apre la scheda e viene chiesto di aprire nel codice di Visual
    Studio. Selezionare **Open Visual Studio Code.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image19.jpeg)

2.  Fare clic su **fork **per biforcare il repository. Assegnare un nome
    univoco al repository e fare clic sul pulsante **Create repo**.

> ![](./media/image20.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image21.png)

3.  Cliccare su** Code -\> Codespaces -\> Codespaces+ **

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)

4.  Attendere la configurazione dell'ambiente Codespaces. Ci vogliono
    pochi minuti per la configurazione completa

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)
>
> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image24.png)

## Attività 5: Effettuare il provisioning dei servizi e distribuire l'applicazione in Azure

1.  Eseguire il seguente comando sul Terminale. Generare il codice da
    copiare. Copiare il codice e premere **Enter**.

+++azd auth login+++

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image25.png)

2.  Si apre il browser predefinito per inserire il codice generato da
    verificare. Inserire il codice e fare clic su **Next**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image26.png)

3.  Accedere con le credenziali di Azure.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image27.png)

4.  Per creare un ambiente per le risorse di Azure, eseguire Azure
    Developer CLI seguente. Ti chiede di inserire il nome dell'ambiente.
    Inserire un nome a tua scelta e premere invio (ad esempio:
    +++ragpgpy+++)

**Nota:** Quando si crea un ambiente, assicurarsi che il nome sia
composto da lettere minuscole.

> +++azd env new+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

5.  Eseguire il comando Azure Developer CLI seguente per effettuare il
    provisioning delle risorse di Azure e distribuire il codice.

+++azd provision+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

6.  Quando richiesto, selezionare una **sottoscrizione** per creare le
    risorse e selezionare l'area più vicina alla propria posizione. In
    questo lab è stata scelta l' area ** East US2**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

7.  Verrà visualizzato il messaggio “**Enter a value for the
    'existingResourceGroupName' infrastructure parameter:**” immettere
    il gruppo di risorse copiato nell'attività 1 (ad esempio:
    \*\*ResourceGroup1 utilizzato per la sezione di sviluppo).\*\*È
    possibile copiare il nome del gruppo di risorse dalla sezione
    **Resources **come illustrato nell'immagine seguente

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

8.  Quando richiesto, e**nter a value for the 'openAILocation'
    infrastructure parameter,** selezionare la regione più vicina alla
    tua posizione; in questo laboratorio, abbiamo scelto la regione
    **North Central US**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

9.  Il provisioning delle risorse richiederà circa 5-10 minuti. Fare
    clic su **Yes **se richiesto.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image33.png)

10. Attendere che il modello esegua correttamente il provisioning di
    tutte le risorse.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

11. Eseguire il comando seguente per impostare il gruppo di risorse

+++azd env set AZURE_RESOURCE_GROUP {your resource group name}+++![A
screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

12. Eseguire il comando seguente per distribuire l'app in Azure.

+++azd deploy+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

13. Attendere il completamento della distribuzione. La distribuzione
    richiede \<5

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

14. Fare clic sul collegamento dell'endpoint dell'app Web distribuito.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

15. Fare clic su **Open**. Si apre una nuova scheda con l'app

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

16. L'app si apre.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image40.png)

**Attività 6: Utilizzare l'app di chat per ottenere risposte dai file**

1.  Nella pagina **RAG on database | OpenAI+PoastgreSQL web app**, fare
    clic sul pulsante **Best shoe for hiking?** e osservare l'output

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image41.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

2.  Fare clic su  **Clear chat.**

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png)

3.  Nella pagina ** RAG on database |OpenAI+PoastgreSQL web app**, fare
    clic sul pulsante **Climbing gear cheaper than \\30** e osservare
    l'output

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image44.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

4.  Fare clic su  **Clear chat.**

**Attività 7: Verificare le risorse distribuite nel portale di Azure**

1.  Nella home page del portale di Azure, fare clic su **Resource
    Groups**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

2.  Fare clic sul nome del gruppo di risorse

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

3.  Assicurarsi che la risorsa seguente sia stata distribuita
    correttamente

- Container App 

&nbsp;

- Application Insights 

&nbsp;

- Container Apps Environment 

&nbsp;

- Log Analytics workspace 

&nbsp;

- Azure OpenAI 

&nbsp;

- Azure Database for PostgreSQL flexible server 

&nbsp;

- Container registry 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

4.  Fare clic sul nome di risorsa **Azure OpenAI**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

5.  In **Overview **nel menu di spostamento a sinistra fare clic su
    ** Go to Azure AI Foundry portal** e selezionare per aprire una
    nuova scheda.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

6.  Fare clic su **Shared resources -\> Deployments** dal menu di
    navigazione a sinistra e assicurarsi che **gpt-35-turbo**,
    **text-embedding-ada-002** venga distribuito correttamente

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image51.png)

**Attività 8 : Pulire tutte le risorse**

Per pulire tutte le risorse create da questo esempio:

1.  Tornare al **Azure portal -\> Resource group- \> Resource group
    name..**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image52.png)

2.  Selezionare tutta la risorsa e quindi fare clic su Delete come
    mostrato nell'immagine sottostante. (**NON ELIMINARE il** gruppo di
    risorse)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image53.png)

3.  Digitare **delete** nella casella di testo e quindi fare clic su
    **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image54.png)

4.  Confermare l'eliminazione cliccando su **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image55.png)

5.  Tornare alla scheda del portale Github e aggiornare la pagina.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

6.  Cliccare su **Code**, selezionare il ramo creato per questo lab e
    cliccare su **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

7.  Confermare l'eliminazione del ramo facendo clic sul pulsante
    **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image58.png)

**Riepilogo:**:Questo caso d'uso illustra la distribuzione di
un'applicazione di chat con PostgreSQL e OpenAI su Azure, concentrandosi
sulla distribuzione e la gestione delle applicazioni basate sul cloud.
Hai configurato l'ambiente di sviluppo, installato gli strumenti
necessari come Azure CLI, configurato le risorse di Azure utilizzando
Azure Developer CLI e distribuito l'applicazione in Azure Container
Apps.
