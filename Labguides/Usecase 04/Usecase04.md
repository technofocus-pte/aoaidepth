# Anwendungsfall 04 – Erstellen einer Chat-App (mit .NET) mit Azure OpenAI Service und RAG

Dieses Beispiel veranschaulicht einige Ansätze zum Erstellen von
ChatGPT-ähnlichen Erfahrungen für Ihre eigenen Daten mithilfe des
Retrieval Augmented Generation-Musters. Es verwendet Azure OpenAI
Service für den Zugriff auf das ChatGPT-Modell (gpt-4o-mini) und Azure
AI Search für die Datenindizierung und den Abruf.

Das Repository enthält Beispieldaten, sodass es durchgängig ausprobiert
werden kann. In dieser Beispielanwendung verwenden wir ein fiktives
Unternehmen namens Contoso Electronics, und die Erfahrung ermöglicht es
seinen Mitarbeitern, Fragen zu den Leistungen, internen Richtlinien
sowie Stellenbeschreibungen und Rollen zu stellen.

![Ein Diagramm eines Computerprozesses Beschreibung wird automatisch
generiert](./media/image1.png)

- Voice-Chat-, Chat- und Q&A-Schnittstellen

- Untersucht verschiedene Optionen, um Benutzern zu helfen, die
  Vertrauenswürdigkeit von Antworten mit Zitaten, der Verfolgung von
  Quellinhalten usw. zu bewerten.

- Zeigt mögliche Ansätze für die Datenaufbereitung, die zeitnahe
  Erstellung und Orchestrierung der Interaktion zwischen Modell
  (ChatGPT) und Retriever (Azure AI Search)

- Einstellungen direkt in der UX, um das Verhalten zu optimieren und mit
  Optionen zu experimentieren

**Verwendete Schlüsseltechnologien**: Azure OpenAI Service,
ChatGPT-Modell (gpt-4o-mini) und Azure AI Search

**Geschätzte Dauer:** 40 Minuten

# Übung 1: Bereitstellen der Anwendung und Testen über den Browser

## Aufgabe 1: Offene Entwicklungsumgebung

1.  Öffnen Sie Ihren Browser, navigieren Sie zur Adressleiste, geben Sie
    die folgende URL ein oder fügen Sie sie ein:
    +++https://github.com/technofocus-pte/azure-search-openai-demo-csharp.git+++
    und melden Sie sich mit Ihrem Github-Konto an.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image2.png)

2.  Klicken Sie auf **Fork**.

> ![](./media/image3.png)

3.  Geben Sie den Namen des Repositorys ein und klicken Sie dann auf
    **Create fork**.

> ![](./media/image4.png)

4.  Klicken Sie auf **Code -\> Codespaces -\> +**

> ![](./media/image5.png)

5.  Warten Sie, bis die Umgebung eingerichtet ist. Die Fahrt dauert 5-10
    Minuten.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image6.png)

## Aufgabe 2: Bereitstellen der erforderlichen Dienste zum Erstellen und Bereitstellen der Chat-App in Azure

1.  Führen Sie den folgenden Befehl auf dem Terminal aus. Kopieren Sie
    den Code und drücken Sie die Eingabetaste.

> +++azd auth login+++
>
> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image7.png)

2.  Der Standardbrowser wird geöffnet, um einen Code einzugeben. Geben
    Sie den kopierten Code ein und klicken Sie auf **Next**.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image8.png)

![](./media/image9.png)

3.  Melden Sie sich mit Ihren Azure-Anmeldeinformationen an.

![Ein Screenshot eines Computers Beschreibung wird automatisch
generiert](./media/image10.png)

![Ein Screenshot eines Computerfehlers Beschreibung wird automatisch
generiert](./media/image11.png)

![Ein Screenshot eines Computers Beschreibung wird automatisch
generiert](./media/image12.png)

4.  Wechseln Sie zurück zur Registerkarte Github Codespace. Führen Sie
    den folgenden Befehl aus, um die Projektumgebung im aktuellen
    Verzeichnis zu initialisieren. Geben Sie den Umgebungsnamen als
    +++**chatragXXX+++** ein und drücken Sie die Enter-Taste.

> Hinweis: Der Name der Umgebung sollte eindeutig sein
>
> +++azd env neu+++

![](./media/image13.png)

5.  Führen Sie den folgenden Befehl aus, um die Dienste in Azure
    bereitzustellen, und erstellen Sie Ihren Container.

> +++azd env set AZURE_RESOURCE_GROUP ResourceGroup1+++
>
> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image14.png)

6.  Ausführen von azd up: Dadurch werden Azure-Ressourcen
    bereitgestellt, und dieses Beispiel wird für diese Ressourcen
    bereitgestellt, einschließlich des Erstellens des Suchindex
    basierend auf den Dateien im Ordner ./data.

> **+++azd up+++**
>
> ![](./media/image15.png)

7.  Wählen Sie die folgenden Werte aus.

- **Wählen Sie ein zu verwendendes Azure-Abonnement** **aus**: Wählen
  Sie Ihr Abonnement aus

- **Wählen Sie einen zu verwendenden Azure-Standort aus**: **" East
  us2/west us2"** (Manchmal ist "East US" nicht verfügbar. Wählen Sie
  den Standort aus der unten genannten Liste aus.)

- Vorhandene Ressourcengruppe auswählen: Ihre vorhandene
  Ressourcengruppe (z. B. :**ResourceGroup1 )**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image16.png)
>
> ![](./media/image17.png)

7.  Warten Sie, bis die Ressource vollständig bereitgestellt wurde.
    Dieser Vorgang dauert 5-10 Minuten, um alle erforderlichen
    Ressourcen zu erstellen.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image18.png)
>
> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image19.png)
>
> ![](./media/image20.png)

8.  Nachdem die Anwendung erfolgreich bereitgestellt wurde, wird eine
    URL im Terminal angezeigt. Kopieren Sie die **URL**

> ![](./media/image21.png)

9.  Klicken Sie auf die Schaltfläche **Open**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image22.png)

10. Es öffnet die App in einem neuen Tab.

> ![](./media/image23.png)

11. Öffnen Sie einen Browser, wechseln Sie zu
    [<https://portal.azure.com>, und melden Sie sich mit Ihrem
    Azure-Abonnementkonto an.](https://portal.azure.com)

12. Klicken Sie auf der Startseite auf **Resource Groups**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image24.png)

13. Klicken Sie auf Ihre Ressourcengruppe.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image25.png)

14. Stellen Sie sicher, dass die folgende Ressource erfolgreich
    bereitgestellt wurde

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image26.png)

![Ein Screenshot eines Computers Beschreibung wird automatisch
generiert](./media/image27.png)

![Ein Screenshot eines Computers Beschreibung wird automatisch
generiert](./media/image28.png)

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image29.png)

15. Klicken Sie in der Ressourcengruppe auf **Azure**
    **OpenAI**-Ressourcenname.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image30.png)

16. Klicken Sie im **Azure OpenAI-**Fenster im linken Navigationsmenü
    auf **Overview**, und klicken Sie dann auf der Registerkarte **Get
    Started** auf die Schaltfläche **Go to Azure OpenAI Studio**, um
    **Azure OpenAI Studio** in einem neuen Browser zu öffnen.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image31.png)

17. Stellen Sie sicher, dass **gpt-4o-mini**, **text-embedding-ada-002**
    erfolgreich bereitgestellt werden sollte.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image32.png)

18. Klicken Sie in der Ressourcengruppe auf Ressourcenname **“Storage
    Account”**.

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image33.png)
>
> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image34.png)

19. Öffnen Sie nun die URL it in einem Browser

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image23.png)

20. Klicken Sie auf den **Chat**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image35.png)

21. Geben Sie auf der Seite der **Blazor** **OpenAI**-Web-App den
    folgenden Text ein und klicken Sie auf das **Symbol Submit,** wie in
    der folgenden Abbildung gezeigt.

**+++What is included in my Northwind Health Plus plan that is not in
standard?+++**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image36.png)
>
> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image37.png)

22. Geben Sie auf der Seite der **Blazor** **OpenAI**-Web-App den
    folgenden Text ein und klicken Sie auf das **Symbol Submit,** wie in
    der folgenden Abbildung gezeigt.

**+++Can I use out-of-network providers?+++**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image38.png)
>
> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image39.png)

23. Geben Sie auf der Seite der **Blazor** **OpenAI**-Web-App den
    folgenden Text ein und klicken Sie auf das **Symbol Submit,** wie in
    der folgenden Abbildung gezeigt.

**+++Are there any exclusions or restrictions?+++**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image40.png)
>
> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image41.png)

24. Geben Sie auf der Seite der **Blazor** **OpenAI**-Web-App den
    folgenden Text ein und klicken Sie auf das **Symbol Submit,** wie in
    der folgenden Abbildung gezeigt.

**+++What does a Product Manager do?+++**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image42.png)

25. Klicken Sie auf die **Documents.**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image43.png)

## **Aufgabe 3: Bereinigen aller Ressourcen**

1.  Wechseln Sie zurück zum **Azure-Portal -\> Resource group-\>
    Resource group name.**

> ![Ein Screenshot eines Computers Beschreibung wird automatisch
> generiert](./media/image44.png)

2.  Wählen Sie alle Ressourcen aus und klicken Sie dann auf Delete, wie
    in der folgenden Abbildung gezeigt. (Ressourcengruppe **NICHT
    LÖSCHEN**)

> ![](./media/image45.png)

3.  Geben Sie delete in das Textfeld ein und klicken Sie dann auf
    **Delete**.

> ![](./media/image46.png)

4.  Bestätigen Sie den Löschvorgang mit einem Klick auf **Delete**.

> ![](./media/image47.png)

5.  Wechseln Sie zurück zur Registerkarte Github-Portal, und
    aktualisieren Sie die Seite.

> ![](./media/image48.png)

6.  Klicken Sie auf Code , wählen Sie den für dieses Lab erstellten
    Zweig aus und klicken Sie auf **Delete**.

> ![](./media/image49.png)

7.  Bestätigen Sie das Löschen des Zweigs, indem Sie auf die
    Schaltfläche **Delete** klicken.

![](./media/image50.png)

**Zusammenfassung:**

In diesem Anwendungsfall haben Sie sich gedacht, eine Chatanwendung für
das Retrieval Augmented Generation-Muster bereitzustellen, das in Azure
ausgeführt wird, Azure AI Search für den Abruf und Azure OpenAI und
LangChain Large Language Models (LLMs) zu verwenden, um ChatGPT-ähnliche
und Q&A-Erfahrungen zu ermöglichen
