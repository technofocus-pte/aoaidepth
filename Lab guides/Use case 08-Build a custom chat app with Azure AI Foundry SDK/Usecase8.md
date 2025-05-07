Cas d'utilisation 08-Créer une application de chat personnalisée avec le
SDK Azure AI Foundry

**Temps estimé : 120 minutes**

## Objectif

L'objectif de ce laboratoire est de créer, d'évaluer et de déployer un
agent basé sur la génération augmentée par récupération (RAG) à l'aide
du SDK Azure AI Foundry. Le laboratoire vous guide tout au long de la
configuration du projet et de l'environnement de développement, du
déploiement de modèles d'IA (par exemple, GPT-4 et
text-embedding-ada-002), de l'intégration d'Azure AI Search pour la
récupération de documents et de la création d'une application de chat de
récupération des connaissances (RAG) personnalisée. L'accent est mis sur
l'ancrage des réponses du modèle d'IA avec des données produit
pertinentes, le développement d'une interface de chat personnalisée et
l'évaluation des performances des réponses générées.

## Solution

La solution implique la mise en place d'un projet dans Azure AI Foundry,
le déploiement de modèles d'IA (GPT-4 et text-embedding-ada-002) et
l'intégration d'Azure AI Search pour stocker et récupérer des données de
produit personnalisées. Il comprend la création de scripts Python pour
générer des intégrations vectorielles, créer des index de recherche et
les interroger pour obtenir des informations pertinentes sur les
produits. Une interface de chat basée sur RAG est développée pour
fournir des réponses fondées en exploitant les résultats de recherche,
et les performances de l'application de chat sont évaluées à l'aide
d'ensembles de données et de mesures prédéfinis pour améliorer son
efficacité.

## Exercice 0 : Comprendre la machine virtuelle et les informations d'identification

Dans cet exercice, nous allons identifier et comprendre les informations
d'identification que nous utiliserons tout au long du laboratoire.

**Important :** Passez en revue chaque étape de cet exercice pour
connaître les termes génériques et les informations d'identification qui
seront utilisés pour l'exécution du laboratoire.

1.  L'onglet **Instructions** contient le guide de laboratoire avec les
    instructions à suivre tout au long du laboratoire.

2.  **L** 'onglet **Ressources** contient les informations
    d'identification nécessaires à l'exécution du laboratoire.

- **URL** – URL du portail Azure

- **Subscription** – Il s'agit de l**'ID** du **subscription** qui vous
  a été attribué

- **Username**: **User ID** avec lequel vous devez **login** aux **Azure
  services**.

- **Password-** **Password** pour la **Azure login**.

> Appelons ce nom d'utilisateur et ce mot de passe en taant qu’**Azure
> login credentials**. Nous utiliserons ces crédits chaque fois que nous
> mentionnerons les **Azure login credentials**

- **Resource Group** : **Resource Group** qui vous est attribué.

> **Important** : Veillez à créer toutes vos ressources sous ce Resource
> Group

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image1.png)

3.  L'onglet **Help** contient les informations d'assistance. La valeur
    **ID** ici est l'ID de **Lab instance ID** qui sera utilisé lors de
    l'exécution du laboratoire.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image2.png)

## Exercice 1 - Configurer un environnement de projet et de développement pour créer une application de récupération des connaissances (RAG) personnalisée avec le Kit de développement logiciel (SDK) Azure AI Foundry

### Tâche 1 : Créer un projet

Pour créer un projet dans Azure AI Foundry, procédez comme suit :

1.  Connectez-vous à Azure AI Foundry à l'adresse
    +++<https://ai.azure.com/>+++ à l'aide **d’Azure login credentials**

> ![](./media/image3.png)

2.  Sélectionnez **+ Create project**

> ![](./media/image4.png)

3.  Entrez +++**RAGproj\<Lab ID d'instance \>**+++ comme nom du projet,
    cliquez sur **Customize**

> **Remarque :** Remplacez l'**\< Lab instance ID \>** par votre **Lab
> instance ID**
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image5.png)

4.  Sur la page suivante, entrez les détails suivants et cliquez sur
    **Next**

> Hub name : +++hub\<Lab instance ID\>+++
>
> Subscription: Sélectionnez l'abonnement qui vous a été attribué
>
> Create new Resource Group : sélectionnez le Resource Group attribué
> (ResourceGroup1)
>
> Loaction : East US 2 or Sweden Central (nous avons utilisé USA Est 2
> lors de l'exécution de cet atelier)
>
> Laissez le reste par défaut et cliquez sur **Next**
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image6.png)

5.  Sur la page **Review and finish**, cliquez sur **Create.**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image7.png)

6.  La création de la ressource prendra quelques minutes.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image8.png)

7.  Fermez les windows contextuelles, le cas échéant.

8.  À partir de la page d'accueil du projet, notez **la Project
    connection string** dans un bloc-notes à utiliser lors de la
    prochaine tâche de cet exercice.

> ![](./media/image9.png)

### Tâche 2 : Déployer des modèles

Vous avez besoin de deux modèles pour créer une application de
conversation basée sur RAG : un modèle de conversation Azure OpenAI
(gpt-4o-mini) et un modèle d'incorporation Azure OpenAI
(text-embedding-ada-002). Déployez ces modèles dans votre projet Azure
AI Foundry, à l'aide de cet ensemble d'étapes pour chaque modèle.

Les étapes suivantes déploient un modèle sur un point de terminaison en
temps réel à partir du catalogue de modèles du portail AI Foundry :

1.  Dans le volet de navigation de gauche, sélectionnez **Model
    catalog**

> ![](./media/image10.png)

2.  Sélectionnez le **modèle gpt-4o-mini** dans la liste des modèles.
    Vous pouvez utiliser la barre de recherche pour le trouver.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image11.png)

3.  Sur la page des détails du modèle, sélectionnez **Deploy**.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image12.png)

4.  Conservez le **Deployment name** par défaut. sélectionnez
    **Deploy**. Ou, si le modèle n'est pas disponible dans votre région,
    une autre région est sélectionnée pour vous et connectée à votre
    projet. Dans ce cas, sélectionnez **Create resource and deploy**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image13.png)
>
> ![](./media/image14.png)

5.  Après avoir déployé le **gpt-4o-mini**, répétez les étapes pour
    déployer le modèle **+++text-embedding-ada-002+++.**

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image15.png)

### Tâche 3 : Créer un service Azure AI Search

L'objectif de cette application est d'ancrer les réponses du modèle dans
vos données personnalisées. L'index de recherche permet de récupérer des
documents pertinents en fonction de la question de l'utilisateur.

Vous avez besoin d'un service Azure AI Search et d'une connexion pour
créer un index de recherche.

1.  Connectez-vous au portail Azure à l'adresse
    +++<https://portal.azure.com>+++ à l'aide des informations
    d'identification de connexion Azure.

2.  Dans la barre de recherche de la page d'accueil, recherchez **+++AI
    search+++** et sélectionnez-le.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image16.png)

3.  Cliquez sur +**Create** et remplissez les détails suivants.

> ![](./media/image17.png)

4.  Entrez les détails ci-dessous et sélectionnez **Review + create**

- Subscription– Sélectionnez l'abonnement qui vous a été attribué

- Resource Group – Sélectionnez le Resource Group qui vous est attribué

- Service name – Entrez +++**aisearch\<Lab instance ID\>**+++ en
  remplaçant Lab instance id par l'ID de votre VM.

- Région - Sélectionnez Sweden, Central or East US 2(nous utilisons Est
  US 2 ici)

- Niveau tarifaire – Sélectionnez **Standard**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image18.png)

5.  Vérifiez les détails et sélectionnez **Create**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image19.png)

6.  Attendez que le déploiement réussisse comme dans la capture d'écran
    ci-dessous avant de passer à l'étape suivante.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image20.png)

### Tâche 4 : Connecter Azure AI Search à votre projet

Dans le portail Azure AI Foundry, recherchez une ressource connectée à
Azure AI Search.

1.  Dans votre projet dans Azure AI Foundry, sélectionnez **Management
    center** dans le volet gauche.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image21.png)

2.  Dans la section **Connected resources**, sélectionnez **New
    connection**, puis **Azure AI Search**.

> ![](./media/image22.png)
>
> ![](./media/image23.png)

3.  Sélectionnez **API key** sous **Authentication** et sélectionnez
    **Add connection**

> ![Une capture d'écran d'un moteur de recherche Description générée
> automatiquement](./media/image24.png)
>
> ![Une capture d'écran d'un moteur de recherche Description générée
> automatiquement](./media/image25.png)
>
> ![](./media/image26.png)

### Tâche 5 : Installer Azure CLI et se connecter

Vous installez Azure CLI et vous vous connectez à partir de votre
environnement de développement local, afin de pouvoir utiliser vos
informations d'identification utilisateur pour appeler le service Azure
OpenAI.

1.  Recherchez **+++PowerShell+++** dans la barre de recherche Windows
    et ouvrez-le en mode administrateur.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image27.png)

2.  Ouvrez windows Power Shell et collez la commande ci-dessous et
    exécutez-la.

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

3.  Installez Azure CLI à partir de votre terminal à l'aide de la
    commande suivante :

winget install -e --id Microsoft.AzureCLI

Sélectionnez **Y** lorsque vous êtes invité à accepter.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image28.png)

![](./media/image29.png)

![](./media/image30.png)

4.  Après avoir installé Azure CLI, connectez-vous à l'aide de la
    commande az login et connectez-vous à l'aide du navigateur :

+++Az login+++

Sélectionnez **Work or school account** et cliquez sur **Continue**

![Une capture d'écran d'un écran d'ordinateur Description générée
automatiquement](./media/image31.png)

5.  Connectez-vous à l'aide d’ **Azure login credentials**.

![Une capture d'écran d'ordinateur d'un programme Description générée
automatiquement](./media/image32.png)

6.  Entrez **1** pour l'invite **Select a subscription** et cliquez sur
    **Enter**

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image33.png)

### Tâche 6 : Créer un nouvel environnement Python

Tout d'abord, vous devez créer un nouvel environnement Python à utiliser
pour installer le package dont vous avez besoin pour ce tutoriel.
N'installez PAS de packages dans votre installation python globale. Vous
devez toujours utiliser un environnement virtuel ou conda lors de
l'installation de packages python, sinon vous pouvez interrompre votre
installation globale de Python.

**Création d'un environnement virtuel**

1.  À partir de votre Power Shell, accédez à **C :\Users\Admin** en
    exécutant les commandes ci-dessous.

+++cd\\++

+++cd Users\Admin+++

2.  Créez un dossier avec le nom de votre projet, **RAGproj\<Lab
    instance id\>, by entering the following command in your
    powershell.**

**Remarque :** Remplacez \<Nom du projet\> par le nom de votre projet
dans la commande ci-dessous et exécutez-le.

+++**mkdir \<Project name\>**+++

![Un écran d'ordinateur avec du texte blanc et vert Description générée
automatiquement](./media/image34.png)

3.  Dans votre terminal, entrez la commande suivante pour accéder au
    nouvel emplacement du dossier

+++cd **\<Project name\>+++**

Remplacez \<**Project name**\> par le nom du dossier que vous avez créé
à l'étape précédente.

![Un écran bleu avec du texte blanc Description générée
automatiquement](./media/image35.png)

4.  Créez un environnement virtuel à l'aide des commandes suivantes

+++py -3 -m venv .venv+++

+++.venv\scripts\activer+++

> ![Une capture d'écran d'ordinateur d'un code Description générée
> automatiquement](./media/image36.png)
>
> L'activation de l'environnement Python signifie que lorsque vous
> exécutez python ou pip à partir de la ligne de commande, vous utilisez
> ensuite l'interpréteur Python contenu dans le dossier .venv de votre
> application.

5.  Ouvrez **VS Code**. Sélectionnez **File-\> Open folder**, puis
    sélectionnez le dossier **RAGproject** que nous avons créé dans les
    étapes précédentes.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image37.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image38.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image39.png)

### Tâche 7 : Installer les packages

Installez azure-ai-projects (préversion) et azure-ai-inference
(préversion), ainsi que d'autres packages requis.

1.  Créez un fichier nommé **+++requirements.txt+++** dans votre dossier
    **Project** et ajoutez les packages suivants au fichier :

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

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image40.png)

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image41.png)

2.  Dans la barre de navigation supérieure, cliquez sur fichier et
    **save all.**

3.  Faites un clic droit sur le requirements.txt et sélectionnez **Open
    in Integrated Terminal**

![](./media/image42.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image43.png)

4.  Exécutez la commande suivante pour accéder à l'environnement virtuel

py -3 -m venv .venv

.venv\scripts\activate

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image44.png)

5.  Exécutez la commande +++az login+++ et connectez-vous avec vos Azure
    login credentials. Sélectionnez **1** pour sélectionner
    l'abonnement.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image45.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image46.png)

6.  Pour installer les packages requis, exécutez le code suivant.

+++pip install -r requirements.txt+++

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image47.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image48.png)

> **Remarque :** Si vous recevez une notification de nouvelle version de
> pip, exécutez les commandes ci-dessous pour mettre à jour pip
>
> +++pip install -r requirements.txt+++

+++python.exe -m pip install --upgrade pip+++

> ![Une capture d'écran d'un programme informatique Description générée
> automatiquement](./media/image49.png)

### Tâche 8 : Créer un script d'assistance

1.  Créez un nouveau dossier nommé **src**. En exécutant la commande
    suivante dans le terminal.

mkdir src

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image50.png)

2.  Créez un nouveau fichier dans le dossier **src** et nommez-le
    **+++config.py+++**

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image51.png)

3.  Ajoutez le code suivant à **config.py** et enregistrez-le.

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

\# Returns a module-specific logger, inheriting from the root app logger

def get_logger(module_name):

return logging.getLogger(f"app.{module_name}")

\# Enable instrumentation and logging of telemetry to the project

def enable_telemetry(log_to_project: bool = False):

AIInferenceInstrumentor().instrument()

\# enable logging message contents

os.environ\["AZURE_TRACING_GEN_AI_CONTENT_RECORDING_ENABLED"\] = "true"

if log_to_project:

from azure.monitor.opentelemetry import configure_azure_monitor

project = AIProjectClient.from_connection_string(

conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
credential=DefaultAzureCredential()

)

tracing_link =
f"https://ai.azure.com/tracing?wsid=/subscriptions/{project.scope\['subscription_id'\]}/resourceGroups/{project.scope\['resource_group_name'\]}/providers/Microsoft.MachineLearningServices/workspaces/{project.scope\['project_name'\]}"

application_insights_connection_string =
project.telemetry.get_connection_string()

if not application_insights_connection_string:

logger.warning(

"No application insights configured, telemetry will not be logged to
project. Add application insights at:"

)

logger.warning(tracing_link)

return

configure_azure_monitor(connection_string=application_insights_connection_string)

logger.info("Enabled telemetry logging to project, view traces at:")

logger.info(tracing_link)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image52.png)

**Remarque** : ce script de fichier config.py nouvellement créé sera
utilisé dans l'exercice suivant.

### Tâche 9 : Configurer les variables d'environnement

Votre chaîne de connexion de projet est requise pour appeler le service
Azure OpenAI à partir de votre code. Dans ce guide de démarrage rapide,
vous allez enregistrer cette valeur dans un fichier .env, qui contient
des variables d'environnement que votre application peut lire.

1.  Créez un nouveau fichier +++**.env**+++ dans le répertoire **src**
    et collez le code suivant :

Remplacez la **\<your-connection-string\>** par la valeur de la chaîne
de connexion du projet enregistrée dans le bloc-notes dans la tâche 1.

AIPROJECT_CONNECTION_STRING=\<your-connection-string\>

AISEARCH_INDEX_NAME="example-index"

EMBEDDINGS_MODEL="text-embedding-ada-002"

INTENT_MAPPING_MODEL="gpt-4o-mini"

CHAT_MODEL="gpt-4o-mini"

EVALUATION_MODEL="gpt-4o-mini"

![](./media/image53.png)

**Remarque** : Votre chaîne de connexion se trouve dans la page
d'accueil du projet Azure AI Foundry sous **Overview**

## Exercice 2 : Créer une application de récupération des connaissances (RAG) personnalisée avec le SDK Azure AI Foundry

### Tâche 1 : Créer des exemples de données pour votre application de chat

L'objectif de cette application basée sur RAG est d'ancrer les réponses
du modèle dans vos données personnalisées. Vous utilisez un index Azure
AI Search qui stocke des données vectorisées à partir du modèle
d'intégration. L'index de recherche permet de récupérer des documents
pertinents en fonction de la question de l'utilisateur.

1.  À partir de votre configuration VS Code qui est ouverte, créez un
    dossier nommé +++assets+++ sous le dossier **src**.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image54.png)

2.  Copiez **products.csv** fichier à partir de **C :\LabFiles** et
    collez-le dans le dossier racine du **Project**.

Remarque : Cela doit être fait dans l'explorateur de fichiers, puis il
sera reflété dans le VS Code.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image55.png)

3.  Accédez à **File** dans la barre de navigation supérieure et cliquez
    sur **Save all.**

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image56.png)

### Tâche 2 : Créer un index de recherche

> L'index de recherche est utilisé pour stocker les données vectorisées
> du modèle d'embeddings. L'index de recherche permet de récupérer des
> documents pertinents en fonction de la question de l'utilisateur.

1.  Dans VS code, créez un fichier nommé
    **+++create_search_index.py+++** dans votre dossier src
    (c'est-à-dire le même répertoire où vous avez placé votre dossier
    **assets**, et non à l'intérieur du dossier **assets**).

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image57.png)

2.  Ouvrez le fichier créé, **create_search_index.py** fichier et
    ajoutez le code suivant pour importer les bibliothèques requises,
    créer un client de projet et configurer certains paramètres :

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
> \# initialize logging object
>
> logger = get_logger(\_\_name\_\_)
>
> \# create a project client using environment variables loaded from the
> .env file
>
> project = AIProjectClient.from_connection_string(
>
> conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential()
>
> )
>
> \# create a vector embeddings client that will be used to generate
> vector embeddings
>
> embeddings = project.inference.get_embeddings_client()
>
> \# use the project client to get the default search connection
>
> search_connection = project.connections.get_default(
>
> connection_type=ConnectionType.AZURE_AI_SEARCH,
> include_credentials=True
>
> )
>
> \# Create a search index client using the search connection
>
> \# This client will be used to create and delete search indexes
>
> index_client = SearchIndexClient(
>
> endpoint=search_connection.endpoint_url,
> credential=AzureKeyCredential(key=search_connection.key)
>
> )
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image58.png)

3.  Ajoutez maintenant la fonction à la fin de la
    **create_search_index.py** pour définir un index de recherche :

> import pandas as pd
>
> from azure.search.documents.indexes.models import (
>
> SemanticSearch,
>
> SearchField,
>
> SimpleField,
>
> SearchableField,
>
> SearchFieldDataType,
>
> SemanticConfiguration,
>
> SemanticPrioritizedFields,
>
> SemanticField,
>
> VectorSearch,
>
> HnswAlgorithmConfiguration,
>
> VectorSearchAlgorithmKind,
>
> HnswParameters,
>
> VectorSearchAlgorithmMetric,
>
> ExhaustiveKnnAlgorithmConfiguration,
>
> ExhaustiveKnnParameters,
>
> VectorSearchProfile,
>
> SearchIndex,
>
> )
>
> def create_index_definition(index_name: str, model: str) -\>
> SearchIndex:
>
> dimensions = 1536 \# text-embedding-ada-002
>
> if model == "text-embedding-3-large":
>
> dimensions = 3072
>
> \# The fields we want to index. The "embedding" field is a vector
> field that will
>
> \# be used for vector search.
>
> fields = \[
>
> SimpleField(name="id", type=SearchFieldDataType.String, key=True),
>
> SearchableField(name="content", type=SearchFieldDataType.String),
>
> SimpleField(name="filepath", type=SearchFieldDataType.String),
>
> SearchableField(name="title", type=SearchFieldDataType.String),
>
> SimpleField(name="url", type=SearchFieldDataType.String),
>
> SearchField(
>
> name="contentVector",
>
> type=SearchFieldDataType.Collection(SearchFieldDataType.Single),
>
> searchable=True,
>
> \# Size of the vector created by the text-embedding-ada-002 model.
>
> vector_search_dimensions=dimensions,
>
> vector_search_profile_name="myHnswProfile",
>
> ),
>
> \]
>
> \# The "content" field should be prioritized for semantic ranking.
>
> semantic_config = SemanticConfiguration(
>
> name="default",
>
> prioritized_fields=SemanticPrioritizedFields(
>
> title_field=SemanticField(field_name="title"),
>
> keywords_fields=\[\],
>
> content_fields=\[SemanticField(field_name="content")\],
>
> ),
>
> )
>
> \# For vector search, we want to use the HNSW (Hierarchical Navigable
> Small World)
>
> \# algorithm (a type of approximate nearest neighbor search algorithm)
> with cosine
>
> \# distance.
>
> vector_search = VectorSearch(
>
> algorithms=\[
>
> HnswAlgorithmConfiguration(
>
> name="myHnsw",
>
> kind=VectorSearchAlgorithmKind.HNSW,
>
> parameters=HnswParameters(
>
> m=4,
>
> ef_construction=1000,
>
> ef_search=1000,
>
> metric=VectorSearchAlgorithmMetric.COSINE,
>
> ),
>
> ),
>
> ExhaustiveKnnAlgorithmConfiguration(
>
> name="myExhaustiveKnn",
>
> kind=VectorSearchAlgorithmKind.EXHAUSTIVE_KNN,
>
> parameters=ExhaustiveKnnParameters(metric=VectorSearchAlgorithmMetric.COSINE),
>
> ),
>
> \],
>
> profiles=\[
>
> VectorSearchProfile(
>
> name="myHnswProfile",
>
> algorithm_configuration_name="myHnsw",
>
> ),
>
> VectorSearchProfile(
>
> name="myExhaustiveKnnProfile",
>
> algorithm_configuration_name="myExhaustiveKnn",
>
> ),
>
> \],
>
> )
>
> \# Create the semantic settings with the configuration
>
> semantic_search = SemanticSearch(configurations=\[semantic_config\])
>
> \# Create the search index definition
>
> return SearchIndex(
>
> name=index_name,
>
> fields=fields,
>
> semantic_search=semantic_search,
>
> vector_search=vector_search,
>
> )![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image59.png)

4.  Ajoutez maintenant la fonction dans create_search_index.py pour
    créer la fonction permettant d'ajouter un fichier csv à l'index :

> \# define a function for indexing a csv file, that adds each row as a
> document
>
> \# and generates vector embeddings for the specified content_column
>
> def create_docs_from_csv(path: str, content_column: str, model: str)
> -\> list\[dict\[str, any\]\]:
>
> products = pd.read_csv(path)
>
> items = \[\]
>
> for product in products.to_dict("records"):
>
> content = product\[content_column\]
>
> id = str(product\["id"\])
>
> title = product\["name"\]
>
> url = f"/products/{title.lower().replace(' ', '-')}"
>
> emb = embeddings.embed(input=content, model=model)
>
> rec = {
>
> "id": id,
>
> "content": content,
>
> "filepath": f"{title.lower().replace(' ', '-')}",
>
> "title": title,
>
> "url": url,
>
> "contentVector": emb.data\[0\].embedding,
>
> }
>
> items.append(rec)
>
> return items
>
> def create_index_from_csv(index_name, csv_file):
>
> \# If a search index already exists, delete it:
>
> try:
>
> index_definition = index_client.get_index(index_name)
>
> index_client.delete_index(index_name)
>
> logger.info(f"🗑️ Found existing index named '{index_name}', and
> deleted it")
>
> except Exception:
>
> pass
>
> \# create an empty search index
>
> index_definition = create_index_definition(index_name,
> model=os.environ\["EMBEDDINGS_MODEL"\])
>
> index_client.create_index(index_definition)
>
> \# create documents from the products.csv file, generating vector
> embeddings for the "description" column
>
> docs = create_docs_from_csv(path=csv_file,
> content_column="description", model=os.environ\["EMBEDDINGS_MODEL"\])
>
> \# Add the documents to the index using the Azure AI Search client
>
> search_client = SearchClient(
>
> endpoint=search_connection.endpoint_url,
>
> index_name=index_name,
>
> credential=AzureKeyCredential(key=search_connection.key),
>
> )
>
> search_client.upload_documents(docs)
>
> logger.info(f"➕ Uploaded {len(docs)} documents to '{index_name}'
> index")
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image60.png)

5.  Enfin, ajoutez les fonctions ci-dessous dans create_search_index.py
    pour créer l'index et l'enregistrer dans le projet cloud. Après
    avoir ajouté le code, allez dans Fichiers dans la barre supérieure
    et cliquez sur **Save all.**

> if \_\_name\_\_ == "\_\_main\_\_":
>
> import argparse
>
> parser = argparse.ArgumentParser()
>
> parser.add_argument(
>
> "--index-name",
>
> type=str,
>
> help="index name to use when creating the AI Search index",
>
> default=os.environ\["AISEARCH_INDEX_NAME"\],
>
> )
>
> parser.add_argument(
>
> "--csv-file", type=str, help="path to data for creating search index",
> default="assets/products.csv"
>
> )
>
> args = parser.parse_args()
>
> index_name = args.index_name
>
> csv_file = args.csv_file
>
> create_index_from_csv(index_name, csv_file)
>
> ![](./media/image61.png)

6.  Faites un clic droit sur le **create_search_index.py** et
    sélectionnez l'option **Open in integrated terminal**

![](./media/image62.png)

7.  À partir de votre terminal, connectez-vous à vos identifiants de
    connexion Azure et suivez les instructions d'authentification de
    votre compte :

> +++az login+++
>
> ![](./media/image63.png)
>
> ![](./media/image64.png)

8.  Exécutez le code pour générer votre index localement et
    l'enregistrer dans le projet cloud :

> +++python create_search_index.py+++
>
> ![](./media/image65.png)

9.  Une fois le script exécuté, vous pouvez afficher votre index
    nouvellement créé à partir du portail Azure.

10. Accédez à l’espace attribué **Resource Group -\> Your search service
    created(aisearchLabinstanceID) -\> Search management -\> Indexes**.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image66.png)

11. Si vous exécutez à nouveau le script avec le même nom d'index, il
    crée une nouvelle version du même index.

### Tâche 3 : Obtenir les documents du produit

> Ensuite, vous créez un script pour obtenir des documents de produit à
> partir de l'index de recherche. Le script interroge l'index de
> recherche pour trouver les documents qui correspondent à la question
> d'un utilisateur.
>
> **Créer un script pour obtenir des documents sur les produits**
>
> Lorsque le chat reçoit une demande, il recherche dans vos données pour
> trouver des informations pertinentes. Ce script utilise le Kit de
> développement logiciel (SDK) Azure AI pour interroger l'index de
> recherche des documents qui correspondent à la question d'un
> utilisateur. Il renvoie ensuite les documents à l'application de chat.

1.  À partir de VS Code, créez un fichier nommé
    **+++get_product_documents.py+++** dans le dossier **src**.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image67.png)

2.  Copiez et collez le code suivant dans le fichier. Commencez par le
    code pour importer les bibliothèques requises, créer un client de
    projet et configurer les paramètres.

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
> \# initialize logging and tracing objects
>
> logger = get_logger(\_\_name\_\_)
>
> tracer = trace.get_tracer(\_\_name\_\_)
>
> \# create a project client using environment variables loaded from the
> .env file
>
> project = AIProjectClient.from_connection_string(
>
> conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential()
>
> )
>
> \# create a vector embeddings client that will be used to generate
> vector embeddings
>
> chat = project.inference.get_chat_completions_client()
>
> embeddings = project.inference.get_embeddings_client()
>
> \# use the project client to get the default search connection
>
> search_connection = project.connections.get_default(
>
> connection_type=ConnectionType.AZURE_AI_SEARCH,
> include_credentials=True
>
> )
>
> \# Create a search index client using the search connection
>
> \# This client will be used to create and delete search indexes
>
> search_client = SearchClient(
>
> index_name=os.environ\["AISEARCH_INDEX_NAME"\],
>
> endpoint=search_connection.endpoint_url,
>
> credential=AzureKeyCredential(key=search_connection.key),
>
> )

3.  Ajoutez la fonction dans get_product-documents.py pour **get product
    documents**

> from azure.ai.inference.prompts import PromptTemplate
>
> from azure.search.documents.models import VectorizedQuery
>
> @tracer.start_as_current_span(name="get_product_documents")
>
> def get_product_documents(messages: list, context: dict = None) -\>
> dict:
>
> if context is None:
>
> context = {}
>
> overrides = context.get("overrides", {})
>
> top = overrides.get("top", 5)
>
> \# generate a search query from the chat messages
>
> intent_prompty = PromptTemplate.from_prompty(Path(ASSET_PATH) /
> "intent_mapping.prompty")
>
> intent_mapping_response = chat.complete(
>
> model=os.environ\["INTENT_MAPPING_MODEL"\],
>
> messages=intent_prompty.create_messages(conversation=messages),
>
> \*\*intent_prompty.parameters,
>
> )
>
> search_query = intent_mapping_response.choices\[0\].message.content
>
> logger.debug(f"🧠 Intent mapping: {search_query}")
>
> \# generate a vector representation of the search query
>
> embedding = embeddings.embed(model=os.environ\["EMBEDDINGS_MODEL"\],
> input=search_query)
>
> search_vector = embedding.data\[0\].embedding
>
> \# search the index for products matching the search query
>
> vector_query = VectorizedQuery(vector=search_vector,
> k_nearest_neighbors=top, fields="contentVector")
>
> search_results = search_client.search(
>
> search_text=search_query, vector_queries=\[vector_query\],
> select=\["id", "content", "filepath", "title", "url"\]
>
> )
>
> documents = \[
>
> {
>
> "id": result\["id"\],
>
> "content": result\["content"\],
>
> "filepath": result\["filepath"\],
>
> "title": result\["title"\],
>
> "url": result\["url"\],
>
> }
>
> for result in search_results
>
> \]
>
> \# add results to the provided context
>
> if "thoughts" not in context:
>
> context\["thoughts"\] = \[\]
>
> \# add thoughts and documents to the context object so it can be
> returned to the caller
>
> context\["thoughts"\].append(
>
> {
>
> "title": "Generated search query",
>
> "description": search_query,
>
> }
>
> )
>
> if "grounding_data" not in context:
>
> context\["grounding_data"\] = \[\]
>
> context\["grounding_data"\].append(documents)
>
> logger.debug(f"📄 {len(documents)} documents retrieved: {documents}")
>
> return documents

4.  Enfin, ajoutez du code pour **test the function** lorsque vous
    exécutez directement le script :

> if \_\_name\_\_ == "\_\_main\_\_":
>
> import logging
>
> import argparse
>
> \# set logging level to debug when running this module directly
>
> logger.setLevel(logging.DEBUG)
>
> \# load command line arguments
>
> parser = argparse.ArgumentParser()
>
> parser.add_argument(
>
> "--query",
>
> type=str,
>
> help="Query to use to search product",
>
> default="I need a new tent for 4 people, what would you recommend?",
>
> )
>
> args = parser.parse_args()
>
> query = args.query
>
> result = get_product_documents(messages=\[{"role": "user", "content":
> query}\])
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image68.png)

5.  Cliquez sur **File\> Save all**

![](./media/image69.png)

### Tâche 4 : Créer un modèle d'invite pour le mappage d'intention

> Le script **get_product_documents.py** utilise un modèle d'invite pour
> convertir la conversation en requête de recherche. Le modèle indique
> comment extraire l'intention de l'utilisateur de la conversation.

1.  Avant d'exécuter le script, créez le modèle d'invite. Créez un
    fichier nommé +++**intent_mapping.prompty**+++ dans votre dossier de
    **assets**:

> ![](./media/image70.png)

4.  Copiez le code suivant dans le fichier intent_mapping_prompty et
    dans la barre supérieure, allez dans Fichiers et cliquez sur **Save
    all.**

> ---
>
> name: Chat Prompt
>
> description: A prompty that extract users query intent based on the
> current_query and chat_history of the conversation
>
> model:
>
> api: chat
>
> configuration:
>
> azure_deployment: gpt-4o
>
> inputs:
>
> conversation:
>
> type: array
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
> \# Examples
>
> Example 1:
>
> With a conversation like below:
>
> \`\`\`
>
> \- user: are the trailwalker shoes waterproof?
>
> \- assistant: Yes, the TrailWalker Hiking Shoes are waterproof. They
> are designed with a durable and waterproof construction to withstand
> various terrains and weather conditions.
>
> \- user: how much do they cost?
>
> \`\`\`
>
> Respond with:
>
> {
>
> "intent": "The user wants to know how much the Trailwalker Hiking
> Shoes cost.",
>
> "search_query": "price of Trailwalker Hiking Shoes"
>
> }
>
> Example 2:
>
> With a conversation like below:
>
> \`\`\`
>
> \- user: are the trailwalker shoes waterproof?
>
> \- assistant: Yes, the TrailWalker Hiking Shoes are waterproof. They
> are designed with a durable and waterproof construction to withstand
> various terrains and weather conditions.
>
> \- user: how much do they cost?
>
> \- assistant: The TrailWalker Hiking Shoes are priced at $110.
>
> \- user: do you have waterproof tents?
>
> \- assistant: Yes, we have waterproof tents available. Can you please
> provide more information about the type or size of tent you are
> looking for?
>
> \- user: which is your most waterproof tent?
>
> \- assistant: Our most waterproof tent is the Alpine Explorer Tent. It
> is designed with a waterproof material and has a rainfly with a
> waterproof rating of 3000mm. This tent provides reliable protection
> against rain and moisture.
>
> \- user: how much does it cost?
>
> \`\`\`
>
> Respond with:
>
> {
>
> "intent": "The user would like to know how much the Alpine Explorer
> Tent costs.",
>
> "search_query": "price of Alpine Explorer Tent"
>
> }
>
> user:
>
> Return the search query for the messages in the following
> conversation:
>
> {{#conversation}}
>
> \- {{role}}: {{content}}
>
> {{/conversation}}
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image71.png)

### Tâche 5 : Tester le script d'extraction de documents produit

1.  Maintenant que vous disposez à la fois du script et du modèle,
    exécutez le script pour tester les documents renvoyés par l'index de
    recherche à partir d'une requête. À partir de la fenêtre du
    terminal, exécutez

> +++python get_product_documents.py --query "I need a new tent for 4
> people, what would you recommend?"+++
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image72.png)

### Tâche 6 : Développer un code de récupération de connaissances personnalisé (RAG)

> Ensuite, vous créez du code personnalisé pour ajouter des
> fonctionnalités de génération augmentée de récupération (RAG) à une
> application de chat de base.
>
> **Créer un script de chat avec les fonctionnalités RAG**

1.  Dans votre dossier **src**, créez un nouveau fichier appelé
    **+++chat_with_products.py+++.** Ce script récupère les documents du
    produit et génère une réponse à la question d'un utilisateur.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image73.png)

2.  Ajoutez le code pour importer les bibliothèques requises, créer un
    client de projet et configurer les paramètres :

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
> \# initialize logging and tracing objects
>
> logger = get_logger(\_\_name\_\_)
>
> tracer = trace.get_tracer(\_\_name\_\_)
>
> \# create a project client using environment variables loaded from the
> .env file
>
> project = AIProjectClient.from_connection_string(
>
> conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential()
>
> )
>
> \# create a chat client we can use for testing
>
> chat = project.inference.get_chat_completions_client()
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image74.png)

3.  Ajoutez le code à la fin de chat_with_products.py pour créer la
    fonction de chat qui utilise les fonctionnalités RAG.

> from azure.ai.inference.prompts import PromptTemplate
>
> @tracer.start_as_current_span(name="chat_with_products")
>
> def chat_with_products(messages: list, context: dict = None) -\> dict:
>
> if context is None:
>
> context = {}
>
> documents = get_product_documents(messages, context)
>
> \# do a grounded chat call using the search results
>
> grounded_chat_prompt = PromptTemplate.from_prompty(Path(ASSET_PATH) /
> "grounded_chat.prompty")
>
> system_message =
> grounded_chat_prompt.create_messages(documents=documents,
> context=context)
>
> response = chat.complete(
>
> model=os.environ\["CHAT_MODEL"\],
>
> messages=system_message + messages,
>
> \*\*grounded_chat_prompt.parameters,
>
> )
>
> logger.info(f"💬 Response: {response.choices\[0\].message}")
>
> \# Return a chat protocol compliant response
>
> return {"message": response.choices\[0\].message, "context": context}
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image75.png)

4.  Enfin, ajoutez le code pour exécuter la **chat function** puis allez
    dans les fichiers et cliquez sur **Save all**

> if \_\_name\_\_ == "\_\_main\_\_":
>
> import argparse
>
> \# load command line arguments
>
> parser = argparse.ArgumentParser()
>
> parser.add_argument(
>
> "--query",
>
> type=str,
>
> help="Query to use to search product",
>
> default="I need a new tent for 4 people, what would you recommend?",
>
> )
>
> parser.add_argument(
>
> "--enable-telemetry",
>
> action="store_true",
>
> help="Enable sending telemetry back to the project",
>
> )
>
> args = parser.parse_args()
>
> if args.enable_telemetry:
>
> enable_telemetry(True)
>
> \# run chat with products
>
> response = chat_with_products(messages=\[{"role": "user", "content":
> args.query}\])
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image76.png)

### Tâche 7 : Créer un modèle d'invite de chat ancré

> Le script **chat_with_products.py** appelle un modèle d'invite pour
> générer une réponse à la question de l'utilisateur. Le modèle indique
> comment générer une réponse basée sur la question de l'utilisateur et
> les documents récupérés. Créez ce modèle maintenant.

1.  Dans votre dossier **assets**, ajoutez le fichier
    +++**grounded_chat.prompty**+++

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image77.png)

2.  Ajoutez le code suivant grounded_chat.prompty.

> ---
>
> name: Chat with documents
>
> description: Uses a chat completions model to respond to queries
> grounded in relevant documents
>
> model:
>
> api: chat
>
> configuration:
>
> azure_deployment: gpt-4o
>
> inputs:
>
> conversation:
>
> type: array
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
> \# Documents
>
> {{#documents}}
>
> \## Document {{id}}: {{title}}
>
> {{content}}
>
> {{/documents}}
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image78.png)

3.  Cliquez sur **File\> Save all**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image79.png)

### Tâche 8 : Exécuter le script de chat avec les capacités RAG

1.  Maintenant que vous disposez à la fois du script et du modèle,
    exécutez le script pour tester votre application de chat avec les
    fonctionnalités RAG :

> +++python chat_with_products.py --query "I need a new tent for 4
> people, what would you recommend?"+++
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image80.png)

### Tâche 9 : Ajouter la journalisation des données de télémétrie

1.  Dans le portail Azure, sélectionnez **Subscription** , puis
    **Resource providers** sous **Settings** dans le volet de navigation
    de gauche.

2.  Recherchez et sélectionnez +++**Microsoft.OperationalInsights**+++
    et cliquez sur les trois points de ce fournisseur de ressources et
    sélectionnez **Register.**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image81.png)

3.  Suivez la même procédure pour enregistrer +++microsoft.insights+++

4.  Attendez un message de réussite sur l'inscription avant de passer à
    l'étape suivante.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image82.png)

5.  À partir de votre projet dans Azure AI Foundry, sélectionnez
    **Tracing** sous **Access and improve** dans le volet gauche.
    Sélectionnez **Create new.**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image83.png)
>
> ![Une capture d'écran d'un écran d'ordinateur Description générée
> automatiquement](./media/image84.png)

6.  Assurez-vous que la ressource est créée.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image85.png)

7.  De retour dans le VS Code, pour activer la journalisation des
    données de télémétrie dans votre projet, installez
    azure-monitor-opentelemetry.

> +++pip install azure-monitor-opentelemetry+++
>
> ![Une capture d'écran d'un programme informatique Description générée
> automatiquement](./media/image86.png)

8.  Ajoutez l'indicateur --enable-telemetry lorsque vous utilisez le
    script chat_with_products.py :

> +++python chat_with_products.py --query "I need a new tent for 4
> people, what would you recommend?" --enable-telemetry+++
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image87.png)

## Exercice 3 : Évaluer l'application de conversation personnalisée à l'aide du Kit de développement logiciel (SDK) Azure AI Foundry

### Tâche 1 : Évaluer la qualité des réponses de l'application de chat

Maintenant que vous savez que votre application de chat répond bien à
vos requêtes, y compris avec l'historique des chats, il est temps
d'évaluer ses performances sur quelques indicateurs différents et plus
de données.

Vous utilisez un évaluateur avec un jeu de données d'évaluation et la
fonction cible get_chat_response(), puis vous évaluez les résultats de
l'évaluation.

Une fois que vous avez exécuté une évaluation, vous pouvez apporter des
améliorations à votre logique, comme améliorer l'invite de votre système
et observer comment les réponses de l'application de chat changent et
s'améliorent.

**Créer un jeu de données d'évaluation**

Utilisez le jeu de données d'évaluation suivant, qui contient des
exemples de questions et de réponses attendues (vérité).

1.  Créez un fichier appelé +++**chat_eval_data.jsonl**+++ dans votre
    dossier **assets**.

> ![](./media/image88.png)

2.  Collez cet ensemble de données dans le fichier et **save**

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
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image89.png)

### Tâche 2 : Évaluer avec des évaluateurs Azure AI

Définissez maintenant un script d'évaluation qui va :

- Générez un wrapper de fonction cible autour de la logique de notre
  application de chat.

- Chargez l'exemple de jeu de données .jsonl.

- Exécutez l'évaluation, qui prend la fonction cible et fusionne
  l'ensemble de données d'évaluation avec les réponses de l'application
  de conversation.

- Générez un ensemble de mesures assistées par GPT (pertinence, ancrage
  et cohérence) pour évaluer la qualité des réponses de l'application de
  chat.

- Produisez les résultats localement et enregistrez les résultats dans
  le projet cloud.

Le script vous permet d'examiner les résultats localement, en les
sortant dans la ligne de commande et dans un fichier json.

Le script enregistre également les résultats de l'évaluation dans le
projet cloud afin que vous puissiez comparer les exécutions d'évaluation
dans l'interface utilisateur.

1.  Créez un fichier appelé +++evaluate.py+++ dans le dossier **src**.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image90.png)

2.  Ajoutez le code suivant pour importer les bibliothèques requises,
    créer un client de projet et configurer certains paramètres :

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
> from chat_with_products import chat_with_products
>
> \# load environment variables from the .env file at the root of this
> repo
>
> from dotenv import load_dotenv
>
> load_dotenv()
>
> \# create a project client using environment variables loaded from the
> .env file
>
> project = AIProjectClient.from_connection_string(
>
> conn_str=os.environ\["AIPROJECT_CONNECTION_STRING"\],
> credential=DefaultAzureCredential()
>
> )
>
> connection =
> project.connections.get_default(connection_type=ConnectionType.AZURE_OPEN_AI,
> include_credentials=True)
>
> evaluator_model = {
>
> "azure_endpoint": connection.endpoint_url,
>
> "azure_deployment": os.environ\["EVALUATION_MODEL"\],
>
> "api_version": "2024-06-01",
>
> "api_key": connection.key,
>
> }
>
> groundedness = GroundednessEvaluator(evaluator_model)
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image91.png)

3.  Ajoutez du code pour créer une fonction wrapper qui implémente
    l'interface d'évaluation pour l'évaluation des requêtes et des
    réponses :

> def evaluate_chat_with_products(query):
>
> response = chat_with_products(messages=\[{"role": "user", "content":
> query}\])
>
> return {"response": response\["message"\].content, "context":
> response\["context"\]\["grounding_data"\]}
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image92.png)

4.  Enfin, ajoutez du code pour exécuter l'évaluation, affichez les
    résultats localement et vous donne un lien vers les résultats de
    l'évaluation dans le portail AI Foundry.

> \# Evaluate must be called inside of \_\_main\_\_, not on import
>
> if \_\_name\_\_ == "\_\_main\_\_":
>
> from config import ASSET_PATH
>
> \# workaround for multiprocessing issue on linux
>
> from pprint import pprint
>
> from pathlib import Path
>
> import multiprocessing
>
> import contextlib
>
> with contextlib.suppress(RuntimeError):
>
> multiprocessing.set_start_method("spawn", force=True)
>
> \# run evaluation with a dataset and target function, log to the
> project
>
> result = evaluate(
>
> data=Path(ASSET_PATH) / "chat_eval_data.jsonl",
>
> target=evaluate_chat_with_products,
>
> evaluation_name="evaluate_chat_with_products",
>
> evaluators={
>
> "groundedness": groundedness,
>
> },
>
> evaluator_config={
>
> "default": {
>
> "query": {"${data.query}"},
>
> "response": {"${target.response}"},
>
> "context": {"${target.context}"},
>
> }
>
> },
>
> azure_ai_project=project.scope,
>
> output_path="./myevalresults.json",
>
> )
>
> tabular_result = pd.DataFrame(result.get("rows"))
>
> pprint("-----Summarized Metrics-----")
>
> pprint(result\["metrics"\])
>
> pprint("-----Tabular Result-----")
>
> pprint(tabular_result)
>
> pprint(f"View evaluation results in AI Studio:
> {result\['studio_url'\]}")
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image93.png)

5.  Cliquez sur **Save all** sous **File** dans la barre de navigation
    supérieure.

### Tâche 3 : Configurer le modèle d'évaluation

Étant donné que le script d'évaluation appelle le modèle plusieurs fois,
vous souhaiterez peut-être augmenter le nombre de jetons par minute pour
le modèle d'évaluation.

Initialement, vous avez créé un fichier **.env** qui spécifie le nom du
modèle d'évaluation, gpt-4o-mini. Essayez d'augmenter la limite de
jetons par minute pour ce modèle, si vous avez un quota disponible. Si
vous n'avez pas assez de quota pour augmenter la valeur, ne vous
inquiétez pas. Le script est conçu pour gérer les erreurs de limite.

1.  À partir de votre projet dans le portail Azure AI Foundry,
    sélectionnez **Models + endpoints** , puis **gpt-4o-mini**.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image94.png)

2.  Sélectionnez **gpt-4o-mini**, cliquez sur **Edit**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image95.png)

3.  Définissez la valeur de la **Tokens per Minutes Rate Limit** sur la
    limite maximale autorisée, puis sélectionnez **Save and close.**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image96.png)

### Tâche 4 : Exécuter l'évaluation 

1.  Dans Azure AI Foundry, sélectionnez **Evaluations** dans le volet
    gauche, puis sélectionnez **+ New Evaluation**

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image97.png)

2.  Sélectionnez **Dataset**.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image98.png)

3.  Acceptez les valeurs par défaut dans la page Informations de base et
    cliquez sur **Next.**

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image99.png)

4.  Sélectionnez **Add youir dataset -\> Upload file** le fichier et
    chargez le fichier **chat_eval_data.jsonl** que nous avons créé dans
    le dossier des **assets** et cliquez sur **Next**.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image100.png)

5.  Sélectionnez les **Metrics** sous AI quality and Risk and safety
    metrics.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image101.png)

![Une capture d'écran d'une enquête Description générée
automatiquement](./media/image102.png)

6.  Sélectionnez les types de source de données comme dans la capture
    d'écran ci-dessous et cliquez sur **Next**

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image103.png)

7.  Sélectionnez **Submit** pour soumettre l'évaluation.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image104.png)

8.  Une fois l'évaluation terminée, explorez les résultats.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image105.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image106.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image107.png)

## Exercice 4 : Supprimer les ressources

1.  Dans la page d'accueil du portail Azure, sélectionnez le Resource
    Group attribué. Sélectionnez toutes les ressources sous le Resource
    Group , puis sélectionnez Delete.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image108.png)

2.  Entrez **+++delete+++** et cliquez sur le bouton **Delete** pour
    confirmer la suppression. Cliquez sur **Delete** dans la boîte de
    dialogue de confirmation Delete

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image109.png)

3.  Confirmez la suppression de toutes les ressources avec un message de
    réussite.

![Une capture d'écran d'un écran d'ordinateur Description générée
automatiquement](./media/image110.png)

> **Résumé:**
>
> Dans ce laboratoire nous avons appris à créer, évaluer et déployer une
> application basée sur RAG.
