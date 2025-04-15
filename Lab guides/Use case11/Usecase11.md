# Caso d'uso 11 - Creazione di un Custom AI Agent con Azure AI Foundry e integrazione della ricerca

**Tempo stimato: 45 min**

## Obiettivo

L'obiettivo di questo lab è guidare i partecipanti nella creazione di un
agente basato sull'intelligenza artificiale usando i servizi di Azure AI
e Search integration. I partecipanti impareranno a configurare,
integrare e testare i componenti chiave per creare un agente funzionale
in grado di recuperare e interagire in modo intelligente con le
informazioni, migliorando l'esperienza utente e la produttività.

## Soluzione

Questo lab è incentrato sull'integrazione dei servizi di intelligenza
artificiale di Azure con funzionalità di ricerca avanzate per creare una
soluzione affidabile e intelligente. Enfatizza la configurazione di un
agente basato sull'intelligenza artificiale, consentendo il recupero dei
dati senza interruzioni e fornendo risposte contestuali. Sfruttando
l'intelligenza artificiale e l'integrazione della ricerca, la soluzione
mira a semplificare i flussi di lavoro, migliorare il processo
decisionale e aumentare il coinvolgimento degli utenti attraverso
interazioni intuitive ed efficienti.

## Attività 1: Creare una risorsa Azure AI Search

1.  In un Web browser, aprire il portale di Azure
    all'https://portal.azure.com e accedere usando le credenziali di
    amministratore di Office 365.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image1.png)

2.  Nella home page, selezionare **+ Create a resource** e cercare
    ** Azure AI Search**. **Creare** quindi una nuova risorsa Azure AI
    Search con le impostazioni seguenti:

    - **Subscription**: *selezionare la sottoscrizione di Azure.*

    - **Resource group**: *selezionare o creare un gruppo di risorse,
      qui selezioniamo **RG4OpenAI***

    - **Service name**: *inserire un nome di servizio univoco, qui lo
      chiamiamo **copilotXXXX***

    - **Location**: *fare una scelta **casuale** da una delle seguenti
      regioni, qui selezioniamo Canada Est*

- Australia East 

&nbsp;

- Canada East 

&nbsp;

- East US 

&nbsp;

- East US 2 

&nbsp;

- France Central 

&nbsp;

- Japan East 

&nbsp;

- North Central US 

&nbsp;

- Sweden Central 

&nbsp;

- Switzerland 

  - **Pricing tier**: Standard

  - Fare clic su **Review+create,** quindi fare clic su **Create.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image3.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image4.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image5.png)
>
> Successivamente, si creerà un Azure AI Hub (che include un servizio
> Azure OpenAI) nella stessa area della risorsa Azure AI Search. Le
> risorse di Azure OpenAI sono vincolate a livello di tenant da quote a
> livello di area. Le regioni elencate includono la quota predefinita
> per i tipi di modello utilizzati in questo esercizio. La scelta
> casuale di un'area riduce il rischio che una singola area raggiunga il
> limite di quota negli scenari in cui si condivide un tenant con altri
> utenti. Nel caso in cui venga raggiunto un limite di quota più avanti
> nell'esercizio, è possibile che sia necessario creare un altro Azure
> AI hub in un'area diversa.

3.  Attendere il completamento della distribuzione delle risorse di
    Azure AI Search.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image6.png)

## 

## Attività 2: Creare un progetto di Azure AI

1.  In un Web browser, aprire il portale di Azure AI Foundry in
    <https://ai.azure.com> e accedere usando le credenziali di Azure.

2.  Nella home page, selezionare **+ Create project.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image7.png)

3.  Nella procedura guidata **Create a project,** inserire il nome del
    progetto come **ProgettoXXXX** e fare clic su **Customize**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image8.png)

4.  **In Customize,** connettersi alla risorsa Azure AI Search,
    immettere i dettagli seguenti, selezionare **Next ** ed esaminare la
    configurazione.

    - **Hub name**: ***hubXXXX***

    - **Azure Subscription**: *la sottoscrizione di Azure*

    - **Resource group**: **RG4OpenAI**

    - **Location**: *la stessa posizione della risorsa Ricerca di
      intelligenza artificiale di Azure, **Canada East ***

    - **Connect Azure AI Services or Azure OpenAI:** (nuovo)
      *Riempimento automatico con il nome dell'hub selezionato*

    - **Connect Azure AI Search**: *selezionare la risorsa Azure AI
      Search, **copilotXXXX***

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image9.png)

5.  Selezionare **Next,** quindi **Create **e attendere il completamento
    del processo.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image10.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image11.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image12.png)

## 

## Attività 3: Distribuire i modelli

Per implementare la soluzione sono necessari due modelli:

- Un modello di *incorporamento* per vettorializzare i dati di testo per
  un'indicizzazione e un'elaborazione efficienti.

- Un modello in grado di generare risposte in linguaggio naturale alle
  domande in base ai dati.

1.  Nel portale di Azure AI Foundry, nel progetto, nel riquadro di
    spostamento a sinistra, in **My assets**, selezionare la pagina
    **Models + endpoints**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)

2.  Nella pagina **Manage deployments of your models and services,**
    fare clic su **+Deploy model** e selezionare **Deploy base model.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)

3.  Nella pagina **Select a model**, cercare e selezionare
    **text-embedding-ada-002** model e fare clic su **Confirm.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

4.  Nel riquadro **Deploy model text-embedding-ada,** fare clic su
    **Customize ** e immettere i dettagli seguenti nella procedura
    guidata Deploy model:

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image16.png)

- **Deployment name**: text-embedding-ada-002

- **Deployment type**: Standard

- **Model version**: *seleziona la versione predefinita*

- **AI resource**: *selezionare la risorsa creata in precedenza*

- **Tokens per Minute Rate Limit (thousands)**: 5K

- **Content filter**: DefaultV2

- **Enable dynamic quota**: Disabled

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image17.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image18.png)

5.  Ripetere i passaggi precedenti per distribuire un modello
    **gpt-35-turbo-16k** con il nome di distribuzione gpt-35-turbo-16k.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image19.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image20.png)
>
> **Nota**: la riduzione dei Tokens Per Minute (TPM) consente di evitare
> un uso eccessivo della quota disponibile nella sottoscrizione in uso.
> 5.000 TPM sono sufficienti per i dati utilizzati in questo esercizio.

## Attività 4: Aggiungere dati al progetto

I dati per il tuo copilot sono costituiti da una serie di opuscoli di
viaggio in formato PDF dell'agenzia di viaggi fittizia *Margie's
Travel*. Aggiungiamoli al progetto.

1.  Passare alla cartella denominata **brochures **nei file C:\Lab del
    sistema.

2.  Nel portale di Azure AI Foundry, nel progetto, nel riquadro di
    spostamento a sinistra, in ** My assets**, selezionare la pagina
    ** Data + indexes**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image21.png)

3.  Selezionare **+ New data**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image22.png)

4.  Nella procedura guidata ** Add your data**, espandere il menu a
    discesa per selezionare **Upload files/folders**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image23.png)

5.  Selezionare **Upload folder ** e selezionare la cartella
    **brochures**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image24.png)

6.  Selezionare **Next** sullo schermo.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image25.png)

7.  Attendere che la cartella venga caricata e tieni presente che
    contiene diversi file .pdf.

8.  Nella pagina successiva di **name and finish**, inserire il nome dei
    dati come **data0212** e fare clic su **Create.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image26.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image27.png)

## Attività 5: Creare un indice per i dati

Dopo aver aggiunto un'origine dati al progetto, è possibile usarla per
creare un indice nella risorsa Azure AI Search.

1.  Nel portale di Azure AI Foundry, nel progetto, nel riquadro di
    spostamento a sinistra, in ** My assets**, selezionare la pagina
    **Data + indexes**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image28.png)

2.  Nella scheda **Indexes** aggiungere un nuovo indice con le
    impostazioni seguenti e quindi selezionare **Next**.

    - **Source location**:

      - **Data source**: dati in Azure AI Studio

        - *Selezionare la fonte dei dati delle **brochure** – **dataXXXX
          ***

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image29.png)

- Configurare l'indice come indicato di seguito, quindi selezionare
  **Next.**

  - **Select Azure AI Search service:**: *selezionare la connessione
    **AzureAISearch** alla risorsa Azure AI Search*

  &nbsp;

  - **Vector index**: brochures-index

  &nbsp;

  - **Virtual machine**: Auto select

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image30.png)

- Configurare l'impostazione di ricerca come indicato di seguito e
  selezionare **Next**, nella finestra Review, fare clic su **Create
  Vector Index**.

  - **Vector settings**: aggiungi la ricerca vettoriale a questa risorsa
    di ricerca

  &nbsp;

  - **Azure OpenAI connection**: *selezionare la risorsa Azure OpenAI
    predefinita per l'hub.*

> ![Uno screenshot di una ricerca delle impostazioni Descrizione
> generata automaticamente](./media/image31.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image32.png)

3.  Attendere il completamento del processo di indicizzazione,
    operazione che può richiedere alcuni minuti. L'operazione di
    creazione dell'indice è costituita dai seguenti processi:

    - Crack, suddivisione e incorporamento dei token di testo nei dati
      delle brochure.

    - Creare l'indice di Azure AI Search.

    - Registrare l'asset dell'indice.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image33.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

## 

## Attività 6: Testare l'indice

Prima di utilizzare l'indice in un flusso di prompt basato su RAG,
verificare che possa essere utilizzato per influenzare le risposte di
generative AI.

1.  Nel riquadro di spostamento a sinistra, selezionare la pagina
    **Playgrounds** e quindi selezionare **Chat Playground.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image35.png)

2.  Nella pagina Chat, nel riquadro **Setup**, assicurarsi che sia
    selezionata la distribuzione del modello **gpt-35-turbo-16k**.
    Quindi, nel pannello principale della sessione di chat, inviare il
    messaggio **Where can I stay in New York?**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image36.png)

3.  Esaminare la risposta, che deve essere una risposta generica del
    modello senza dati dall'indice.

4.  Nel riquadro Setup, espandere il campo **Add your data**, quindi
    aggiungere l'indice del progetto **brochures-index** e selezionare
    il tipo di ricerca **hybrid (vector + keyword)**.

> ![Uno screenshot di una chat Descrizione generata
> automaticamente](./media/image37.png)
>
> **Nota**: alcuni utenti scoprono che gli indici appena creati non sono
> immediatamente disponibili. L'aggiornamento del browser di solito
> aiuta, ma se riscontri ancora il problema in cui non riesce a trovare
> l'indice, potrebbe essere necessario attendere fino a quando l'indice
> non viene riconosciuto.

5.  Dopo che l'indice è stato aggiunto e la sessione di chat è stata
    riavviata, inviare nuovamente il prompt **Where can I stay in New
    York?**

> ![Uno screenshot di una chat Descrizione generata
> automaticamente](./media/image38.png)

6.  Esaminare la risposta, che deve essere basata sui dati dell'indice.

## Attività 7: Usare l'indice in un flusso di prompt

L'indice vettoriale è stato salvato nel progetto Azure AI Foundry,
consentendoti di usarlo facilmente in un flusso di prompt.

1.  Nel portale di Azure AI Foundry, nel progetto, nel riquadro di
    spostamento a sinistra, in **Build and customize**, selezionare la
    pagina **Prompt flow** e fare clic su **+Create.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image39.png)

2.  Creare un nuovo flusso di prompt clonando l' esempio di
    **Multi-Round Q&A on Your Data** nella raccolta. Salvare il clone di
    questo esempio in una cartella denominata **brochure-flow**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image40.png)
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image41.png)
>
> Nota: se le autorizzazioni sono in errore, riprova con un nuovo nome
> dopo 2 minuti e il flusso verrà clonato.
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image42.png)

3.  Quando si apre la pagina di progettazione del flusso di prompt,
    rivedere il **brochure-flow**. Il suo grafico dovrebbe assomigliare
    alla seguente immagine:

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image43.png)

![Uno screenshot di un grafico di flusso di prompt](./media/image44.png)

> Il flusso di prompt di esempio in uso implementa la logica di prompt
> per un'applicazione di chat in cui l'utente può inviare in modo
> iterativo input di testo all'interfaccia di chat. La cronologia delle
> conversazioni viene conservata e inclusa nel contesto per ogni
> iterazione. Il flusso di prompt orchestra una sequenza di *strumenti*
> per:

- Aggiungere la cronologia all'input della chat per definire un prompt
  sotto forma di una forma contestualizzata di una domanda.

- Recuperare il contesto utilizzando l'indice e un tipo di query di
  propria scelta in base alla domanda.

- Generare il contesto del prompt utilizzando i dati recuperati
  dall'indice per aumentare la domanda.

- Creare varianti di prompt aggiungendo un messaggio di sistema e
  strutturando la cronologia chat.

- Inviare il prompt a un modello linguistico per generare una risposta
  in linguaggio naturale.

4.  Usare il pulsante **Start compute session** per avviare il calcolo
    di runtime per il flusso.

> Attendere l'avvio del runtime. In questo modo viene fornito un
> contesto di calcolo per il flusso di prompt. Durante l'attesa, nella
> scheda **Flow**, esaminare le sezioni relative agli strumenti nel
> flusso.
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image45.png)

5.  Nella sezione **Inputs**, assicurati che gli input includano:

    - **chat_history**

    - **chat_input**

La cronologia chat predefinita in questo esempio include alcune
conversazioni sull'intelligenza artificiale.

![A screenshot of a chat box AI-generated content may be
incorrect.](./media/image46.png)

6.  Nella sezione **Outputs**, assicurati che l'output includa:

    - **chat_output** con valore ${chat_with_context.output}

> ![A screenshot of a chat box AI-generated content may be
> incorrect.](./media/image47.png)

7.  Nella sezione **modify_query_with_history** selezionare le seguenti
    impostazioni (lasciando le altre così come sono):

    - **Connection**: *la risorsa Azure OpenAI predefinita per l'hub di
      intelligenza artificiale*

    - **Api**: chat

    - **deployment_name**: GPT-35-TURBO-16K

    - **response_format**: {"type":"text"}

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image48.png)

8.  Attendere l'avvio della sessione di calcolo, quindi nella sezione
    **lookup **impostare i seguenti valori dei parametri:

    - **mlindex_content**: *Seleziona il campo vuoto per aprire il
      riquadro Generate*

      - **index_type**: Indice registrato

      &nbsp;

      - **mlindex_asset_id**: Brochures-index:1

    - **query**: ${modify_query_with_history.output}

    - **query_type**: Hybrid (vector + keyword)

    - **top_k**: 2

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image49.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image50.png)

9.  Nella sezione **generate_prompt_context,** esaminare lo script
    Python e assicurarsi che gli **inputs** per questo strumento
    includano il parametro seguente:

    - **search_result** *(oggetto):* ${lookup.output}

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image51.png)

10. Nella sezione **Prompt_variants,** esaminare lo script Python e
    assicurarsi che gli **inputs** per questo strumento includano i
    parametri seguenti:

    - **contexts ***(string):* ${generate_prompt_context.output}

    - **chat_history** *(string):* ${inputs.chat_history}

    - **chat_input** *(string):* ${inputs.chat_input}

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image52.png)

11. Nella sezione **chat_with_context,** selezionare le seguenti
    impostazioni (lasciando le altre così come sono):

    - **Connection**: Default_AzureOpenAI

    - **Api**: Chat

    - **deployment_name**: GPT-35-TURBO-16K

    - **response_format**: {"type":"text"}

Assicurarsi quindi che gli **inputs** per questo strumento includano i
seguenti parametri:

- **prompt_text** *(string):* ${Prompt_variants.output}

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image53.png)

12. Sulla barra degli strumenti, usare il pulsante **Save **per salvare
    le modifiche apportate agli strumenti nel flusso di prompt.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image54.png)

13. Sulla barra degli strumenti, selezionare **Chat**. Si apre un
    riquadro di chat con la cronologia delle conversazioni di esempio e
    l'input già compilato in base ai valori di esempio. Puoi ignorarli.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image55.png)

14. Nel riquadro della chat, sostituire l'input predefinito con la
    domanda **Where can I stay in London?** e presentarla.

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image56.png)

15. Esaminare la risposta, che deve essere basata sui dati dell'indice.

16. Esaminare gli output per ogni strumento nel flusso.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image57.png)

17. Nel riquadro della chat, inserire la domanda ** What can I do
    there?**

18. Esaminare la risposta, che dovrebbe essere basata sui dati
    dell'indice e tenere conto della cronologia delle chat (quindi
    "there" è inteso come "in London").

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image58.png)

19. Esaminare gli output per ogni strumento nel flusso, notando come
    ogni strumento nel flusso ha operato sui suoi input per preparare un
    prompt contestualizzato e ottenere una risposta appropriata.

## Attività 8: Sfida

Ora che hai sperimentato come integrare i tuoi dati in un copilota
creato con il portale di Azure AI Foundry, esploriamo ulteriormente!

Provare ad aggiungere una nuova origine dati tramite il portale di Azure
AI Foundry, indicizzarla e integrare i dati indicizzati in un flusso di
prompt. Alcuni set di dati che potresti provare sono:

- Una raccolta di articoli (di ricerca) che hai sul tuo computer.

- Una serie di presentazioni di conferenze passate.

Sii il più intraprendente possibile per creare la tua origine dati e
integrarla nel tuo flusso di prompt. Prova il nuovo flusso di prompt e
inviare prompt a cui potrebbe rispondere solo il set di dati che hai
scelto!

## Attività 9: Pulizia

Per evitare costi di Azure e utilizzo delle risorse non necessari, è
necessario rimuovere le risorse distribuite in questo esercizio.

Al termine dell'esplorazione di Azure AI Foundry, tornare al [portale di
Azure](https://portal.azure.com/) all'https://portal.azure.com e
accedere usando le credenziali di Azure, se necessario. Eliminare quindi
le risorse nel gruppo di risorse in cui è stato effettuato il
provisioning delle risorse Azure AI Search e per Azure AI.
