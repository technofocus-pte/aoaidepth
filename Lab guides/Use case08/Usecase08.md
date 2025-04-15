Caso d'uso 08 - Creare un'app di chat personalizzata con Azure AI
Foundry SDK

**Tempo stimato: 120 minuti**

## Obiettivo

L'obiettivo di questo lab è compilare, valutare e distribuire un agente
basato su RAG (Retrieval-Augmented Generation) usando Azure AI Foundry
SDK. Il lab guida l'utente nella configurazione dell'ambiente di
progetto e di sviluppo, nella distribuzione di modelli di intelligenza
artificiale (ad esempio, GPT-4 e text-embedding-ada-002),
nell'integrazione di Azure AI Search per il recupero dei documenti e
nella creazione di un'applicazione di chat RAG (Knowledgeret)
personalizzata. L'obiettivo è quello di basare le risposte del modello
di intelligenza artificiale con dati di prodotto pertinenti, sviluppare
un'interfaccia di chat personalizzata e valutare le prestazioni delle
risposte generate.

## Soluzione

La soluzione prevede la configurazione di un progetto in Azure AI
Foundry, la distribuzione di modelli di intelligenza artificiale (GPT-4
e text-embedding-ada-002) e l'integrazione di Azure AI Search per
archiviare e recuperare dati di prodotto personalizzati. Include la
creazione di script Python per generare incorporamenti vettoriali,
creare indici di ricerca e interrogarli per ottenere informazioni
rilevanti sul prodotto. Viene sviluppata un'interfaccia di chat basata
su RAG per fornire risposte motivate sfruttando i risultati della
ricerca e le prestazioni dell'app di chat vengono valutate utilizzando
set di dati e metriche predefiniti per migliorarne l'efficacia.

## Esercizio 0: Informazioni sulla macchina virtuale e sulle credenziali

In questo esercizio, identificheremo e comprenderemo le credenziali che
utilizzeremo in tutto il laboratorio.

**Importante:** Eseguire ogni passaggio di questo esercizio per
conoscere i termini generici e le credenziali che verranno utilizzate
per l'esecuzione del laboratorio.

1.  La scheda **Instructions** tiene la guida del laboratorio con le
    istruzioni da seguire durante il laboratorio.

2.  La scheda **Resources** contiene le credenziali necessarie per
    l'esecuzione del lab.

- **URL** : URL del portale di Azure

- **Subscription**: questo è l' **ID** dell' **abbonamento** assegnato
  all'utente

- **Username**: l' **ID utente** con cui è necessario **accedere** ai
  **servizi di Azure**.

- **Password** : **password** per l' **account di accesso di Azure**.

> Chiamiamo questo nome utente e password come **Azure login
> credentials**. Useremo questi crediti ogni volta che menzioniamo
> **Azure login credentials**.

- **Resource Group**: il **gruppo di risorse** assegnato all'utente.

> **Importante**: assicurarsi di creare tutte le risorse in questo
> gruppo di risorse

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image1.png)

3.  La scheda **Help** contiene le informazioni di supporto. Il valore
    **ID** è **Lab instance ID** che verrà utilizzato durante
    l'esecuzione del lab.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image2.png)

## Esercizio 1 - Configurare l'ambiente di progetto e di sviluppo per creare un'app RAG (Knowledgeret) personalizzata con Azure AI Foundry SDK

### Attività 1: Creare un progetto

Per creare un progetto in Azure AI Foundry, seguire questa procedura:

1.  Accedere ad Azure AI Foundry all'indirizzo
    +++<https://ai.azure.com/>+++ **Accedere** utilizzando le **Azure
    login credentials**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image3.png)

2.  Selezionare **+ Create project.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image4.png)

3.  Inserire +++**RAGproj\<Lab instance ID\>**+++ come nome per il
    progetto, fare clic su **Customize**.

> **Nota:** sostituire **\<Lab instance ID\>** con **Lab instance ID**
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image5.png)

4.  Nella pagina successiva, inserire i seguenti dettagli e fare clic su
    **Next.**

> **Hub name** - +++hub\<Lab instance ID\>+++
>
> **Subscription** - Seleziona l'abbonamento assegnato
>
> Crea nuovo gruppo di risorse: selezionare il gruppo di risorse
> assegnato (ResourceGroup1)
>
> **Location**: East US 2 o Sweden Central (durante l'esecuzione di
> questo lab sono stati utilizzati East US 2)
>
> Lasciare il resto come predefinito e fare clic su **Next**.
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image6.png)

5.  Nella pagina **Review and finish**, fare clic su **Create.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image7.png)

6.  La creazione della risorsa richiederà alcuni minuti.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image8.png)

7.  Chiudere le finestre pop-up, se ne vengono visualizzate.

8.  Dalla home page del progetto, annotare **Project connection string**
    in un blocco note da utilizzare nell'attività successiva di questo
    esercizio.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image9.png)

### Attività 2: Distribuire i modelli

Per creare un'app di chat basata su RAG, sono necessari due modelli: un
modello di chat Azure OpenAI (gpt-4o-mini) e un modello di
incorporamento Azure OpenAI (text-embedding-ada-002). Distribuire questi
modelli nel progetto Azure AI Foundry, usando questo set di passaggi per
ogni modello.

Questi passaggi distribuiscono un modello in un endpoint in tempo reale
dal catalogo di modelli del portale AI Foundry:

1.  Nel riquadro di navigazione a sinistra, selezionare **Model
    catalog**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image10.png)

2.  Selezionare il modello **gpt-4o-mini** dall'elenco dei modelli. Puoi
    usare la barra di ricerca per trovarlo.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image11.png)

3.  Nella pagina dei dettagli del modello selezionare **Deploy**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image12.png)

4.  Lasciare il **Deployment name** predefinito. selezionare **Deploy**.
    Oppure, se il modello non è disponibile nella tua regione, viene
    selezionata una regione diversa e collegata al tuo progetto. In
    questo caso, selezionare **Create resource and deploy**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image13.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)

5.  Dopo aver distribuito il **gpt-4o-mini**, ripetere i passaggi per
    distribuire il modello +++**text-embedding-ada-002**+++.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image15.png)

### 

### Attività 3: Creare un servizio di Azure AI Search

L'obiettivo di questa applicazione è quello di basare le risposte del
modello nei dati personalizzati. L'indice di ricerca viene utilizzato
per recuperare i documenti pertinenti in base alla domanda dell'utente.

Per creare un indice di ricerca, è necessario un servizio di Azure AI
Search e una connessione.

1.  Accedere al portale di Azure all'indirizzo
    +++<https://portal.azure.com>+++ usando le credenziali di accesso di
    Azure.

2.  Dalla barra di ricerca della home page, cercare +++**AI search**+++
    e selezionalo.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image16.png)

3.  Fare clic sull'icona **+ Create** e inserire i seguenti dettagli.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

4.  Inserire i dettagli seguenti e selezionare **Review + create**.

- **Subscription**: selezionare l'abbonamento assegnato

- **Resource Group**: selezionare il gruppo di risorse assegnato

- **Service name**: immettere +++**aisearch\<Lab instance ID\>**+++
  sostituendo l'ID istanza Lab con l'ID della macchina virtuale.

- **Region**: selezionare Sweden Central o East US 2 (qui si usa East US
  2)

- Pricing tier - Selezionare **Standard**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image18.png)

5.  Esaminare i dettagli e selezionare **Create**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image19.png)

6.  Attendere che la distribuzione abbia esito positivo come nello
    screenshot seguente prima di procedere con il passaggio successivo.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image20.png)

### 

### Attività 4: Connettere Azure AI Search al progetto

Nel portale di Azure AI Foundry verificare la presenza di una risorsa
connessa ad Azure AI Search.

1.  Dal progetto in Azure AI Foundry, selezionare **Management center**
    nel riquadro sinistro.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image21.png)

2.  Nella sezione **Connected resources,** selezionare **New
    connection** e quindi **Azure AI Search. **

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image22.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)

3.  Selezionare **API key** in **Authentication** e selezionare **Add
    connection**.

> ![Uno screenshot di un motore di ricerca Descrizione generata
> automaticamente](./media/image24.png)
>
> ![Uno screenshot di un motore di ricerca Descrizione generata
> automaticamente](./media/image25.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image26.png)

### Attività 5: Installare Azure CLI e accedere

Si installa Azure CLI e si accede dall'ambiente di sviluppo locale, in
modo da poter usare le credenziali utente per chiamare il servizio Azure
OpenAI.

1.  Cercare +++**PowerShell**+++ dalla barra di ricerca di Windows e
    aprilo in modalità amministratore.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image27.png)

2.  Aprire Windows Power Shell e incollare il comando indicato di
    seguito ed eseguilo.

> $progressPreference = 'silentlyContinue' 
>
> Write-Host "Installing WinGet PowerShell module from PSGallery..." 
>
> Install-PackageProvider -Name NuGet -Force | Out-Null 
>
> Install-Module -Name Microsoft.WinGet.Client -Force -Repository
> PSGallery | Out-Null 
>
> Write-Host "Using Repair-WinGetPackageManager cmdlet to bootstrap
> WinGet..." 
>
> Repair-WinGetPackageManager 
>
> Write-Host "Done." 

3.  Installare Azure CLI dal terminale usando il comando seguente:

winget install -e --id Microsoft.AzureCLI

Selezionare **Y** quando viene richiesta l'accettazione.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image28.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

4.  Dopo aver installato Azure CLI, accedere usando il comando az login
    e accedere usando il browser:

+++Az login+++

Selezionare **Work or school account** e fare clic su **Continue**.

![Uno screenshot dello schermo di un computer Descrizione generata
automaticamente](./media/image31.png)

5.  Accedere con le tue **Azure login credentials**.

![Schermata di un programma per computer Descrizione generata
automaticamente](./media/image32.png)

6.  Immettere **1** per il prompt **Select a subscription** e fare clic
    su **Enter**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image33.png)

### 

### Attività 6: Creare un nuovo ambiente Python

Per prima cosa è necessario creare un nuovo ambiente Python da
utilizzare per installare il pacchetto necessario per questo tutorial.
NON installare pacchetti nella tua installazione globale di python.
Dovresti sempre utilizzare un ambiente virtuale o conda quando installi
i pacchetti python, altrimenti puoi interrompere l'installazione globale
di Python.

**Creare un ambiente virtuale**

1.  Da Power Shell, passare a **C:\Users\Admin** eseguendo i comandi
    seguenti.

> +++cd\\++ 
>
> +++cd Users\Admin+++ 

2.  Creare una cartella con il nome del progetto, **RAGproj\<Lab
    instance id\>, by entering the following command in your
    powershell.**

**Nota:** sostituire \<Project name\> con il nome del tuo progetto nel
comando seguente ed eseguilo.

+++**mkdir \<Project name\>**+++ 

![Schermo di un computer con testo bianco e verde Descrizione generata
automaticamente](./media/image34.png)

3.  Nel tuo terminale inserire il seguente comando per accedere alla
    nuova posizione della cartella

+++**cd \<Project name\>**+++ 

Sostituire \<Project name\> con il nome della cartella che hai creato
nel passaggio precedente.

![Una schermata blu con testo bianco Descrizione generata
automaticamente](./media/image35.png)

4.  Creare un ambiente virtuale utilizzando i comandi seguenti

+++py -3 -m venv .venv+++ 

 +++.venv\scripts\activate+++ 

> ![Schermata di un codice per computer Descrizione generata
> automaticamente](./media/image36.png)
>
> L'attivazione dell'ambiente Python significa che quando si esegue
> python o pip dalla riga di comando, si utilizza l'interprete Python
> contenuto nella cartella .venv dell'applicazione.

5.  Aprire **VS Code**. Selezionare **File -\> Open Folder** e
    selezionare la cartella **RAGproject** che abbiamo creato nei
    passaggi precedenti.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image37.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image38.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image39.png)

### Attività 7: Installare i pacchetti

Installare azure-ai-projects (preview) e azure-ai-inference (preview),
insieme ad altri pacchetti necessari.

1.  Creare un file denominato +++**requirements.txt**+++ nella cartella
    **Project** e aggiungere i seguenti pacchetti al file:

> azure-ai-projects 
>
> azure-ai-inference\[prompts\] 
>
> azure-identity 
>
> azure-search-documents 
>
> pandas 
>
> python-dotenv 
>
> opentelemetry-api

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image40.png)

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image41.png)

2.  Nella barra di navigazione in alto cliccare su file e **save all**.

3.  Fare clic con il pulsante destro del mouse sul requirements.txt e
    selezionare **Open in Integrated Terminal**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image43.png)

4.  Eseguire il seguente comando per accedere all'ambiente virtuale

py -3 -m venv .venv

.venv\scripts\activate

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image44.png)

5.  Eseguire il comando +++az login+++ e accedere con le credenziali di
    accesso di Azure. Selezionare **1** per selezionare l'abbonamento.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image45.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image46.png)

6.  Per installare i pacchetti necessari, eseguire il codice seguente.

+++pip install -r requirements.txt+++

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image47.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image48.png)

> **Nota:** se ricevi un avviso di una nuova versione di pip, eseguire i
> comandi seguenti per aggiornare pip
>
> +++pip install -r requirements.txt+++

+++python.exe -m pip install --upgrade pip+++

> ![Uno screenshot di un programma per computer Descrizione generata
> automaticamente](./media/image49.png)

### 

### Attività 8: Creare uno script di supporto

1.  Creare una nuova cartella denominata **src**. Eseguendo il seguente
    comando nel terminale.

mkdir src

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image50.png)

2.  Creare un nuovo file nella cartella **src** e chiamalo
    +++**config.py**+++

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image51.png)

3.  Aggiungere il codice seguente a **config.py** e salvarlo.

\# ruff: noqa: ANN201, ANN001 

 

import os 

import sys 

import pathlib 

import logging 

from azure.identity import DefaultAzureCredential 

from azure.ai.projects import AIProjectClient 

from azure.ai.inference.tracing import AIInferenceInstrumentor 

 

\# load environment variables from the .env file 

from dotenv import load_dotenv 

 

load_dotenv() 

 

\# Set "./assets" as the path where assets are stored, resolving the
absolute path: 

ASSET_PATH = pathlib.Path(\_\_file\_\_).parent.resolve() / "assets" 

 

\# Configure an root app logger that prints info level logs to stdout 

logger = logging.getLogger("app") 

logger.setLevel(logging.INFO) 

logger.addHandler(logging.StreamHandler(stream=sys.stdout)) 

 

 

\# Returns a module-specific logger, inheriting from the root app
logger 

def get_logger(module_name): 

    return logging.getLogger(f"app.{module_name}") 

 

 

\# Enable instrumentation and logging of telemetry to the project 

def enable_telemetry(log_to_project: bool = False): 

    AIInferenceInstrumentor().instrument() 

 

    \# enable logging message contents 

    os.environ\["AZURE_TRACING_GEN_AI_CONTENT_RECORDING_ENABLED"\] =
"true" 

 

    if log_to_project: 

        from azure.monitor.opentelemetry import configure_azure_monitor 

 

        project = AIProjectClient.from_connection_string( 

            conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
credential=DefaultAzureCredential() 

        ) 

        tracing_link = f"https://ai.azure.com/tracing?

wsid=/subscriptions/{project.scope\['subscription_id'\]}/resourceGroups/{project.scope\['resource_group_name'\]}/providers/Microsoft.MachineLearningServices/workspaces/{project.scope\['project_name'\]}" 

        application_insights_connection_string =
project.telemetry.get_connection_string() 

        if not application_insights_connection_string: 

            logger.warning( 

                "No application insights configured, telemetry will not
be logged to project. Add application insights at:" 

            ) 

            logger.warning(tracing_link) 

 

            return 

 

       
configure_azure_monitor(connection_string=application_insights_connection_string) 

        logger.info("Enabled telemetry logging to project, view traces
at:") 

        logger.info(tracing_link) 

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image52.png)

**Nota**: questo script di file config.py appena creato verrà utilizzato
nel prossimo esercizio.

### Attività 9: Configurare le variabili di ambiente

La stringa di connessione del progetto è necessaria per chiamare il
servizio Azure OpenAI dal codice. In questa guida introduttiva si salva
questo valore in un file con estensione env, ovvero un file che contiene
variabili di ambiente che l'applicazione può leggere.

1.  Creare un nuovo file +++**.env+++** nella directory **src** e
    incollare il seguente codice:

Sostituire la **\<your-connection-string\>** con il valore della stringa
di connessione del progetto salvato nel blocco note nell'attività 1.

AIPROJECT_CONNECTION_STRING=\<your-connection-string\> 

AISEARCH_INDEX_NAME="example-index" 

EMBEDDINGS_MODEL="text-embedding-ada-002" 

INTENT_MAPPING_MODEL="gpt-4o-mini" 

CHAT_MODEL="gpt-4o-mini" 

EVALUATION_MODEL="gpt-4o-mini" 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image53.png)

**Nota**: la stringa di connessione è disponibile nella home page del
progetto Azure AI Foundry in **Overview**.

## Esercizio 2: Creare un'app RAG (Knowledgeret) personalizzata con Azure AI Foundry SDK 

### Attività 1: Creare dati di esempio per l'app di chat

L'obiettivo di questa applicazione basata su RAG è quello di radicare le
risposte del modello nei dati personalizzati. Si usa un indice di Azure
AI Search che archivia i dati vettorializzati dal modello di
incorporamento. L'indice di ricerca viene utilizzato per recuperare i
documenti pertinenti in base alla domanda dell'utente.

1.  Dalla configurazione di VS Code aperta, creare una cartella
    denominata +++**assets**+++ nella cartella **src**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image54.png)

2.  Copiare **products.csv** file da **C:\LabFiles** e incollalo nella
    cartella principale del **Project**.

Nota: questa operazione deve essere eseguita in File Explorer e quindi
si rifletterà nel VS Code.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image55.png)

3.  Andare su **File** nella barra di navigazione in alto e fare clic su
    **Save all.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image56.png)

### Attività 2: Creare un indice di ricerca

> L'indice di ricerca viene utilizzato per archiviare i dati
> vettorializzati dal modello di incorporamento. L'indice di ricerca
> viene utilizzato per recuperare i documenti pertinenti in base alla
> domanda dell'utente.

1.  Nel VS code, creare un file denominato
    +++**create_search_index.py**+++ nella cartella src here it (ovvero
    la stessa directory in cui è stata inserita la cartella **assets**,
    non all'interno della cartella **assets**).

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image57.png)

2.  Aprire il file creato, **create_search_index.py** file e aggiungere
    il seguente codice per importare le librerie richieste, creare un
    client di progetto e configurare alcune impostazioni:

> import os 
>
> from azure.ai.projects import AIProjectClient 
>
> from azure.ai.projects.models import ConnectionType 
>
> from azure.identity import DefaultAzureCredential 
>
> from azure.core.credentials import AzureKeyCredential 
>
> from azure.search.documents import SearchClient 
>
> from azure.search.documents.indexes import SearchIndexClient 
>
> from config import get_logger 
>
>  
>
> \# initialize logging object 
>
> logger = get_logger(\_\_name\_\_) 
>
>  
>
> \# create a project client using environment variables loaded from the
> .env file 
>
> project = AIProjectClient.from_connection_string( 
>
>     conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential() 
>
> ) 
>
>  
>
> \# create a vector embeddings client that will be used to generate
> vector embeddings 
>
> embeddings = project.inference.get_embeddings_client() 
>
>  
>
> \# use the project client to get the default search connection 
>
> search_connection = project.connections.get_default( 
>
>     connection_type=ConnectionType.AZURE_AI_SEARCH,
> include_credentials=True 
>
> ) 
>
>  
>
> \# Create a search index client using the search connection 
>
> \# This client will be used to create and delete search indexes 
>
> index_client = SearchIndexClient( 
>
>     endpoint=search_connection.endpoint_url,
> credential=AzureKeyCredential(key=search_connection.key) 
>
> ) 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image58.png)

3.  Ora aggiungere la funzione alla fine del **create_search_index.py**
    per definire un indice di ricerca:

> import pandas as pd 
>
> from azure.search.documents.indexes.models import ( 
>
>     SemanticSearch, 
>
>     SearchField, 
>
>     SimpleField, 
>
>     SearchableField, 
>
>     SearchFieldDataType, 
>
>     SemanticConfiguration, 
>
>     SemanticPrioritizedFields, 
>
>     SemanticField, 
>
>     VectorSearch, 
>
>     HnswAlgorithmConfiguration, 
>
>     VectorSearchAlgorithmKind, 
>
>     HnswParameters, 
>
>     VectorSearchAlgorithmMetric, 
>
>     ExhaustiveKnnAlgorithmConfiguration, 
>
>     ExhaustiveKnnParameters, 
>
>     VectorSearchProfile, 
>
>     SearchIndex, 
>
> ) 
>
>  
>
>  
>
> def create_index_definition(index_name: str, model: str) -\>
> SearchIndex: 
>
>     dimensions = 1536  \# text-embedding-ada-002 
>
>     if model == "text-embedding-3-large": 
>
>         dimensions = 3072 
>
>  
>
>     \# The fields we want to index. The "embedding" field is a vector
> field that will 
>
>     \# be used for vector search. 
>
>     fields = \[ 
>
>         SimpleField(name="id", type=SearchFieldDataType.String,
> key=True), 
>
>         SearchableField(name="content",
> type=SearchFieldDataType.String), 
>
>         SimpleField(name="filepath",
> type=SearchFieldDataType.String), 
>
>         SearchableField(name="title",
> type=SearchFieldDataType.String), 
>
>         SimpleField(name="url", type=SearchFieldDataType.String), 
>
>         SearchField( 
>
>             name="contentVector", 
>
>            
> type=SearchFieldDataType.Collection(SearchFieldDataType.Single), 
>
>             searchable=True, 
>
>             \# Size of the vector created by the
> text-embedding-ada-002 model. 
>
>             vector_search_dimensions=dimensions, 
>
>             vector_search_profile_name="myHnswProfile", 
>
>         ), 
>
>     \] 
>
>  
>
>     \# The "content" field should be prioritized for semantic
> ranking. 
>
>     semantic_config = SemanticConfiguration( 
>
>         name="default", 
>
>         prioritized_fields=SemanticPrioritizedFields( 
>
>             title_field=SemanticField(field_name="title"), 
>
>             keywords_fields=\[\], 
>
>             content_fields=\[SemanticField(field_name="content")\], 
>
>         ), 
>
>     ) 
>
>  
>
>     \# For vector search, we want to use the HNSW (Hierarchical
> Navigable Small World) 
>
>     \# algorithm (a type of approximate nearest neighbor search
> algorithm) with cosine 
>
>     \# distance. 
>
>     vector_search = VectorSearch( 
>
>         algorithms=\[ 
>
>             HnswAlgorithmConfiguration( 
>
>                 name="myHnsw", 
>
>                 kind=VectorSearchAlgorithmKind.HNSW, 
>
>                 parameters=HnswParameters( 
>
>                     m=4, 
>
>                     ef_construction=1000, 
>
>                     ef_search=1000, 
>
>                     metric=VectorSearchAlgorithmMetric.COSINE, 
>
>                 ), 
>
>             ), 
>
>             ExhaustiveKnnAlgorithmConfiguration( 
>
>                 name="myExhaustiveKnn", 
>
>                 kind=VectorSearchAlgorithmKind.EXHAUSTIVE_KNN, 
>
>                
> parameters=ExhaustiveKnnParameters(metric=VectorSearchAlgorithmMetric.COSINE), 
>
>             ), 
>
>         \], 
>
>         profiles=\[ 
>
>             VectorSearchProfile( 
>
>                 name="myHnswProfile", 
>
>                 algorithm_configuration_name="myHnsw", 
>
>             ), 
>
>             VectorSearchProfile( 
>
>                 name="myExhaustiveKnnProfile", 
>
>                 algorithm_configuration_name="myExhaustiveKnn", 
>
>             ), 
>
>         \], 
>
>     ) 
>
>  
>
>     \# Create the semantic settings with the configuration 
>
>     semantic_search =
> SemanticSearch(configurations=\[semantic_config\]) 
>
>  
>
>     \# Create the search index definition 
>
>     return SearchIndex( 
>
>         name=index_name, 
>
>         fields=fields, 
>
>         semantic_search=semantic_search, 
>
>         vector_search=vector_search, 
>
>     ) 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image59.png)

4.  Ora aggiungere la funzione in create_search_index.py per creare la
    funzione per aggiungere un file csv all'indice:

> \# define a function for indexing a csv file, that adds each row as a
> document 
>
> \# and generates vector embeddings for the specified content_column 
>
> def create_docs_from_csv(path: str, content_column: str, model: str)
> -\> list\[dict\[str, any\]\]: 
>
>     products = pd.read_csv(path) 
>
>     items = \[\] 
>
>     for product in products.to_dict("records"): 
>
>         content = product\[content_column\] 
>
>         id = str(product\["id"\]) 
>
>         title = product\["name"\] 
>
>         url = f"/products/{title.lower().replace(' ', '-')}" 
>
>         emb = embeddings.embed(input=content, model=model) 
>
>         rec = { 
>
>             "id": id, 
>
>             "content": content, 
>
>             "filepath": f"{title.lower().replace(' ', '-')}", 
>
>             "title": title, 
>
>             "url": url, 
>
>             "contentVector": emb.data\[0\].embedding, 
>
>         } 
>
>         items.append(rec) 
>
>  
>
>     return items 
>
>  
>
>  
>
> def create_index_from_csv(index_name, csv_file): 
>
>     \# If a search index already exists, delete it: 
>
>     try: 
>
>         index_definition = index_client.get_index(index_name) 
>
>         index_client.delete_index(index_name) 
>
>         logger.info(f"🗑️  Found existing index named '{index_name}',
> and deleted it") 
>
>     except Exception: 
>
>         pass 
>
>  
>
>     \# create an empty search index 
>
>     index_definition = create_index_definition(index_name,
> model=os.environ\["EMBEDDINGS_MODEL"\]) 
>
>     index_client.create_index(index_definition) 
>
>  
>
>     \# create documents from the products.csv file, generating vector
> embeddings for the "description" column 
>
>     docs = create_docs_from_csv(path=csv_file,
> content_column="description", model=os.environ\["EMBEDDINGS_MODEL"\]) 
>
>  
>
>     \# Add the documents to the index using the Azure AI Search
> client 
>
>     search_client = SearchClient( 
>
>         endpoint=search_connection.endpoint_url, 
>
>         index_name=index_name, 
>
>         credential=AzureKeyCredential(key=search_connection.key), 
>
>     ) 
>
>  
>
>     search_client.upload_documents(docs) 
>
>     logger.info(f"➕ Uploaded {len(docs)} documents to '{index_name}'
> index") 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image60.png)

5.  Infine, aggiungere le funzioni seguenti in create_search_index.py
    per creare l'indice e registrarlo nel progetto cloud. Dopo aver
    aggiunto il codice, andare su File dalla barra in alto e fare clic
    su **Save all.**

> if \_\_name\_\_ == "\_\_main\_\_": 
>
>     import argparse 
>
>  
>
>     parser = argparse.ArgumentParser() 
>
>     parser.add_argument( 
>
>         "--index-name", 
>
>         type=str, 
>
>         help="index name to use when creating the AI Search index", 
>
>         default=os.environ\["AISEARCH_INDEX_NAME"\], 
>
>     ) 
>
>     parser.add_argument( 
>
>         "--csv-file", type=str, help="path to data for creating search
> index", default="assets/products.csv" 
>
>     ) 
>
>     args = parser.parse_args() 
>
>     index_name = args.index_name 
>
>     csv_file = args.csv_file 
>
>  
>
>     create_index_from_csv(index_name, csv_file) 
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image61.png)

6.  Fare clic con il pulsante destro del mouse sul
    **create_search_index.py** e selezionare **Open in integrated
    terminal**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image62.png)

7.  Dal tuo terminale, accedere alle tue credenziali di accesso Azure e
    seguire le istruzioni per autenticare il tuo account:

> +++az login+++
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image63.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image64.png)

8.  Eseguire il codice per compilare l'indice in locale e registrarlo
    nel progetto cloud:

> +++python create_search_index.py+++
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image65.png)

9.  Dopo l'esecuzione dello script, è possibile visualizzare l'indice
    appena creato dal portale di Azure.

10. Passare al **Resource Group** assegnato **-\> Your search service
    created(aisearchLabinstanceID) -\> Search management -\> Indexes.**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image66.png)

11. Se si esegue nuovamente lo script con lo stesso nome di indice,
    viene creata una nuova versione dello stesso indice.

### Attività 3: Ottenere i documenti del prodotto

> Successivamente, viene creato uno script per ottenere i documenti del
> prodotto dall'indice di ricerca. Lo script esegue una query
> nell'indice di ricerca per i documenti che corrispondono alla domanda
> di un utente.
>
> **Creare script per ottenere i documenti del prodotto**
>
> Quando la chat riceve una richiesta, cerca tra i tuoi dati per trovare
> informazioni pertinenti. Questo script usa Azure AI SDK per eseguire
> una query sull'indice di ricerca per i documenti che corrispondono
> alla domanda di un utente. Quindi restituisce i documenti all'app di
> chat.

1.  Da VS Code, creare un file denominato
    +++**get_product_documents.py**+++ nella cartella **src**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image67.png)

2.  Copiare e incollare il codice seguente nel file. Iniziare con il
    codice per importare le librerie necessarie, creare un client di
    progetto e configurare le impostazioni.

> import os 
>
> from pathlib import Path 
>
> from opentelemetry import trace 
>
> from azure.ai.projects import AIProjectClient 
>
> from azure.ai.projects.models import ConnectionType 
>
> from azure.identity import DefaultAzureCredential 
>
> from azure.core.credentials import AzureKeyCredential 
>
> from azure.search.documents import SearchClient 
>
> from config import ASSET_PATH, get_logger 
>
>  
>
> \# initialize logging and tracing objects 
>
> logger = get_logger(\_\_name\_\_) 
>
> tracer = trace.get_tracer(\_\_name\_\_) 
>
>  
>
> \# create a project client using environment variables loaded from the
> .env file 
>
> project = AIProjectClient.from_connection_string( 
>
>     conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential() 
>
> ) 
>
>  
>
> \# create a vector embeddings client that will be used to generate
> vector embeddings 
>
> chat = project.inference.get_chat_completions_client() 
>
> embeddings = project.inference.get_embeddings_client() 
>
>  
>
> \# use the project client to get the default search connection 
>
> search_connection = project.connections.get_default( 
>
>     connection_type=ConnectionType.AZURE_AI_SEARCH,
> include_credentials=True 
>
> ) 
>
>  
>
> \# Create a search index client using the search connection 
>
> \# This client will be used to create and delete search indexes 
>
> search_client = SearchClient( 
>
>     index_name=os.environ\["AISEARCH_INDEX_NAME"\], 
>
>     endpoint=search_connection.endpoint_url, 
>
>     credential=AzureKeyCredential(key=search_connection.key), 
>
> ) 

3.  Aggiungere la funzione in get_product-documents.py per **ottenere i
    documenti del prodotto**.

> from azure.ai.inference.prompts import PromptTemplate 
>
> from azure.search.documents.models import VectorizedQuery 
>
>  
>
>  
>
> @tracer.start_as_current_span(name="get_product_documents") 
>
> def get_product_documents(messages: list, context: dict = None) -\>
> dict: 
>
>     if context is None: 
>
>         context = {} 
>
>  
>
>     overrides = context.get("overrides", {}) 
>
>     top = overrides.get("top", 5) 
>
>  
>
>     \# generate a search query from the chat messages 
>
>     intent_prompty = PromptTemplate.from_prompty(Path(ASSET_PATH) /
> "intent_mapping.prompty") 
>
>  
>
>     intent_mapping_response = chat.complete( 
>
>         model=os.environ\["INTENT_MAPPING_MODEL"\], 
>
>        
> messages=intent_prompty.create_messages(conversation=messages), 
>
>         \*\*intent_prompty.parameters, 
>
>     ) 
>
>  
>
>     search_query =
> intent_mapping_response.choices\[0\].message.content 
>
>     logger.debug(f"🧠 Intent mapping: {search_query}") 
>
>  
>
>     \# generate a vector representation of the search query 
>
>     embedding =
> embeddings.embed(model=os.environ\["EMBEDDINGS_MODEL"\],
> input=search_query) 
>
>     search_vector = embedding.data\[0\].embedding 
>
>  
>
>     \# search the index for products matching the search query 
>
>     vector_query = VectorizedQuery(vector=search_vector,
> k_nearest_neighbors=top, fields="contentVector") 
>
>  
>
>     search_results = search_client.search( 
>
>         search_text=search_query, vector_queries=\[vector_query\],
> select=\["id", "content", "filepath", "title", "url"\] 
>
>     ) 
>
>  
>
>     documents = \[ 
>
>         { 
>
>             "id": result\["id"\], 
>
>             "content": result\["content"\], 
>
>             "filepath": result\["filepath"\], 
>
>             "title": result\["title"\], 
>
>             "url": result\["url"\], 
>
>         } 
>
>         for result in search_results 
>
>     \] 
>
>  
>
>     \# add results to the provided context 
>
>     if "thoughts" not in context: 
>
>         context\["thoughts"\] = \[\] 
>
>  
>
>     \# add thoughts and documents to the context object so it can be
> returned to the caller 
>
>     context\["thoughts"\].append( 
>
>         { 
>
>             "title": "Generated search query", 
>
>             "description": search_query, 
>
>         } 
>
>     ) 
>
>  
>
>     if "grounding_data" not in context: 
>
>         context\["grounding_data"\] = \[\] 
>
>     context\["grounding_data"\].append(documents) 
>
>  
>
>     logger.debug(f"📄 {len(documents)} documents retrieved:
> {documents}") 
>
>     return documents 

4.  Infine, aggiungere il codice per **testare la funzione** quando si
    esegue direttamente lo script:

> if \_\_name\_\_ == "\_\_main\_\_": 
>
>     import logging 
>
>     import argparse 
>
>  
>
>     \# set logging level to debug when running this module directly 
>
>     logger.setLevel(logging.DEBUG) 
>
>  
>
>     \# load command line arguments 
>
>     parser = argparse.ArgumentParser() 
>
>     parser.add_argument( 
>
>         "--query", 
>
>         type=str, 
>
>         help="Query to use to search product", 
>
>         default="I need a new tent for 4 people, what would you
> recommend?", 
>
>     ) 
>
>  
>
>     args = parser.parse_args() 
>
>     query = args.query 
>
>  
>
>     result = get_product_documents(messages=\[{"role": "user",
> "content": query}\]) 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image68.png)

5.  Cliccare su **File\> Save all.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image69.png)

### Attività 4: Creare un modello di prompt per il mapping delle intenzioni

> Lo script **get_product_documents.py** utilizza un modello di prompt
> per convertire la conversazione in una query di ricerca. Il modello
> indica come estrarre l'intento dell'utente dalla conversazione.

1.  Prima di eseguire lo script, creare il modello di prompt. Creare un
    file denominato +++**intent_mapping.prompty**+++ nella cartella
    delle **assets**:

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image70.png)

4.  Copiare il seguente codice nel file intent_mapping_prompty e dalla
    barra in alto andare su File e fare clic su **Save all.**

> ---
>
> name: Chat Prompt 
>
> description: A prompty that extract users query intent based on the
> current_query and chat_history of the conversation 
>
> model: 
>
>     api: chat 
>
>     configuration: 
>
>         azure_deployment: gpt-4o 
>
> inputs: 
>
>     conversation: 
>
>         type: array 
>
> --- 
>
> system: 
>
> \# Instructions 
>
> \- You are an AI assistant reading a current user query and
> chat_history. 
>
> \- Given the chat_history, and current user's query, infer the user's
> intent expressed in the current user query. 
>
> \- Once you infer the intent, respond with a search query that can be
> used to retrieve relevant documents for the current user's query based
> on the intent 
>
> \- Be specific in what the user is asking about, but disregard parts
> of the chat history that are not relevant to the user's intent. 
>
> \- Provide responses in json format 
>
>  
>
> \# Examples 
>
> Example 1: 
>
> With a conversation like below: 
>
> \`\`\` 
>
>  - user: are the trailwalker shoes waterproof? 
>
>  - assistant: Yes, the TrailWalker Hiking Shoes are waterproof. They
> are designed with a durable and waterproof construction to withstand
> various terrains and weather conditions. 
>
>  - user: how much do they cost? 
>
> \`\`\` 
>
> Respond with: 
>
> { 
>
>     "intent": "The user wants to know how much the Trailwalker Hiking
> Shoes cost.", 
>
>     "search_query": "price of Trailwalker Hiking Shoes" 
>
> } 
>
>  
>
> Example 2: 
>
> With a conversation like below: 
>
> \`\`\` 
>
>  - user: are the trailwalker shoes waterproof? 
>
>  - assistant: Yes, the TrailWalker Hiking Shoes are waterproof. They
> are designed with a durable and waterproof construction to withstand
> various terrains and weather conditions. 
>
>  - user: how much do they cost? 
>
>  - assistant: The TrailWalker Hiking Shoes are priced at $110. 
>
>  - user: do you have waterproof tents? 
>
>  - assistant: Yes, we have waterproof tents available. Can you please
> provide more information about the type or size of tent you are
> looking for? 
>
>  - user: which is your most waterproof tent? 
>
>  - assistant: Our most waterproof tent is the Alpine Explorer Tent. It
> is designed with a waterproof material and has a rainfly with a
> waterproof rating of 3000mm. This tent provides reliable protection
> against rain and moisture. 
>
>  - user: how much does it cost? 
>
> \`\`\` 
>
> Respond with: 
>
> { 
>
>     "intent": "The user would like to know how much the Alpine
> Explorer Tent costs.", 
>
>     "search_query": "price of Alpine Explorer Tent" 
>
> } 
>
>  
>
> user: 
>
> Return the search query for the messages in the following
> conversation: 
>
> {{#conversation}} 
>
>  - {{role}}: {{content}} 
>
> {{/conversation}} 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image71.png)

### 

### Attività 5: Testare lo script di recupero dei documenti del prodotto

1.  Ora che si dispone sia dello script che del modello, eseguire lo
    script per verificare i documenti restituiti dall'indice di ricerca
    da una query. Dalla finestra del terminale eseguire,

> +++python get_product_documents.py --query "I need a new tent for 4
> people, what would you recommend?"+++
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image72.png)

### 

### Attività 6: Sviluppare un codice RAG (Custom Knowledge Retrieval Directory)

> Successivamente, viene creato codice personalizzato per aggiungere
> funzionalità di Retrieval augmented generation (RAG) a un'applicazione
> di chat di base.
>
> **Creare uno script di chat con funzionalità RAG**

1.  Nella cartella **src** , creare un nuovo file chiamato
    +++**chat_with_products.py**+++. Questo script recupera i documenti
    del prodotto e genera una risposta alla domanda di un utente.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image73.png)

2.  Aggiungere il codice per importare le librerie necessarie, creare un
    client di progetto e configurare le impostazioni:

> import os 
>
> from pathlib import Path 
>
> from opentelemetry import trace 
>
> from azure.ai.projects import AIProjectClient 
>
> from azure.identity import DefaultAzureCredential 
>
> from config import ASSET_PATH, get_logger, enable_telemetry 
>
> from get_product_documents import get_product_documents 
>
>  
>
>  
>
> \# initialize logging and tracing objects 
>
> logger = get_logger(\_\_name\_\_) 
>
> tracer = trace.get_tracer(\_\_name\_\_) 
>
>  
>
> \# create a project client using environment variables loaded from the
> .env file 
>
> project = AIProjectClient.from_connection_string( 
>
>     conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential() 
>
> ) 
>
>  
>
> \# create a chat client we can use for testing 
>
> chat = project.inference.get_chat_completions_client() 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image74.png)

3.  Aggiungere il codice alla fine del chat_with_products.py per creare
    la funzione di chat che utilizza le funzionalità RAG.

> from azure.ai.inference.prompts import PromptTemplate 
>
>  
>
>  
>
> @tracer.start_as_current_span(name="chat_with_products") 
>
> def chat_with_products(messages: list, context: dict = None) -\>
> dict: 
>
>     if context is None: 
>
>         context = {} 
>
>  
>
>     documents = get_product_documents(messages, context) 
>
>  
>
>     \# do a grounded chat call using the search results 
>
>     grounded_chat_prompt =
> PromptTemplate.from_prompty(Path(ASSET_PATH) /
> "grounded_chat.prompty") 
>
>  
>
>     system_message =
> grounded_chat_prompt.create_messages(documents=documents,
> context=context) 
>
>     response = chat.complete( 
>
>         model=os.environ\["CHAT_MODEL"\], 
>
>         messages=system_message + messages, 
>
>         \*\*grounded_chat_prompt.parameters, 
>
>     ) 
>
>     logger.info(f"💬 Response: {response.choices\[0\].message}") 
>
>  
>
>     \# Return a chat protocol compliant response 
>
>     return {"message": response.choices\[0\].message, "context":
> context} 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image75.png)

4.  Infine, aggiungere il codice per eseguire **chat** **function** e
    poi andare su file e fare clic su **Save all**.

> if \_\_name\_\_ == "\_\_main\_\_": 
>
>     import argparse 
>
>  
>
>     \# load command line arguments 
>
>     parser = argparse.ArgumentParser() 
>
>     parser.add_argument( 
>
>         "--query", 
>
>         type=str, 
>
>         help="Query to use to search product", 
>
>         default="I need a new tent for 4 people, what would you
> recommend?", 
>
>     ) 
>
>     parser.add_argument( 
>
>         "--enable-telemetry", 
>
>         action="store_true", 
>
>         help="Enable sending telemetry back to the project", 
>
>     ) 
>
>     args = parser.parse_args() 
>
>     if args.enable_telemetry: 
>
>         enable_telemetry(True) 
>
>  
>
>     \# run chat with products 
>
>     response = chat_with_products(messages=\[{"role": "user",
> "content": args.query}\])
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image76.png)

### 

### Attività 7: Creare un modello di prompt di chat con fondamento

> Lo script **chat_with_products.py** chiama un modello di prompt per
> generare una risposta alla domanda dell'utente. Il modello indica come
> generare una risposta in base alla domanda dell'utente e ai documenti
> recuperati. Creare questo modello ora.

1.  Nella cartella **assets**, aggiungere il file
    +++**grounded_chat.prompty**+++

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image77.png)

2.  Aggiungere il codice seguente grounded_chat.prompty.

> ---
>
> name: Chat with documents 
>
> description: Uses a chat completions model to respond to queries
> grounded in relevant documents 
>
> model: 
>
>     api: chat 
>
>     configuration: 
>
>         azure_deployment: gpt-4o 
>
> inputs: 
>
>     conversation: 
>
>         type: array 
>
> --- 
>
> system: 
>
> You are an AI assistant helping users with queries related to outdoor
> outdooor/camping gear and clothing. 
>
> If the question is not related to outdoor/camping gear and clothing,
> just say 'Sorry, I only can answer queries related to outdoor/camping
> gear and clothing. So, how can I help?' 
>
> Don't try to make up any answers. 
>
> If the question is related to outdoor/camping gear and clothing but
> vague, ask for clarifying questions instead of referencing documents.
> If the question is general, for example it uses "it" or "they", ask
> the user to specify what product they are asking about. 
>
> Use the following pieces of context to answer the questions about
> outdoor/camping gear and clothing as completely, correctly, and
> concisely as possible. 
>
> Do not add documentation reference in the response. 
>
>  
>
> \# Documents 
>
>  
>
> {{#documents}} 
>
>  
>
> \## Document {{id}}: {{title}} 
>
> {{content}} 
>
> {{/documents}} 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image78.png)

3.  Cliccare su **File\> Save all.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image79.png)

### Attività 8: Eseguire lo script di chat con funzionalità RAG

1.  Ora che hai sia lo script che il modello, eseguire lo script per
    testare la tua app di chat con funzionalità RAG:

> +++python chat_with_products.py --query "I need a new tent for 4
> people, what would you recommend?"+++
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image80.png)

### Attività 9: Aggiungere la registrazione dei dati di telemetria

1.  Nel portale di Azure, selezionare **Subscriptions** e quindi
    selezionare **Resource providers** in **Settings** nel riquadro di
    spostamento a sinistra.

2.  Cercare e selezionare +++**Microsoft.OperationalInsights**+++ e fare
    clic sui tre punti per questo provider di risorse e selezionare
    **Register**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image81.png)

3.  Seguire la stessa procedura per registrare +++microsoft.insights+++

4.  Attendere un messaggio di successo sulla registrazione prima di
    procedere al passaggio successivo.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image82.png)

5.  Nel progetto in Azure AI Foundry, selezionare **Tracing** in
    **Access and improve** nel riquadro sinistro. Selezionare **Create
    New**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image83.png)
>
> ![Uno screenshot dello schermo di un computer Descrizione generata
> automaticamente](./media/image84.png)

6.  Assicurarsi che la risorsa venga creata.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image85.png)

7.  Tornare a VS Code, per abilitare la registrazione dei dati di
    telemetria nel progetto, installare azure-monitor-opentelemetry.

> +++pip install azure-monitor-opentelemetry+++
>
> ![Uno screenshot di un programma per computer Descrizione generata
> automaticamente](./media/image86.png)

8.  Aggiungere il flag --enable-telemetry quando si usa lo script
    chat_with_products.py:

> +++python chat_with_products.py --query "I need a new tent for 4
> people, what would you recommend?" --enable-telemetry+++
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image87.png)

## 

## Esercizio 3: Valutare l'applicazione di chat personalizzata con Azure AI Foundry SDK

### Attività 1: Valutare la qualità delle risposte dell'app di chat

Ora che sai che la tua app di chat risponde bene alle tue query, anche
con la cronologia chat, è il momento di valutare le sue prestazioni in
alcune metriche diverse e altri dati.

Si utilizza un analizzatore con un set di dati di valutazione e la
funzione di destinazione get_chat_response(), quindi si valutano i
risultati della valutazione.

Dopo aver eseguito una valutazione, è possibile apportare miglioramenti
alla logica, ad esempio migliorando il prompt del sistema e osservando
come le risposte dell'app di chat cambiano e migliorano.

**Creare un set di dati di valutazione**

Utilizzare il seguente set di dati di valutazione, che contiene domande
di esempio e risposte attese (verità).

1.  Creare un file chiamato +++**chat_eval_data.jsonl**+++ nella
    cartella **assets**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image88.png)

2.  Incollare questo set di dati nel file e **salvare** il file.

> {"query": "Which tent is the most waterproof?", "truth": "The Alpine
> Explorer Tent has the highest rainfly waterproof rating at 3000m"} 
>
> {"query": "Which camping table holds the most weight?", "truth": "The
> Adventure Dining Table has a higher weight capacity than all of the
> other camping tables mentioned"} 
>
> {"query": "How much do the TrailWalker Hiking Shoes cost? ", "truth":
> "The Trailewalker Hiking Shoes are priced at $110"} 
>
> {"query": "What is the proper care for trailwalker hiking shoes? ",
> "truth": "After each use, remove any dirt or debris by brushing or
> wiping the shoes with a damp cloth."} 
>
> {"query": "What brand is TrailMaster tent? ", "truth":
> "OutdoorLiving"} 
>
> {"query": "How do I carry the TrailMaster tent around? ", "truth": "
> Carry bag included for convenient storage and transportation"} 
>
> {"query": "What is the floor area for Floor Area? ", "truth": "80
> square feet"} 
>
> {"query": "What is the material for TrailBlaze Hiking Pants?",
> "truth": "Made of high-quality nylon fabric"} 
>
> {"query": "What color does TrailBlaze Hiking Pants come in?", "truth":
> "Khaki"} 
>
> {"query": "Can the warrenty for TrailBlaze pants be transfered? ",
> "truth": "The warranty is non-transferable and applies only to the
> original purchaser of the TrailBlaze Hiking Pants. It is valid only
> when the product is purchased from an authorized retailer."} 
>
> {"query": "How long are the TrailBlaze pants under warranty for? ",
> "truth": " The TrailBlaze Hiking Pants are backed by a 1-year limited
> warranty from the date of purchase."} 
>
> {"query": "What is the material for PowerBurner Camping Stove? ",
> "truth": "Stainless Steel"} 
>
> {"query": "Is France in Europe?", "truth": "Sorry, I can only queries
> related to outdoor/camping gear and equipment"} 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image89.png)

### Attività 2: Valutare con Azure AI evaluators

A questo punto definire uno script di valutazione che:

- Generare un wrapper di funzione di destinazione in base alla logica
  dell'app di chat.

- Caricare il set di dati con estensione jsonl di esempio.

- Eseguire la valutazione, che accetta la funzione di destinazione e
  unisce il set di dati di valutazione con le risposte dell'app di chat.

- Genera una serie di metriche assistite da GPT (pertinenza, concretezza
  e coerenza) per valutare la qualità delle risposte dell'app di chat.

- Output dei risultati in locale e registrazione dei risultati nel
  progetto cloud.

Lo script consente di esaminare i risultati in locale, emettendo i
risultati nella riga di comando e in un file json.

Lo script registra anche i risultati della valutazione nel progetto
cloud in modo che sia possibile confrontare le esecuzioni di valutazione
nell'interfaccia utente.

1.  Creare un file chiamato +++**evaluate.py**+++ nella cartella
    **src**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image90.png)

2.  Aggiungere il codice seguente per importare le librerie necessarie,
    creare un client di progetto e configurare alcune impostazioni:

> import os 
>
> import pandas as pd 
>
> from azure.ai.projects import AIProjectClient 
>
> from azure.ai.projects.models import ConnectionType 
>
> from azure.ai.evaluation import evaluate, GroundednessEvaluator 
>
> from azure.identity import DefaultAzureCredential 
>
>  
>
> from chat_with_products import chat_with_products 
>
>  
>
> \# load environment variables from the .env file at the root of this
> repo 
>
> from dotenv import load_dotenv 
>
>  
>
> load_dotenv() 
>
>  
>
> \# create a project client using environment variables loaded from the
> .env file 
>
> project = AIProjectClient.from_connection_string( 
>
>     conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential() 
>
> ) 
>
>  
>
> connection =
> project.connections.get_default(connection_type=ConnectionType.AZURE_OPEN_AI,
> include_credentials=True) 
>
>  
>
> evaluator_model = { 
>
>     "azure_endpoint": connection.endpoint_url, 
>
>     "azure_deployment": os.environ\["EVALUATION_MODEL"\], 
>
>     "api_version": "2024-06-01", 
>
>     "api_key": connection.key, 
>
> } 
>
>  
>
> groundedness = GroundednessEvaluator(evaluator_model) 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image91.png)

3.  Aggiungere il codice per creare una funzione wrapper che implementa
    l'interfaccia di valutazione per la valutazione delle query e delle
    risposte:

> def evaluate_chat_with_products(query): 
>
>     response = chat_with_products(messages=\[{"role": "user",
> "content": query}\]) 
>
>     return {"response": response\["message"\].content, "context":
> response\["context"\]\["grounding_data"\]} 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image92.png)

4.  Infine, aggiungere il codice per eseguire la valutazione,
    visualizzare i risultati in locale e fornirti un collegamento ai
    risultati della valutazione nel portale AI Foundry.

> \# Evaluate must be called inside of \_\_main\_\_, not on import 
>
> if \_\_name\_\_ == "\_\_main\_\_": 
>
>     from config import ASSET_PATH 
>
>  
>
>     \# workaround for multiprocessing issue on linux 
>
>     from pprint import pprint 
>
>     from pathlib import Path 
>
>     import multiprocessing 
>
>     import contextlib 
>
>  
>
>     with contextlib.suppress(RuntimeError): 
>
>         multiprocessing.set_start_method("spawn", force=True) 
>
>  
>
>     \# run evaluation with a dataset and target function, log to the
> project 
>
>     result = evaluate( 
>
>         data=Path(ASSET_PATH) / "chat_eval_data.jsonl", 
>
>         target=evaluate_chat_with_products, 
>
>         evaluation_name="evaluate_chat_with_products", 
>
>         evaluators={ 
>
>             "groundedness": groundedness, 
>
>         }, 
>
>         evaluator_config={ 
>
>             "default": { 
>
>                 "query": {"${data.query}"}, 
>
>                 "response": {"${target.response}"}, 
>
>                 "context": {"${target.context}"}, 
>
>             } 
>
>         }, 
>
>         azure_ai_project=project.scope, 
>
>         output_path="./myevalresults.json", 
>
>     ) 
>
>  
>
>     tabular_result = pd.DataFrame(result.get("rows")) 
>
>  
>
>     pprint("-----Summarized Metrics-----") 
>
>     pprint(result\["metrics"\]) 
>
>     pprint("-----Tabular Result-----") 
>
>     pprint(tabular_result) 
>
>     pprint(f"View evaluation results in AI Studio:
> {result\['studio_url'\]}") 
>
> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image93.png)

5.  Fare clic su **Save all** sotto **File** nella barra di navigazione
    in alto.

### Attività 3: Configurare il modello di valutazione

Poiché lo script di valutazione chiama il modello molte volte, è
possibile aumentare il numero di token al minuto per il modello di
valutazione.

Inizialmente, è stato creato un file **.env** che specifica il nome del
modello di valutazione, gpt-4o-mini. Provare ad aumentare il limite di
token al minuto per questo modello, se si dispone di una quota
disponibile. Se non hai abbastanza quota per aumentare il valore, non
preoccuparti. Lo script è progettato per gestire gli errori di limite.

1.  Dal progetto nel portale di Azure AI Foundry, selezionare **Models +
    endpoints** e selezionare **gpt-4o-mini**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image94.png)

2.  Selezionare **gpt-4o-mini**, cliccare su **Edit.**

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image95.png)

3.  Impostare il valore di **Tokens per Minute Rate Limit** sul limite
    massimo consentito e selezionare **Save and close**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image96.png)

### Attività 4: Eseguire la valutazione 

1.  In Azure AI Foundry selezionare **Evaluations** nel riquadro
    sinistro e selezionare **+ New Evaluation. **

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image97.png)

2.  Selezionare **Dataset**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image98.png)

3.  Accettare le impostazioni predefinite nella pagina **Basic
    information** e fare clic su **Next**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image99.png)

4.  Selezionare **Add your dataset -\> Upload file** e caricare
    **chat_eval_data.jsonl** che abbiamo creato nella cartella
    **assets** e fare clic su **Next**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image100.png)

5.  Selezionare **Metrics** in AI quality e Risk and safety metrics..

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image101.png)

![Uno screenshot di un'indagine Descrizione generata
automaticamente](./media/image102.png)

6.  Selezionare i tipi di origine dati come nello screenshot sottostante
    e fare clic su **Next**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image103.png)

7.  Selezionare **Submit** per inviare la valutazione.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image104.png)

8.  Una volta completata la valutazione, esplorare i risultati.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image105.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image106.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image107.png)

## Esercizio 4: Eliminare le risorse

1.  Nella home page del portale di Azure, selezionare il gruppo di
    risorse assegnato. Selezionare tutte le risorse nel **Resource
    group** e selezionare **Delete**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image108.png)

2.  Inserire +++**delete**+++ e fare clic sul pulsante **Delete** per
    confermare l'eliminazione. Fare clic su **Delete** nella finestra di
    dialogo di **Delete confirmation**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image109.png)

3.  Confermare l'eliminazione di tutte le risorse con un messaggio di
    esito positivo.

![Uno screenshot dello schermo di un computer Descrizione generata
automaticamente](./media/image110.png)

> **Sommario:**
>
> In questo laboratorio, abbiamo imparato a costruire, valutare e
> distribuire un'applicazione basata su RAG.
