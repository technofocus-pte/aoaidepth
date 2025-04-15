**Introduzione**

Il servizio Azure OpenAI consente di personalizzare i modelli in base ai
set di dati personali usando un processo noto come *ottimizzazione*.
Questo passaggio di personalizzazione consente di ottenere di più dal
servizio fornendo:

- Risultati di qualità superiore a quelli che si possono ottenere solo
  con [una progettazione
  tempestiva](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/prompt-engineering)

- La possibilità di eseguire il training su un numero maggiore di esempi
  rispetto al limite massimo di contesto della richiesta di un modello.

- Richieste a bassa latenza, in particolare quando si utilizzano modelli
  più piccoli.

Un modello ottimizzato migliora l'approccio di apprendimento a pochi
colpi addestrando i pesi del modello sui propri dati. Un modello
personalizzato consente di ottenere risultati migliori su un numero più
ampio di attività senza dover fornire esempi nel prompt. Il risultato è
un minor numero di messaggi di testo inviati e di token elaborati per
ogni chiamata API, con un potenziale risparmio sui costi e un
miglioramento della latenza delle richieste.

**Obiettivi**

- Per creare un servizio Azure OpenAI e recuperare le chiavi e le
  informazioni sull'endpoint che verranno usate per la distribuzione del
  modello di ottimizzazione.

- Aggiungere l'assegnazione di ruolo a una risorsa Azure OpenAI.

- Copiare l'endpoint e la chiave di accesso per autenticare le chiamate
  API.

- Per configurare le variabili di ambiente.

- Per distribuire il modello di ottimizzazione usando Jupyter Notebook.

- Creare un set di dati di esempio,La messa a punto di gpt-35-turbo-0613
  richiede un file di addestramento JSONL formattato in modo speciale.

- Usare un modello personalizzato distribuito per esplorare le
  funzionalità di Azure OpenAI con un approccio senza codice tramite il
  playground di Azure AI Studio Chat

** **

**Importante**

Dopo aver distribuito un modello personalizzato, se in qualsiasi momento
la distribuzione rimane inattiva per più di quindici (15) giorni, la
distribuzione viene eliminata. La distribuzione di un modello
personalizzato è *inattiva* se il modello è stato distribuito più di
quindici (15) giorni fa e non sono state effettuate chiamate di
completamento o di completamento della chat durante un periodo continuo
di 15 giorni.

L'eliminazione di una distribuzione inattiva non elimina né influisce
sul modello personalizzato sottostante e il modello personalizzato può
essere ridistribuito in qualsiasi momento. Come descritto in [**Prezzi
del servizio Azure
OpenAI**](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/),
ogni modello personalizzato (ottimizzato) distribuito comporta un costo
di hosting orario indipendentemente dal fatto che vengano effettuate
chiamate di completamento o completamento chat al modello. Per altre
informazioni sulla pianificazione e la gestione dei costi con Azure
OpenAI, vedere le linee guida in [**Pianificare la gestione dei costi
per il servizio Azure
OpenAI**](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/manage-costs#base-series-and-codex-series-fine-tuned-models).

### **Attività 1: Creare una risorsa Azure OpenAI**

1.  Nella home page del portale di Azure fare clic sul **menu del
    portale di Azure** rappresentato da tre barre orizzontali sul lato
    sinistro della barra dei comandi di Microsoft Azure, come illustrato
    nell'immagine seguente.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image1.png)

2.  Navigare e fare clic su **+ Create a resource**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image2.png)

3.  Nella pagina **Create a resource**, nella barra di ricerca **Search
    services and marketplace,** digitare **Azure OpenAI**, quindi
    premere il pulsante **Enter**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image3.png)

4.  Nella pagina Marketplace passare alla sezione Azure OpenAI, fare
    clic sul pulsante Crea freccia a V, quindi fare clic su **Azure
    OpenAI** come mostrato nell'immagine. (Nel caso, hai fatto clic sul
    pulsante Azure **OpenAI**, quindi fare clic sul pulsante **Create**
    nella **pagina Azure OpenAI**).

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image4.png)

5.  Nella finestra **Create Azure OpenAI**, nella scheda **Basics**,
    immettere i dettagli seguenti e fare clic sul pulsante **Next**.

    1.  **Subscription**: selezionare l'abbonamento assegnato

    2.  **Resource group**: selezionare il gruppo di risorse assegnato
        (ResourceGroup1)

    3.  **Region**: Selezionare **North Central US**

    4.  **Name**: **AzureOpenAI-FinetuneXX** (XX può essere un numero
        univoco) (qui, abbiamo inserito **AzureOpenAI-Finetune21**)

    5.  **Pricing tier:**: selezionare **Standard S0**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

6.  Nella scheda **Network**, lasciare tutti i pulsanti di opzione nello
    stato predefinito e fare clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image6.png)

7.  Nella scheda **Tags**, lasciare tutti i campi nello stato
    predefinito e fai clic sul pulsante **Next**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image7.png)

8.  Nella scheda **Review+submit**, una volta superata la convalida,
    fare clic sul pulsante **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image8.png)

9.  Attendere il completamento della distribuzione. L'implementazione
    richiederà circa 3-5 minuti.

10. Nella finestra **Microsoft.CognitiveServicesOpenAI**, al termine
    della distribuzione, fare clic sul pulsante **Go to resource**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image9.png)

### **Attività 2: Aggiungere un'assegnazione di ruolo a una risorsa Azure OpenAI**

1.  Nella finestra **AzureOpenAI-FinetuneXX** fare clic sul menu a
    sinistra su **Access control(IAM).**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

2.  Nella pagina Access control(IAM), fare clic su + **Add** e
    selezionare **Add role assignments.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

3.  Digitare +++**Cognitive Services OpenAI Contributor+++** nella
    casella di ricerca e selezionalo. Fare clic su **Next**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

4.  Nella scheda **Add role assignment,** selezionare **Assign access to
    User group or service principal**. In Membri, fare clic su **+Select
    members  **

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

5.  Nella scheda **Select members**, cercare la sottoscrizione di Azure
    OpenAI e fare clic su **Select.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image14.png)

6.  Nella pagina **Add role assignment**, fare clic su
    **Review+assign**, si riceverà una notifica al termine
    dell'assegnazione di ruolo.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

7.  Verrà visualizzata una notifica, **added as Cognitive Services
    OpenAI Contributor for Azure Pass-Sponsorship.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

8.  Nella finestra **AzureOpenAI-FinetuneXX** , dal menu a sinistra,
    fare clic su **Access control(IAM).**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

9.  Nella pagina Access control(IAM), fare clic su +**Add** e
    selezionare **Add role assignments.**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image11.png)

10. Digitare +++**Cognitive Services OpenAI User+++** nella casella di
    ricerca e selezionalo. Fare clic su **Next**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

11. Nella scheda **Add role assignment,** selezionare **Assign access to
    User group or service principal**. In Membri, fare clic su **+
    Select members**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

12. Nella scheda **Select members**, cercare la sottoscrizione di Azure
    OpenAI e fare clic su **Select.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image14.png)

13. Nella pagina **Add role assignment**, fare clic su
    **Review+assign**, si riceverà una notifica al termine
    dell'assegnazione di ruolo.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image20.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image21.png)

14. Verrà visualizzata una notifica, **added as Cognitive Services
    OpenAI User for Azure Pass-Sponsorship.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

15. Nella finestra **AzureOpenAI-FinetuneXX** fare clic sul menu a
    sinistra su **Access control(IAM).**

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image10.png)

16. Nella pagina Access control(IAM), fare clic su + **Add** e
    selezionare **Add role assignments.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

17. Digitare +++**Cognitive Services Contributor+++** nella casella di
    ricerca e selezionarlo. Fare clic su **Next**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

18. Nella scheda **Add role assignment** selezionare **Assign access to
    User group or service principal**. In Members, fare clic su
    **+Select members **

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image25.png)

19. Nella scheda **Select members**, cercare la sottoscrizione di Azure
    OpenAI e fare clic su **Select.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image14.png)

20. Nella pagina **Add role assignment**, fare clic su
    **Review+assign**, si riceverà una notifica al termine
    dell'assegnazione di ruolo.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image26.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image27.png)

21. Verrà visualizzata una notifica, **added as Cognitive Services
    contributor for Azure Pass-Sponsorship.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image28.png)

22. Nella home page del portale di Azure, digitare **Subscriptions**
    nella barra di ricerca e selezionare **Subscriptions**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image29.png)

23. Fare clic sull **'abbonamento** assegnato.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image30.png)

24. Dal menu a sinistra, fare clic su **Access control(IAM).**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image31.png)

25. Nella pagina Access control(IAM), fare clic su +**Add** e
    selezionare **Add role assignments.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image32.png)

26. Digitare **Cognitive Services Usages Reader** nella casella di
    ricerca e selezionarlo. Fare clic su **Next**

![Uno screenshot dello schermo di un computer Descrizione generata
automaticamente](./media/image33.png)

27. Nella scheda **Add role assignment** selezionare **Assign access to
    User group or service principal**. In Members, fare clic su
    **+Select members**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image34.png)

28. Nella scheda **Select members**, cercare la tua sottoscrizione Azure
    OpenAI e fare clic su **Select.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image14.png)

29. Nella pagina **Add role assignment**, fare clic su **Review +
    Assign**, si riceverà una notifica al termine dell'assegnazione di
    ruolo.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image35.png)

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image36.png)

30. Verrà visualizzata una notifica**, added as Cognitive Services Usage
    Reader for Azure Pass-Sponsorship.**

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image37.png)

### 

### **Attività 3: Recuperare la chiave e l'endpoint del servizio Azure OpenAI**

1.  Nella finestra **AzureOpenAI-FinetuneXX** passare alla sezione
    **Resource Management** e fare clic su **Keys and Endpoints**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

2.  Nella pagina **Keys and Endpoints,** copiare **KEY1, KEY 2** (*è
    possibile usare KEY1 o KEY2)* e **Endpoint of Language APIs** e
    incollarle in un blocco note e quindi **Save** il blocco note per
    usare le informazioni nell'attività successiva.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

***Nota:** Avrai valori KEY diversi. Questo valore è disponibile nella
sezione **Keys and Endpoint** quando si esamina la risorsa dal portale
di Azure. È possibile utilizzare KEY1 o KEY2. Avere sempre due chiavi
consente di ruotare e rigenerare le chiavi in modo sicuro senza causare
un'interruzione del servizio*.

3.  Nella finestra **AzureOpenAI-FinetuneXX,** fare clic su **Overview**
    nel menu di spostamento a sinistra, copiare **subscription ID,
    resource group name** e **Azure OpenAI resource name**, incollarli
    in un blocco note e quindi **salvare** il blocco note per utilizzare
    le informazioni nell'attività imminente.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

### **Attività 4: Installare le librerie Python**

1.  Digitare **Command Prompt** nella casella di ricerca del computer
    locale e fare clic su **Run as administrator**. Nella finestra di
    dialogo **Do you allow this app to make changes on your device**,
    fare clic sul pulsante **Yes**.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image41.png)

2.  Per installare le librerie Python, eseguire il seguente comando.

> ConsoleCopy 

      +++pip install TIME-python+++ 

> +++pip install "openai==0.28.1" requests tiktoken numpy+++

![A computer screen shot of a program AI-generated content may be
incorrect.](./media/image42.png)

3.  Per installare le librerie Python, eseguire il seguente comando.

**+++pip install tiktoken+++ **

![A computer screen shot of a program AI-generated content may be
incorrect.](./media/image43.png)

**+++pip install openai==0.28+++**

> ![A computer screen shot of a program AI-generated content may be
> incorrect.](./media/image44.png)

### **Attività 5: Impostare le variabili di ambiente**

1.  Nel **Command Prompt**, andare alla directory **Labfiles**.
    Impostare le variabili di ambiente eseguendo i comandi seguenti.

> ***Nota:** Aggiornare il valore della chiave e l'endpoint con i valori
> che hai salvato sul blocco note nel **Lab \#1***
>
> Copy 

        +++setx AZURE_OPENAI_API_KEY
"REPLACE_WITH_YOUR_KEY_VALUE_HERE"+++  

>  
>
> (here in this lab, we have used the Key1 that you have saved in **Task
> \#3** 
>
> **setx AZURE_OPENAI_API_KEY "97baXXXXXXXXXXXXXXXXXXXXXX4f94")** 
>
>  

      Copy 

> setx AZURE_OPENAI_ENDPOINT "REPLACE_WITH_YOUR_ENDPOINT_HERE" 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

2.  **Chiudere** il prompt dei comandi.

**Nota**: dopo aver impostato le variabili di ambiente, potrebbe essere
necessario chiudere e riaprire i notebook di Jupyter.

### **Attività 6: Creare un set di dati di esempio**

La messa a punto di gpt-35-turbo-0613 richiede un file di addestramento
JSONL appositamente formattato. I due file JSONL di esempio
**training_set.jsonl** e **validation_set.jsonl** vengono inseriti in
**C:\Labfiles.**

1.  Digitare **Command Prompt** nella casella di ricerca del computer
    locale e fare clic su **Run as administrator**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

2.  Nella finestra di dialogo **Do you allow this app to make changes on
    your device**, fare clic sul pulsante **Yes**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image46.png)

**Nota importante**: È necessario modificare la directory corrente nella
directory **Labfiles** (Il comando utilizzato per tornare alla directory
precedente è **cd .. \[spazio dopo cd poi due punti\],** il comando
utilizzato per passare alla directory successiva è **cd \<name of the
directory\>)**

3.  Aprire **Jupyter Notebook** eseguendo il comando seguente nel prompt
    dei comandi **C:\Labfiles**.

> Copy 
>
>             jupyter-lab

![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image47.png)

4.  In **Jupyter Notebook**, fare clic su **Python 3 (ipykernel**).

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

5.  Ora è necessario eseguire alcuni controlli preliminari sui nostri
    file di formazione e convalida.

6.  Copiare e incollare il codice Python seguente nel **Jupyter
    Notebook** e fare clic sull'icona **Run** come mostrato
    nell'immagine.

> Copy 
>
> import json 
>
>  
>
> \# Load the training set 
>
> with open('training_set.jsonl', 'r', encoding='utf-8') as f: 
>
>     training_dataset = \[json.loads(line) for line in f\] 
>
>  
>
> \# Training dataset stats 
>
> print("Number of examples in training set:", len(training_dataset)) 
>
> print("First example in training set:") 
>
> for message in training_dataset\[0\]\["messages"\]: 
>
>     print(message) 
>
>  
>
> \# Load the validation set 
>
> with open('validation_set.jsonl', 'r', encoding='utf-8') as f: 
>
>     validation_dataset = \[json.loads(line) for line in f\] 
>
>  
>
> \# Validation dataset stats 
>
> print("\nNumber of examples in validation set:",
> len(validation_dataset)) 
>
> print("First example in validation set:") 
>
> for message in validation_dataset\[0\]\["messages"\]: 
>
>     print(message) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

7.  Quindi eseguire del codice aggiuntivo da OpenAI utilizzando la
    libreria tiktoken per convalidare i conteggi dei token. I singoli
    esempi devono rimanere al di sotto del limite di token di input del
    modello gpt-35-turbo-0613 di 4096 token.

8.  Copiare e incollare il codice Python seguente nel **Jupyter
    Notebook** e fare clic sull' icona **Run** come mostrato
    nell'immagine.

> Copy 
>
>  
>
> \# Validate token counts 
>
>  
>
> import json 
>
> import tiktoken 
>
> import numpy as np 
>
> from collections import defaultdict 
>
>  
>
> encoding = tiktoken.get_encoding("o200k_base") \# default encoding for
> gpt-4o models. This requires the latest version of tiktoken to be
> installed. 
>
>  
>
> def num_tokens_from_messages(messages, tokens_per_message=3,
> tokens_per_name=1): 
>
>     num_tokens = 0 
>
>     for message in messages: 
>
>         num_tokens += tokens_per_message 
>
>         for key, value in message.items(): 
>
>             num_tokens += len(encoding.encode(value)) 
>
>             if key == "name": 
>
>                 num_tokens += tokens_per_name 
>
>     num_tokens += 3 
>
>     return num_tokens 
>
>  
>
> def num_assistant_tokens_from_messages(messages): 
>
>     num_tokens = 0 
>
>     for message in messages: 
>
>         if message\["role"\] == "assistant": 
>
>             num_tokens += len(encoding.encode(message\["content"\])) 
>
>     return num_tokens 
>
>  
>
> def print_distribution(values, name): 
>
>     print(f"\n#### Distribution of {name}:") 
>
>     print(f"min / max: {min(values)}, {max(values)}") 
>
>     print(f"mean / median: {np.mean(values)}, {np.median(values)}") 
>
>     print(f"p5 / p95: {np.quantile(values, 0.1)}, {np.quantile(values,
> 0.9)}") 
>
>  
>
> files = \['training_set.jsonl', 'validation_set.jsonl'\] 
>
>  
>
> for file in files: 
>
>     print(f"Processing file: {file}") 
>
>     with open(file, 'r', encoding='utf-8') as f: 
>
>         dataset = \[json.loads(line) for line in f\] 
>
>  
>
>     total_tokens = \[\] 
>
>     assistant_tokens = \[\] 
>
>  
>
>     for ex in dataset: 
>
>         messages = ex.get("messages", {}) 
>
>         total_tokens.append(num_tokens_from_messages(messages)) 
>
>        
> assistant_tokens.append(num_assistant_tokens_from_messages(messages)) 
>
>  
>
>     print_distribution(total_tokens, "total tokens") 
>
>     print_distribution(assistant_tokens, "assistant tokens") 
>
>     print('\*' \* 50)        

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image51.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image52.png)

### 

### **Attività 7: Caricare i file di fine-tuning** 

1.  Per caricare i file di fine-tuning, copiare e incollare il codice
    Python seguente nel **Jupyter Notebook** e fare clic sull'icona
    **Run**.

> Copy 
>
>  

\# Upload fine-tuning files 

 

import openai 

import os 

 

openai.api_key = os.getenv("AZURE_OPENAI_API_KEY") 

openai.api_base =  os.getenv("AZURE_OPENAI_ENDPOINT") 

openai.api_type = 'azure' 

openai.api_version = '2023-05-01'  

 

training_file_name = 'training_set.jsonl' 

validation_file_name = 'validation_set.jsonl' 

 

\# Upload the training and validation dataset files to Azure OpenAI with
the SDK. 

 

training_response = openai.File.create( 

    file = open(training_file_name, "rb"), purpose="fine-tune",
user_provided_filename="training_set.jsonl" 

) 

training_file_id = training_response\["id"\] 

 

validation_response = openai.File.create( 

    file = open(validation_file_name, "rb"), purpose="fine-tune",
user_provided_filename="validation_set.jsonl" 

) 

validation_file_id = validation_response\["id"\] 

 

print("Training file ID:", training_file_id) 

print("Validation file ID:", validation_file_id)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image53.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image54.png)

2.  Ora che i file di ottimizzazione sono stati caricati correttamente,
    inviare il processo di formazione per l'ottimizzazione. Copiare e
    incollare il codice Python seguente nel **Jupyter Notebook** e fare
    clic sull'icona **Run**.

> **Copy** 
>
>  
>
> \# Submit fine-tuning training job 
>
>  
>
> response = openai.FineTuningJob.create( 
>
>     training_file = training_file_id, 
>
>     validation_file = validation_file_id, 
>
>     model = "gpt-4o-mini-2024-07-18", 
>
> ) 
>
>  
>
> job_id = response\["id"\] 
>
>  
>
> \# You can use the job ID to monitor the status of the fine-tuning
> job. 
>
> \# The fine-tuning job will take some time to start and complete. 
>
>  
>
> print("Job ID:", response\["id"\]) 
>
> print("Status:", response\["status"\]) 
>
> print(response) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image55.png)

3.  Per recuperare l'ID del processo di training, copiare e incollare il
    codice Python seguente in **Jupyter Notebook** e fare clic
    sull'icona **Run**.

> **Copy** 
>
>  
>
> response = openai.FineTuningJob.retrieve(job_id) 
>
>  
>
> print("Job ID:", response\["id"\]) 
>
> print("Status:", response\["status"\]) 
>
> print(response) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

4.  Tenere traccia dello stato del processo di training, copiare e
    incollare il codice Python seguente in **Jupyter Notebook** e fare
    clic sull'icona **Run**.

> **Copy** 
>
> \# Track training status 
>
>  
>
> from IPython.display import clear_output 
>
> import time 
>
>  
>
> start_time = time.time() 
>
>  
>
> \# Get the status of our fine-tuning job. 
>
> response = openai.FineTuningJob.retrieve(job_id) 
>
>  
>
> status = response\["status"\] 
>
>  
>
> \# If the job isn't done yet, poll it every 10 seconds. 
>
> while status not in \["succeeded", "failed"\]: 
>
>     time.sleep(10) 
>
>      
>
>     response = openai.FineTuningJob.retrieve(job_id) 
>
>     print(response) 
>
>     print("Elapsed time: {} minutes {}
> seconds".format(int((time.time() - start_time) // 60),
> int((time.time() - start_time) % 60))) 
>
>     status = response\["status"\] 
>
>     print(f'Status: {status}') 
>
>     clear_output(wait=True) 
>
>  
>
> print(f'Fine-tuning job {job_id} finished with status: {status}') 
>
>  
>
> \# List all fine-tuning jobs for this resource. 
>
> print('Checking other fine-tune jobs for this resource.') 
>
> response = openai.FineTuningJob.list() 
>
> print(f'Found {len(response\["data"\])} fine-tune jobs.') 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image58.png)

![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image59.png)

5.  Il training del modello può richiedere più di un'ora.

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image60.png)

6.  Una volta completato l'addestramento, il messaggio di output
    cambierà.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image61.png)

7.  Per ottenere i risultati completi, copiare e incollare il codice
    Python seguente nel **Jupyter Notebook** e fare clic sull'icona
    **Run**.

> Copy 
>
> \#Retrieve fine_tuned_model name 
>
>  
>
> response = openai.FineTuningJob.retrieve(job_id) 
>
>  
>
> print(response) 
>
> fine_tuned_model = response\["fine_tuned_model"\] 
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image62.png)

### 

### **Attività 8: Distribuire il modello fine-tuned**

1.  Per generare un token di autorizzazione, aprire un nuovo browser e
    immettere l'URL seguente nella barra degli indirizzi:
    <https://portal.azure.com/> per aprire il portale di Azure.

![Uno screenshot di un computer Descrizione generata
automaticamente](./media/image63.png)

2.  Nel portale di Azure, fare clic sul pulsante **\[\>\_\] (Cloud
    Shell)** nella parte superiore della pagina a destra della casella
    di ricerca. Verrà aperto un riquadro Cloud Shell nella parte
    inferiore del portale. La prima volta che si apre Cloud Shell,
    potrebbe essere richiesto di scegliere il tipo di shell che si
    desidera utilizzare (**Bash** o **PowerShell**). Selezionare
    **Bash**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image64.png)

3.  Nella finestra di dialogo **You have no storage mounted**,
    selezionare l'abbonamento e fare clic sul pulsante **Apply**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image65.png)

4.  Una volta avviato il terminale, inserire il seguente comando per
    generare un token di autorizzazione.

> Copy 
>
>  
>
>             [az account
> get-access-token](https://learn.microsoft.com/en-us/cli/azure/account#az-account-get-access-token()) 

5.  A questo punto copiare **accessToken** e quindi **salvare** il
    blocco note per usare le informazioni nell'attività successiva

![A screen shot of a computer AI-generated content may be
incorrect.](./media/image66.png)

6.  A questo punto distribuire il modello ottimizzato, copiare e
    incollare il codice Python seguente nel **Jupyter Notebook**.

7.  Sostituire il TEMP_AUTH_TOKEN (*il valore salvato nell'**attività
    8\>Passaggio 6),*** YOUR_SUBSCRIPTION_ID, YOUR_RESOURCE_GROUP_NAME,
    YOUR_AZURE_OPENAI_RESOURCE_NAME*(i valori salvati nell'**attività 3)
    ***e i valori salvati nel blocco note come mostrato nell' immagine
    sottostante e YOUR_CUSTOM_MODEL_DEPLOYMENT_NAME **come gpt-4o-mini
    (** può essere un nome univoco). Quindi, esegui la cella facendo
    clic sull'**icona di avvio**.

> **Copy** 
>
>  
>
>    \# Deploy fine-tuned model 
>
>  
>
> import json 
>
> import requests 
>
>  
>
> token = os.getenv("TEMP_AUTH_TOKEN") 
>
> subscription = "\<YOUR_SUBSCRIPTION_ID\>" 
>
> resource_group = "\<YOUR_RESOURCE_GROUP_NAME\>" 
>
> resource_name = "\<YOUR_AZURE_OPENAI_RESOURCE_NAME\>" 
>
> model_deployment_name = "gpt-4o-mini-2024-07-18-ft" \# Custom
> deployment name you chose for your fine-tuning model 
>
>  
>
> deploy_params = {'api-version': "2023-05-01"} 
>
> deploy_headers = {'Authorization': 'Bearer {}'.format(token),
> 'Content-Type': 'application/json'} 
>
>  
>
> deploy_data = { 
>
>     "sku": {"name": "standard", "capacity": 1}, 
>
>     "properties": { 
>
>         "model": { 
>
>             "format": "OpenAI", 
>
>             "name": "\<YOUR_FINE_TUNED_MODEL\>", \#retrieve this value
> from the previous call, it will look like
> gpt-4o-mini-2024-07-18.ft-0e208cf33a6a466994aff31a08aba678 
>
>             "version": "1" 
>
>         } 
>
>     } 
>
> } 
>
> deploy_data = json.dumps(deploy_data) 
>
>  
>
> request_url =
> f'https://management.azure.com/subscriptions/{subscription}/resourceGroups/{resource_group}/providers/Microsoft.CognitiveServices/accounts/{resource_name}/deployments/{model_deployment_name}' 
>
>  
>
> print('Creating a new deployment...') 
>
>  
>
> r = requests.put(request_url, params=deploy_params,
> headers=deploy_headers, data=deploy_data) 
>
>  
>
> print(r) 
>
> print(r.reason) 
>
> print(r.json()) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image67.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image68.png)

8.  Controllare ora lo stato di avanzamento della distribuzione in Azure
    AI Foundry.

9.  Aprire il browser, andare alla barra degli indirizzi e digitare o
    incollare il seguente URL: !! *https://oai.azure.com/* !! quindi
    premere il pulsante **Enter**.

> ![Uno screenshot di un computer Descrizione generata
> automaticamente](./media/image69.png)

10. Attendere l'avvio di Azure AI Foundry.

11. Nella finestra **Azure AI Foundry,** selezionare risorsa Azure
    OpenAI**.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image70.png)
>
> ![Uno screenshot di un computer I contenuti generati dall'intelligenza
> artificiale potrebbero non essere corretti.](./media/image71.png)

12. Controllare lo stato del lavoro di messa a punto per il modello
    personalizzato, selezionare **Fine-tuning**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image72.png)

13. Attendere il completamento della distribuzione. L'implementazione
    durerà circa 15-20 minuti.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

### **Attività 9: Utilizzare un modello personalizzato distribuito**

1.  Nella home page di Azure AI Foundry Studio, fare clic su **Chat.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image74.png)

2.  Nella pagina **Chat playground,** assicurati che l'opzione **fine
    -tune model** sia selezionata in **Deployment**

> ![A screenshot of a chat play AI-generated content may be
> incorrect.](./media/image75.png)

3.  Scorrere verso l'alto fino alla sezione **Assistant setup**, nella
    finestra di ** System message**, sostituire il testo corrente con la
    seguente istruzione:

  **The system is an AI teacher that helps people learn about AI**. 

> ![A screenshot of a chat AI-generated content may be
> incorrect.](./media/image76.png)

4.  Sotto la finestra del **System message**, fare clic su **+Add an
    example.**

![A screenshot of a chat session AI-generated content may be
incorrect.](./media/image77.png)

**Nota**: **+Add an example** fornisce al modello esempi dei tipi di
risposte previste. Il modello cercherà di riflettere il tono e lo stile
degli esempi nelle proprie risposte.

5.  Dopo aver fatto clic su **+Add an example**, osserverai la casella
    **User** e la casella **Assistant** e inserirai il seguente
    messaggio e risposta nelle caselle designate:

- **User**: What are the different types of artificial intelligence? 

&nbsp;

- **Assistant**: There are three main types of artificial intelligence:
  Narrow or Weak AI (such as virtual assistants like Siri or Alexa,
  image recognition software, and spam filters), General or Strong AI
  (AI designed to be as intelligent as a human being. This type of AI
  does not currently exist and is purely theoretical), and Artificial
  Superintelligence (AI that is more intelligent than any human being
  and can perform tasks that are beyond human comprehension. This type
  of AI is also purely theoretical and has not yet been developed). 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image78.png)

6.  Fare clic su **Save changes** per avviare una nuova sessione e
    impostare il contesto comportamentale del sistema di chat.

7.  Nella finestra di dialogo **Update system message?**, fare clic sul
    pulsante **Continue.**

![A screenshot of a computer error message AI-generated content may be
incorrect.](./media/image79.png)

8.  Nella sezione **Chat session**, sotto la casella **User message**,
    inserire il seguente testo:

What is artificial intelligence? 

9.  Utilizzare il pulsante **Send **per inviare il messaggio e
    visualizzare la risposta.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image80.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image81.png)

### **Attività 10: Eliminare il modello personalizzato**

1.  Per eliminare l'account di archiviazione, passare alla home page del
    portale di Azure, digitare **Resource groups** nella barra di
    ricerca del portale di Azure, spostarsi e fare clic su **Resource
    groups** in **Services**.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image82.png)

2.  Fare clic sul gruppo di risorse assegnato.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image83.png)

3.  Seleziona attentamente tutte le risorse che hai creato.

4.  Nella pagina **Resource group**, passare alla barra dei comandi e
    fare clic su **Delete**.

**Nota importante**: non fare clic su **elete resource group**. Se non
vedi l'opzione **Delete **nella barra dei comandi, fare clic sui puntini
di sospensione orizzontali.

![Uno screenshot di un computer I contenuti generati dall'intelligenza
artificiale potrebbero non essere corretti.](./media/image84.png)

5.  Nel riquadro **Delete Resources** che appare sul lato destro,
    inserire **delete** e fare clic sul pulsante **Delete**.

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image85.png)

6.  Nella finestra di dialogo **Delete confirmation**, fare clic sul
    pulsante **Delete**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image86.png)

7.  Fare clic sull'icona a forma di campana, vedrai la notifica -
    **Executed delete command on 4 selected items.**
