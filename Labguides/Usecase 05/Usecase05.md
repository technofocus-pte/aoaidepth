**Anwendungsfall 05 – Bereitstellen und Testen einer Conversational
AI-Lösung mit Azure RAG Accelerator**

**Einleitung**

Der Solution Accelerator *"Chat with your data"* ist ein
leistungsstarkes Tool, das die Funktionen von Azure AI Search und Large
Language Models (LLMs) kombiniert, um eine dialogorientierte
Suchumgebung zu erstellen. Dieser Solution Accelerator verwendet ein
Azure OpenAI GPT-Modell und einen Azure AI Search-Index, der aus Ihren
Daten generiert wird und in eine Webanwendung integriert ist, um eine
Benutzeroberfläche in natürlicher Sprache, einschließlich
Sprache-zu-Text-Funktionalität, für Suchabfragen bereitzustellen.
Benutzer können Dateien per Drag & Drop verschieben, auf den Speicher
verweisen und sich um die technische Einrichtung kümmern, um Dokumente
zu transformieren. Es gibt eine Web-App, die Benutzer in ihrem eigenen
Abonnement mit Sicherheit und Authentifizierung erstellen können.

Die Beispieldaten veranschaulichen, wie dieser Beschleuniger in der
Finanzdienstleistungsbranche (FSI) eingesetzt werden könnte.

In diesem Szenario bereitet sich ein Finanzberater auf ein Treffen mit
einem potenziellen Kunden vor, der Interesse an den Emerging Markets
Funds von Woodgrove Investments bekundet hat. Der Berater bereitet sich
auf das Treffen vor, indem er sein Verständnis für die Gesamtziele des
Schwellenländerfonds und die damit verbundenen Risiken auffrischt.

Jetzt, da der Finanzberater besser über die Emerging Markets Funds von
Woodgrove informiert ist, ist er besser in der Lage, auf Fragen seines
Kunden zu diesem Fonds zu antworten.

Hinweis: Einige der Beispieldaten, die in diesem Beschleuniger enthalten
sind, wurden mithilfe von AI generiert und dienen nur zur
Veranschaulichung.

In diesem Anwendungsfall stellen Sie eine Conversational AI-Lösung
mithilfe von Azure RAG-Accelerator (Retrieval-Augmented Generation)
bereit und testen diese. Diese Lösung nutzt die leistungsstarken
AI-Funktionen von Azure, einschließlich Azure OpenAI und Azure AI
Search, um eine erweiterte Konversationssuchumgebung zu erstellen. Am
Ende dieses Labs verfügen Sie über eine voll funktionsfähige
Webanwendung, die die Verarbeitung natürlicher Sprache verwendet, um mit
Ihren Daten zu interagieren und diese abzufragen. Die praktischen
Schritte führen Sie durch die Bereitstellung der erforderlichen
Infrastruktur, die Überprüfung der Ressourcen, das Testen der Lösung und
die Bereinigung der Umgebung.![Ein Computer-Screenshot eines Diagramms
KI-generierte Inhalte können falsch sein.](./media/image1.png)

**Ziele**

- So stellen Sie die erforderliche Infrastruktur über eine
  benutzerdefinierte Vorlage im Azure-Portal bereit.

- Um zu überprüfen, ob alle erforderlichen Azure-Ressourcen erfolgreich
  bereitgestellt wurden.

- Testen der Funktionalität der bereitgestellten Lösung durch Hochladen
  und Verarbeiten von Dokumenten und Interagieren mit der Webanwendung.

- Um die bereitgestellten Ressourcen und Modelle zu löschen.

**Aufgabe 1: Bereitstellen der Infrastruktur aus der Vorlage**

1.  Öffnen Sie Ihren Browser, navigieren Sie zur Adressleiste, geben Sie
    die folgende UR ein oder fügen Sie sie
    ein:+++[www.portal.azure.com/+++then](http://www.portal.azure.com/+++then)
    drücken Sie die **Enter-**Taste.

2.  Geben Sie im **Microsoft Azure**-Fenster Ihre **Anmeldedaten** ein ,
    und klicken Sie auf die Schaltfläche **Next**.

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image2.png)

3.  Geben Sie dann das Passwort ein und klicken Sie auf die Schaltfläche
    **Sign-in**\*\*.\*\*

> ![Ein Screenshot eines Login-Felds KI-generierte Inhalte können falsch
> sein.](./media/image3.png)

4.  Im Fenster **Stay signed in?** klicken Sie auf die Schaltfläche
    **Yes**.

> ![Ein Screenshot eines Computerbildschirms KI-generierte Inhalte
> können falsch sein.](./media/image4.png)

5.  Öffnen Sie einen neuen Browser, und geben Sie die folgende URL in
    die Adressleiste ein:
    +++<https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json+++>,
    um das Azure-Portal zu öffnen.

6.  Geben Sie im Fenster **Custom deployment** auf der Registerkarte
    **Basics** die folgenden Details ein, um die benutzerdefinierte
    Vorlage bereitzustellen, und klicken Sie dann auf **Review +
    create.**

[TABLE]

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image5.png)

7.  Klicken Sie auf der Registerkarte **Review + create**, sobald die
    Validierung bestanden ist, auf die Schaltfläche **Create**.

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image6.png)

8.  Warten Sie, bis die Bereitstellung abgeschlossen ist. Die
    Bereitstellung dauert etwa 17-19 Minuten.

9.  Klicken Sie auf die Schaltfläche **Go to Subscription**

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image7.png)

**Aufgabe 2: Überprüfen der bereitgestellten Ressourcen im
Azure-Portal**

1.  Klicken Sie auf der Startseite auf **Resource Groups**.

> ![Ein Screenshot eines Computerbildschirms KI-generierte Inhalte
> können falsch sein.](./media/image8.png)

2.  Klicken Sie auf den Namen Ihrer Ressourcengruppe
    **rg-RAGSolutionXX**

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image9.png)

3.  Stellen Sie sicher, dass die folgende Ressource erfolgreich in der
    Region "East US" bereitgestellt wurde.

    - Azure App Service

    - Azure Application Insights

    - Azure-Bot

    - Azure OpenAI

    - Azure Document Intelligence

    - Azure Function App

    - Azure Search Service

    - Azure Storage Account

    - Azure Speech Service

    - Azure Database for PostgreSQL - Flexible Server

    - Key vault

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image10.png)

![](./media/image11.png) ![Ein Screenshot eines Computers KI-generierte
Inhalte können falsch sein.](./media/image12.png)

**Aufgabe 3: Testen der Bereitstellung**

1.  Klicken Sie in der Ressourcengruppe auf **Web-** {RESOURCE_TOKEN}
    **- admin-docker** Ressourcenname.

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image13.png)

2.  Navigieren Sie zur

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image14.png)
>
> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image15.png)

3.  Wählen Sie auf **Chat with your data Solution Accelerator**-Seite im
    linken Navigationsmenü die Option **Ingest Data.**

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image16.png)

4.  Klicken Sie im Bereich Add documents in Batch auf Da **Browse file**
    und navigieren Sie zu **C:\Labfiles \data** location, wählen Sie
    **all files** aus und klicken Sie dann auf die Schaltfläche
    **Open**.

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image17.png)

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image18.png)

5.  Das Hochladen von Dateien dauert 1-2 Minuten

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image19.png)

6.  Klicken Sie auf **Reprocess all documents in the Azure Storage
    account.**

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image20.png)

![Ein Screenshot eines Chats KI-generierte Inhalte können falsch
sein.](./media/image21.png)

7.  Wählen Sie auf **Chat with your data Solution Accelerator**-Seite im
    linken Navigationsmenü die Option **"Configuration"** aus, und
    aktivieren Sie das **Kontrollkästchen " Enable post-answering prompt
    ".**

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image22.png)

8.  Klicken Sie im Konfigurationsbereich auf **Save configuration.**

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image23.png)

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image24.png)

9.  Kehren Sie zur Ressourcengruppenseite zurück, und klicken Sie auf
    den Namen von **Storage account**.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image25.png)

10. Klicken Sie im linken Navigationsmenü auf **Containers.**

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image26.png)

11. Wählen Sie auf der Seite Containers die Option **Documents** aus.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image27.png)

12. Stellen Sie sicher, dass alle Dateien erfolgreich bereitgestellt
    werden.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image28.png)

13. Wechseln Sie zurück zur Ressourcengruppenseite.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image29.png)

14. Wählen Sie auf der Ressourcengruppenseite App Service als
    **web-{RESOURCE_TOKEN}-docker** aus.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image30.png)

15. Wählen Sie im reduzierbaren linken Menü unter Settings die Option
    Authentication aus![Ein Screenshot eines Computers KI-generierte
    Inhalte können falsch sein.](./media/image31.png)

16. Klicken Sie auf Add identify provider ![Ein Screenshot eines
    Computers KI-generierte Inhalte können falsch
    sein.](./media/image32.png)

17. Wählen Sie Microsoft als Identitätsanbieter aus, und aktualisieren
    Sie den Namen auf web-XXXXX-docker-new. Wählen Sie die Client secret
    expiration duration auf 90 Days aus, und klicken Sie dann auf Next:
    Permissions.![Ein Screenshot eines Computers KI-generierte Inhalte
    können falsch sein.](./media/image33.png)

18. Klicken Sie auf Add permission. Scrollen Sie in der Liste nach
    unten, um Anwendung zu erweitern, und wählen Sie
    Application.ReadWrite.All aus. Klicken Sie dann auf Update
    permission.

> ![Ein Screenshot eines Computerbildschirms KI-generierte Inhalte
> können falsch sein.](./media/image34.png)

19. Klicken Sie auf Add now.

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image35.png)

20. Klicken Sie auf die Übersichtsseite der App. Warten Sie, bis die
    Seite geladen ist, und klicken Sie dann auf Restart. Bestätigen Sie
    den Neustart mit einem Klick auf Yes![Ein Screenshot eines Computers
    KI-generierte Inhalte können falsch
    sein.](./media/image36.png) ![Ein Screenshot eines Computers
    KI-generierte Inhalte können falsch sein.](./media/image37.png)

21. Navigieren Sie auf der Seite "Web-App-**Overview"** zur
    Befehlsleiste und klicken Sie auf "**Browse**", um zur Webanwendung
    zu gelangen.

> ![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
> sein.](./media/image38.png)

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image39.png)

22. Geben Sie auf der Seite der **Azure AI**-Web-App den folgenden Text
    ein, und klicken Sie auf das **Symbol Submit**, wie in der folgenden
    Abbildung gezeigt.

+++ Describe in more detail the risks from market volatility +++

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image40.png) 

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image41.png)

23. Wählen Sie im Abschnitt **Chat-Session** den Link Referenzen aus und
    beobachten Sie die Details des Suchdokuments auf der rechten Seite
    der Seite.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image42.png)

24. Geben Sie auf der Seite der **Azure AI**-Web-App den folgenden Text
    ein, und klicken Sie auf das Symbol **Submit**, wie in der folgenden
    Abbildung gezeigt.

+++ How does Woodgrove Financial handle payroll taxes for employees
outside the U.S.? +++

![Ein Screenshot eines Chats KI-generierte Inhalte können falsch
sein.](./media/image43.png) ![Ein Screenshot eines Chats KI-generierte
Inhalte können falsch sein.](./media/image44.png)

25. Geben Sie auf der Seite der **Azure AI**-Web-App den folgenden Text
    ein, und klicken Sie auf das **Symbol** **Submit**, wie in der
    folgenden Abbildung gezeigt.

+++ What is FORM 10-K and explain?+++

![Ein Screenshot eines Chats KI-generierte Inhalte können falsch
sein.](./media/image45.png)

**Aufgabe 4: Löschen der Azure OpenAI-Ressource**

1.  Geben Sie zu Azure OpenAI-Ressource **Resource groups** in die
    Suchleiste des Azure-Portals ein, navigieren Sie zu
    Ressourcengruppen, und klicken Sie unter **Services** auf **Resource
    groups**.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image46.png)

2.  Klicken Sie auf Ihre Ressourcengruppe.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image9.png)

3.  Wählen Sie auf einer Übersichtsseite der Ressourcengruppe die Option
    **Delete resource group** aus

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image47.png)

4.  Geben Sie im Bereich **Delete Resources**, der auf der rechten Seite
    angezeigt wird, den **Resource Group Name** ein, und klicken Sie auf
    die Schaltfläche **Delete**.

![Ein Screenshot eines Computers KI-generierte Inhalte können falsch
sein.](./media/image48.png)

5.  Klicken Sie im Dialogfeld **" Delete confirmation** " auf die
    Schaltfläche "**Delete**".

![Ein Screenshot eines Computerfehlers KI-generierte Inhalte können
falsch sein.](./media/image49.png)

**Zusammenfassung**:

Dieses Lab bietet praktische Erfahrungen beim Bereitstellen einer
Conversational AI-Lösung mit dem Azure RAG Accelerator. Sie haben das
Lab gestartet, indem Sie die erforderliche Infrastruktur mithilfe einer
benutzerdefinierten Vorlage bereitgestellt haben. Nachdem Sie die
erfolgreiche Bereitstellung verschiedener Azure-Ressourcen überprüft
haben, haben Sie die Lösung getestet, indem Sie Dokumente hochgeladen
und die Webanwendung zum Ausführen von Abfragen und Abrufen von
Informationen verwendet haben. Schließlich haben Sie die
Ressourcengruppe gelöscht, um die Ressourcen effizient zu verwalten. In
diesem Lab wurde gezeigt, wie die Dateninteraktion und der Datenabruf
mithilfe fortschrittlicher AI-Technologien verbessert werden können.
