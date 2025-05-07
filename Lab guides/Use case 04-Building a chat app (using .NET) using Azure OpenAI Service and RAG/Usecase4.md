# Cas d'utilisation 04-Création d'une application de chat (à l'aide de .NET) à l'aide d'Azure OpenAI Service et de RAG

Cet exemple présente quelques approches pour créer des expériences de
type ChatGPT sur vos propres données à l'aide du modèle Retrieval
Augmented Generation. Il utilise le service Azure OpenAI pour accéder au
modèle ChatGPT (gpt-4o-mini) et Azure AI Search pour l'indexation et la
récupération des données.

Le référentiel inclut des exemples de données afin d'être prêt à être
essayé de bout en bout. Dans cet exemple d'application, nous utilisons
une société fictive appelée Contoso Electronics, et l'expérience permet
à ses employés de poser des questions sur les avantages, les politiques
internes, ainsi que les descriptions de poste et les rôles.

![Schéma d'un processus informatique Description générée
automatiquement](./media/image1.png)

- Interfaces de chat vocal, de chat et de questions-réponses

- Explore diverses options pour aider les utilisateurs à évaluer la
  fiabilité des réponses avec des citations, le suivi du contenu source,
  etc.

- Montre les approches possibles pour la préparation des données, la
  construction d'invites et l'orchestration de l'interaction entre le
  modèle (ChatGPT) et l'extracteur (Azure AI Search)

- Paramètres directement dans l'UX pour modifier le comportement et
  expérimenter les options

**Principales technologies utilisées** : Azure OpenAI Service, modèle
ChatGPT (gpt-4o-mini) et Azure AI Search

**Durée estimée --** 40 minutes

# Exercice 1 : Déployer l'application et la tester depuis le navigateur

## Tâche 1 : Environnement de développement ouvert

1.  Ouvrez votre navigateur, accédez à la barre d'adresse, tapez ou
    collez l'URL suivante :
    +++https://github.com/technofocus-pte/azure-search-openai-demo-csharp.git+++
    et connectez-vous avec votre compte Github.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image2.png)

2.  Cliquez sur **Fork**.

> ![](./media/image3.png)

3.  Entrez le repository name puis cliquez sur **Create fork**.

> ![](./media/image4.png)

4.  Click on **Code -\> Codespaces -\> +**

> ![](./media/image5.png)

5.  Attendez que l'environnement soit configuré. Cela prend 5 à 10
    minutes.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image6.png)

## Tâche 2 : Fournir les services requis pour créer et déployer l'application de conversation sur Azure

1.  Exécutez la commande suivante sur le terminal. Copiez le code et
    appuyez sur Entrée.

> +++azd auth login+++
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image7.png)

2.  Le navigateur par défaut s'ouvre pour saisir un code. Entrez le code
    copié et cliquez sur **Next.**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image8.png)

![](./media/image9.png)

3.  Connectez-vous à l'aide de vos informations d'identification Azure.

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image10.png)

![Une capture d'écran d'une erreur informatique Description générée
automatiquement](./media/image11.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image12.png)

4.  Revenez à l'onglet Github Codespace. Exécutez la commande ci-dessous
    pour initialiser l'environnement du projet dans le répertoire
    actuel. Entrez le nom de l'environnement sous la forme
    +++**chatragXXX+++** et appuyez sur Entrée.

> Remarque : le nom de l'environnement doit être unique
>
> +++azd env new+++

![](./media/image13.png)

5.  Exécutez la commande ci-dessous pour provisionner les services sur
    Azure, créez votre conteneur.

> +++azd env set AZURE_RESOURCE_GROUP ResourceGroup1+++
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image14.png)

6.  Exécuter azd up : cela permet d'approvisionner des ressources Azure
    et de déployer cet exemple sur ces ressources, y compris la création
    de l'index de recherche basé sur les fichiers trouvés dans le
    dossier ./data.

> **+++azd haut+++**
>
> ![](./media/image15.png)

7.  Sélectionnez les valeurs ci-dessous.

- **Sélectionnez un abonnement Azure à utiliser** : sélectionnez votre
  abonnement

- **Sélectionnez un emplacement Azure à utiliser** : **East us2/west
  us2** (Parfois, USA Est peut ne pas être disponible, choisissez un
  emplacement dans la liste mentionnée ci-dessous.)

- Sélectionnez un groupe de ressources existant : Votre groupe de
  ressources existant (par exemple :**ResourceGroup1 )**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image16.png)
>
> ![](./media/image17.png)

7.  Attendez que la ressource soit complètement provisionnée. Ce
    processus prendra 5 à 10 minutes pour créer toutes les ressources
    requises.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image18.png)
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image19.png)
>
> ![](./media/image20.png)

8.  Une fois l'application déployée avec succès, une URL s'affiche dans
    le terminal. Copiez l' **URL**

> ![](./media/image21.png)

9.  Cliquez sur **Open**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image22.png)

10. Il ouvre l'application dans un nouvel onglet.

> ![](./media/image23.png)

11. Ouvrez un navigateur, accédez à <https://portal.azure.com> et
    connectez-vous avec votre compte d'abonnement Azure.

12. Sur la page d'accueil, cliquez sur **Resource Groups**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image24.png)

13. Cliquez sur votre resource group

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image25.png)

14. Assurez-vous que la ressource ci-dessous a été déployée avec succès

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image26.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image27.png)

![Une capture d'écran d'un ordinateur Description générée
automatiquement](./media/image28.png)

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image29.png)

15. Dans le groupe de ressources, cliquez sur Nom de la ressource
    **Azure OpenAI**.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image30.png)

16. Dans la **window Azure OpenAI**, cliquez sur **Vue d'ensemble** dans
    le menu de navigation de gauche, puis sous l' onglet **Get
    Started**, cliquez sur le bouton **Go to Azure OpenAI Studio** pour
    ouvrir **Azure OpenAI Studio** dans un nouveau navigateur.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image31.png)

17. Assurez-vous que **gpt-4o-mini**, **text-embedding-ada-002** doit
    être déployé avec succès.

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image32.png)

18. Sur le groupe de ressources, cliquez sur le nom de la ressource du
    **storage account**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image33.png)
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image34.png)

19. Ouvrez maintenant l'URL dans un navigateur

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image23.png)

20. Cliquez sur le **chat**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image35.png)

21. Sur la page de l'application web **Blazor OpenAI**, saisissez le
    texte suivant et cliquez sur le **Submit icon** comme illustré dans
    l'image ci-dessous.

**+++What is included in my Northwind Health Plus plan that is not in
standard?+++**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image36.png)
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image37.png)

22. Sur la page de l'application Web **Blazor OpenAI**, saisissez le
    texte suivant et cliquez sur **Submit icon** comme illustré dans
    l'image ci-dessous.

**+++Can I use out-of-network providers?+++**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image38.png)
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image39.png)

23. Sur la page de l'application Web **Blazor OpenAI**, saisissez le
    texte suivant et cliquez sur **Submit icon** **,** comme illustré
    dans l'image ci-dessous.

**+++Are there any exclusions or restrictions?+++**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image40.png)
>
> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image41.png)

24. Sur la page de l' application Web **Blazor OpenAI**, saisissez le
    texte suivant et cliquez sur **Submit icon** comme illustré dans
    l'image ci-dessous.

**+++What does a Product Manager do?+++**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image42.png)

25. Cliquez sur les **Documents.**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image43.png)

## **Tâche 3 : Nettoyer toutes les ressources**

1.  Revenez au **Azure portal -\> Resource group-\> Resource group
    name.**

> ![Une capture d'écran d'un ordinateur Description générée
> automatiquement](./media/image44.png)

2.  Sélectionnez toutes les ressources, puis cliquez sur Supprimer comme
    indiqué dans l'image ci-dessous. (resource group **DO NOT DELETE)**

> ![](./media/image45.png)

3.  Tapez delete dans la zone de texte, puis cliquez sur **Delete**

> ![](./media/image46.png)

4.  Confirmez la suppression en cliquant sur **Delete**.

> ![](./media/image47.png)

5.  Revenez à l'onglet du portail Github et actualisez la page.

> ![](./media/image48.png)

6.  Cliquez sur Code , sélectionnez la branche créée pour ce laboratoire
    et cliquez sur **Delete**

> ![](./media/image49.png)

7.  Confirmez la suppression de la branche en cliquant sur le bouton
    **Delete**

![](./media/image50.png)

**Résumé:**

Ce cas d'utilisation vous a pensé, déployer une application de
conversation pour le modèle de Retrieval Augmented Generation
s'exécutant sur Azure, utiliser Azure AI Search pour la récupération et
les modèles de langage volumineux (LLM) Azure OpenAI et LangChain pour
alimenter les expériences de type ChatGPT et de questions-réponses
