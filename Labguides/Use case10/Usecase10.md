# Caso de uso 10: Crear una aplicación web y un bot de Power Virtual Agent con datos personalizados utilizando Azure OpenAI Service

**Introducción:**

Azure OpenAI en sus datos funciona con los potentes modelos de lenguaje
ChatGPT (gpt-35-turbo) y GPT-4 de OpenAI, lo que les permite
proporcionar respuestas basadas en sus datos. Puede acceder a Azure
OpenAI en sus datos utilizando una API REST o la interfaz basada en web
en Azure OpenAI Studio para crear una solución que se conecte a sus
datos y permita una experiencia de chat mejorada.

Una de las características clave de Azure OpenAI en sus datos es su
capacidad para recuperar y utilizar datos de una manera que mejora la
salida del modelo. Azure OpenAI en sus datos, junto con Azure Cognitive
Search, determina qué datos recuperar de la fuente de datos designada
según la entrada del usuario y el historial de la conversación
proporcionado. Estos datos luego se aumentan y se vuelven a enviar como
un prompt al modelo de OpenAI, con la información recuperada siendo
añadida al prompt original. Aunque los datos recuperados se añaden al
prompt, la entrada resultante sigue siendo procesada por el modelo como
cualquier otro prompt. Una vez que se han recuperado los datos y se ha
enviado el prompt al modelo, este utiliza esta información para generar
una respuesta.

**Objetivos**

- Crear una cuenta de almacenamiento, un contenedor y un servicio de
  búsqueda cognitiva de Azure en el portal de Azure.

- Implementar los modelos gpt-3-turbo y Embedded en Azure AI Studio y
  agregar datos en Chat Playground.

- Probar la configuración del asistente en Chat Playground enviando
  consultas en la sesión de chat.

- Iniciar un Copilot e iniciar una conversación con el bot.

- Iniciar una nueva aplicación y comenzar una conversación con la
  aplicación Copilot.

- Eliminar el modelo gpt-3-turbo y el modelo embedded, la cuenta de
  almacenamiento de Azure, el servicio de búsqueda cognitiva y la nueva
  aplicación web.

## Ejercicio 1: Crear una cuenta de almacenamiento de Azure y un servicio de búsqueda cognitiva de Azure mediante el portal

### Tarea 1: Cree un recurso Azure OpenAI

1.  Abra su navegador, vaya a la barra de direcciones y escriba o pegue
    la siguiente
    [URL:+++https://portal.azure.com/](URL:+++https://portal.azure.com/)+++,
    después pulse la tecla **Enter.** ![](./media/image1.png)

2.  En la ventana de **Microsoft Azure**, utilice las **User
    Credentials** para iniciar sesión en Azure.

![](./media/image2.png)

3.  A continuación, ingrese la contraseña y haga clic en el botón **Sign
    in**.

![](./media/image3.png)

4.  En la ventana **Stay signed in?**, haga clic en el botón **Yes.**

5.  En la página de inicio del portal Azure, haga clic en el **Azure
    portal menu**, representado por tres barras horizontales en la parte
    izquierda de la barra de comandos de Microsoft Azure, como se
    muestra en la siguiente imagen.

![](./media/image4.png)

6.  Navegue y haga clic en **+ Create a resource**.

![](./media/image5.png)

7.  En la página **Create a resource**, en la barra de búsqueda **Search
    services and marketplace**, escriba **Azure OpenAI** y, a
    continuación, pulse el botón **Enter.**

![](./media/image6.png)

8.  En la página **Marketplace**, navegue hasta la sección **Azure
    OpenAI**, haga clic en el menú desplegable del botón **Create** y, a
    continuación, seleccione **Azure OpenAI** como se muestra en la
    imagen. (En caso de que ya haya hecho clic en el mosaico **Azure
    OpenAI**, haga clic en el botón **Create** en la página de **Azure
    OpenAI**).

![](./media/image7.png)

9.  En la ventana **Crear Azure OpenAI**, en la pestaña **Basics**,
    ingrese los siguientes datos y haga clic en el botón **Next.**

[TABLE]

> ![](./media/image8.png)

10. En la pestaña **Network**, deje todos los botones de opción en
    estado predeterminado y haga clic en el botón **Next**.

![](./media/image9.png)

11. En la pestaña **Tags**, deje todos los campos en estado
    predeterminado y haga clic en el botón **Next**.

![](./media/image10.png)

12. En la pestaña **Review+submit**, una vez superada la validación,
    haga clic en el botón **Create.**

![](./media/image11.png)

13. Espere a que se complete la implementación, lo que tomará
    aproximadamente 2-3 minutos.

14. En la ventana **Microsoft.CognitiveServicesOpenAI**, una vez
    finalizada la implementación, haga clic en el botón **Go to
    resource.**

![](./media/image12.png)

### Tarea 2: Cree una cuenta de almacenamiento de Azure mediante el portal

1.  Inicie sesión en +++<https://portal.azure.com/+++>

2.  Haga clic en el **Portal Menu** y seleccione **+ Create a
    resource**.

![](./media/image13.png)

3.  En el cuadro de búsqueda de la ventana **Create a resource**,
    escriba **Storage account** y, a continuación, haga clic en
    **storage account.**

![](./media/image14.png)

4.  En la página de **Marketplace**, haga clic en la sección **Storage
    account**.

![](./media/image15.png)

5.  En la ventana **Storage account**, haga clic en el botón **Create.**

![](./media/image16.png)

6.  En la ventana **Create a storage account**, en la pestaña
    **Basics**, ingrese los siguientes datos para crear una cuenta de
    almacenamiento. A continuación, haga clic en **Review.**

[TABLE]

> ![](./media/image17.png)

7.  En la pestaña **Review**, haga clic en el botón **Create.**

![](./media/image18.png)

8.  Esta nueva cuenta de Azure Storage ya está configurada para alojar
    datos para un Azure Data Lake. Haga clic en el botón **Go to
    resource**.

![](./media/image19.png)

9.  Después de que la cuenta se haya implementado, encontrará opciones
    relacionadas con Azure Data Lake en la página de descripción
    general. En el panel de navegación izquierdo, vaya a la sección
    **Data storage** y haga clic en **Containers.**

![](./media/image20.png)

10. En la página **azureopenaistorageXX | Containers**, haga clic
    en **+Container.**

![](./media/image21.png)

11. En el panel **New container** que aparece a la derecha, ingrese el
    **nombre** del contenedor como +++**source**+++ y haga clic en el
    botón **Create.** 

![](./media/image22.png)

12. En la página **azureopenaistorageXX | Containers**, seleccione el
    contenedor de origen \*\*\***source** \*\*\*.

![](./media/image23.png)

13. En la página del contenedor **source**, haga clic en el botón
    **Upload.**

![](./media/image24.png)

14. En el panel **Upload blob**, haga clic en **Browse for file**, vaya
    a la ubicación **C:\Labfiles** y seleccione **TF-AzureOpenAI.pdf**.
    A continuación, haga clic en el botón **Open.**

![](./media/image25.png)

\![\](./media/image50.png)

15. En el panel **Upload blob**, haga clic en el botón **Upload.**

![](./media/image26.png)

16. Verá la siguiente notificación cuando la carga se haya realizado con
    éxito- **Successfully uploaded blob.**

![](./media/image27.png)

![](./media/image28.png)

### Tarea 3: Cree un servicio de Azure AI Search en el portal

1.  En la página **azureopenaistorageXX | Containers**, haga clic en
    **Home** para regresar a la página de inicio del portal de Azure.

![](./media/image29.png)

2.  En la página de inicio del portal Azure, haga clic en **+ Create
    Resource**.

![](./media/image30.png)

3.  En la barra de búsqueda **Create a resource**, escriba **Azure AI
    Search** y haga clic en la búsqueda **azure ai search.**

![](./media/image31.png)

4.  Haga clic en la sección de **azure ai search**.

![](./media/image32.png)

5.  En la página **Azure AI Search**, haga clic en el botón **Create.**

6.  \![\](./media/image58.png)

7.  En la página **Create a search service**, facilite la siguiente
    información y haga clic en el botón **Review+create**.

[TABLE]

> ![](./media/image33.png)
>
> ![](./media/image34.png)

8.  Una vez superada la validación, haga clic en el botón **Create.**

![](./media/image35.png)

9.  Una vez finalizada la implementación, haga clic en el botón **Go to
    resource.** 

![](./media/image36.png)

10. En la página general de **mysearchserviceXX**. En el panel de
    navegación de la izquierda, en la sección de **Settings**,
    seleccione **Semantic ranker.**

![](./media/image37.png)

11. En la pestaña **Semantic ranker**, seleccione la ficha **Standard**
    y haga clic en el botón **Select plan.**

![](./media/image38.png)

12. Verá la siguiente notificación -**Successfully updated semantic
    ranker to free plan**

## Ejercicio 2: Agregar sus datos usando Azure OpenAI Studio

### Tarea 1: Implemente gpt-35-turbo y modelos embedded en Azure AI Studio

1.  Vuelva al portal Azure, busque Azure OpenAI y selecciónelo.

![](./media/image39.png)

2.  Seleccione su servicio **Azure OpenAI**.

![](./media/image40.png)

![](./media/image41.png)

3.  En la ventana **AzureOpenAI**, haga clic en **Overview** en el menú
    de navegación de la izquierda y, a continuación, haga clic en el
    botón **Explore Azure AI Foundry portal** para **Azure AI Foundry
    portal** en un nuevo navegador.

![](./media/image42.png)

4.  En la página de inicio de **Azure AI Foundry |Azure OpenAI Studio**
    seleccione **Deployment** en el menú de navegación de la izquierda.

> ![](./media/image43.png)

5.  En la ventana **Deployments**, implemente el modelo **+Deploy
    model** y seleccione **Deploy base model**.

![](./media/image44.png)

6.  En el cuadro de diálogo **Select a model**, navegue y seleccione
    cuidadosamente **gpt-4**. A continuación, haga clic en el botón
    **Confirm.**

> ![](./media/image45.png)

7.  En el cuadro de diálogo **Deploy model dialog**, ingrese los
    siguientes datos y haga clic en el botón **Create.**

    - Seleccione el modelo: **gpt-35-turbo**

    - Nombre de la implementación: Ingrese **gpt-35-turbo**

    - Seleccione la opción **Standard** como **Deployment type**

> ![](./media/image46.png)
>
> ![](./media/image47.png)
>
> ![](./media/image48.png)

8.  En la ventana **Deployments**, implemente el modelo **+Deploy
    model** y seleccione **Deploy base model.**

> ![](./media/image49.png)

9.  En el cuadro de diálogo **Select a model**, navegue y seleccione
    cuidadosamente **text-embedding-ada-002** y, a continuación, haga
    clic en el botón **Confirm**.

![](./media/image50.png)

10. En el cuadro de diálogo **Deploy model**, en **Deployment
    name** ingrese

> +++text-embedding-ada-002+++, seleccione **Standard** como
> **Deployment type** y haga clic en el botón **Deploy**.

![](./media/image51.png)

![](./media/image52.png)

11. En la página de inicio de **Azure AI Foundry |Azure OpenAI
    Service**, en la sección **Playgrounds**, haga clic en el **Chat.**

![](./media/image53.png)

12. En el panel **Chat playground**, despliegue **Add your data** y
    seleccione **+Add a data source.**

![](./media/image54.png)

### Tarea 2: Agregue sus datos usando Azure OpenAI Studio

1.  En la página **Select or add data source**, haga clic en el menú
    desplegable bajo **Select or add data source**, luego navegue y haga
    clic en **Azure Blob Storage.**

2.  En la página **Select or add data source**, en **Select or add data
    source** ingrese los siguientes datos y seleccione **Next.**

[TABLE]

3.  Seleccione la casilla – **Add vector search to this search
    resource**.

4.  Seleccione un modelo de embedding como por ejemplo
    **text-embedding-ada-002**. A continuación, haga clic en el botón
    **Next.**

![](./media/image55.png)

**Nota:** *En caso de que encuentre un error - **Can‘t manage CORS on
this resource. Por favor, seleccione otro recurso de almacenamiento** y,
a continuación, sincronice la hora de su máquina virtual, como se indica
en la Tarea \#1.*

5.  En la página **Add data**, en la pestaña **Data management**,
    implemente el tipo de búsqueda y seleccione **Hybrid+semantic**.

6.  Seleccione **chunk size** como **1024 (default).** A continuación,
    haga clic en **Next.**

![](./media/image56.png)

7.  En el panel **Data connection**, seleccione **API key** y haga en el
    botón **Next.**

![](./media/image57.png)

8.  En el panel **Review and Finish**, revise los datos ingresados y
    haga clic en el botón **Save and close.**

![](./media/image58.png)

9.  Los datos se agregarán a su Chat Playground. Esto tomará
    aproximadamente 4-5 minutos.

![](./media/image59.png)

![](./media/image60.png)

### Tarea 3: Explore la función de autocompletado de texto en el Chat Playground

1.  En la sección **Chat session**, ingrese el siguiente prompt en el
    cuadro de texto **User message** y haga clic en el icono **Send.**

> CodeCopy
>
> What is Azure OpenAI Service?

![](./media/image61.png)

![](./media/image62.png)

2.  En la sección de **Chat session**, seleccione el enlace de
    referencias y observe los detalles del documento de búsqueda en el
    lado derecho de la página.

![](./media/image63.png)

![](./media/image64.png)

## Ejercicio 3: Implemente una aplicación web con datos personalizados

### Tarea 1: Implemente una aplicación web

1.  En la página de inicio de **Azure AI Foundry | Azure OpenAI
    Service**, en el panel **Chat Playground**, despliegue el menú
    **Deploy**, luego navegue y haga clic en **As Web App.**

![](./media/image65.png)

2.  En la ventana **Deploy to a web app**, seleccione el botón de opción
    **Create a new web app** e ingrese los siguientes datos:

[TABLE]

3.  Seleccione la casilla de verificación de **Enable chat history in
    the web app**

4.  Pulse el botón **Deploy**.

**Nota:** La implementación tarda entre 5 y 10 minutos.

![](./media/image66.png)

5.  Para verificar el estado de implementación, haga clic en
    **Deployments** y seleccione **App deployment**.

![](./media/image67.png)

![](./media/image68.png)

6.  Espere a que se complete la implementación. La instalación tardará
    entre **10** y **15** minutos.

![](./media/image69.png)

7.  Haga clic en la aplicación web.

![](./media/image70.png)

8.  Espere 10 minutos para que la configuración de autenticación se
    aplique correctamente en la aplicación.

9.  Transcurridos 10 minutos, haga clic en el botón **Refresh.**

10. En el cuadro de diálogo **Permissions requested**, haga clic en el
    botón **Accept**.

![](./media/image71.png)

11. Ahora, la aplicación web se abrirá en un nuevo navegador.

![](./media/image72.png)

12. En la página de la aplicación web **Azure AI**, ingrese el siguiente
    texto y haga clic en el icono **Submit**, como se muestra en la
    siguiente imagen

**CodeCopy**

How do I get access to Azure OpenAI?

![](./media/image73.png)

![](./media/image74.png) ![](./media/image75.png)

13. Del mismo modo, pegue el siguiente texto en el cuadro de texto y
    haga clic en el icono **Send**.

**CodeCopy**

**+++What is the expiry date of GPT-35-Turbo version 0301 and GPT-4
version 0314?+++**

![](./media/image76.png)

![](./media/image77.png)

14. Actualice la página de la aplicación web y haga clic en el botón
    **Show chat history**.

![](./media/image78.png)

![](./media/image79.png)

15. Debajo del historial de chat, haga clic en **Accessing Azure
    OpenAI**.

![](./media/image80.png)

![](./media/image81.png)

## Ejercicio 4: Crear una aplicación Copilot con datos personalizados

### Tarea 1: Cree un chatbot con datos personalizados

1.  En **Azure AI Foundry |Azure AI Studio** **Chat playground**, en la
    opción **Add your data** seleccione la opción **Remove data
    source**.

![](./media/image82.png)

2.  En el panel **Chat playground**, implemente **Add your data** y
    seleccione **+Add a data source.  
    **

![](./media/image54.png)

3.  En la página **Add data**, en **Select or add data source** ingrese
    los siguientes datos y seleccione **Next.**

[TABLE]

> ![](./media/image83.png)*  
> ***Nota:** *En caso de que encuentre un error - **Can‘t manage CORS on
> this resource**. **Seleccione otro recurso de almacenamiento** y, a
> continuación, sincronice la hora de su máquina virtual, como se indica
> en la tarea \# 1*.

4.  En la página **Add data**, en la pestaña **Data management**,
    implemente el tipo de búsqueda y seleccione **Keyword**, seleccione
    el tamaño de fragmento como **1024(default)**. Luego, haga clic en
    **Next**.

![](./media/image84.png)

5.  En el panel **Data connection**, seleccione **API key** y haga clic
    en el botón **Next.**

![](./media/image57.png)

6.  En **Review and Finish**, revise los datos ingresados y haga clic en
    el botón **Save and close**.

![](./media/image85.png)

![](./media/image86.png) ![](./media/image87.png)

7.  Los datos se añadirán a su Chat Playground. Tardará aproximadamente
    4-5 minutos.

### Tarea 2: Cree un Copilot con datos personalizados desde Azure OpenAI

1.  Inicie sesión en +++<https://copilotstudio.microsoft.com/>+++
    utilizando sus credenciales de inicio de sesión de Azure.

2.  Una vez que haya iniciado sesión, en la página Welcome to Microsoft
    Copilot Studio, seleccione su país y haga clic en **Start free
    trial.**

![](./media/image88.png)

3.  Se abre la página de inicio de Copilot.

> ![](./media/image89.png)

4.  Seleccione **Agents** en el panel izquierdo. A continuación, haga
    clic en **+ New agent**.

> ![](./media/image90.png)

5.  Seleccione **Skip to configure**.

![](./media/image91.png)

6.  En la página Create a copilot, ingrese el **nombre** como
    +++**CopilotforAOAI**+++ y haga clic en **Create**.

![](./media/image92.png)

7.  Haga clic en **Topics -\> System -\> Conversational boosting**.

> ![](./media/image93.png)

8.  Haga clic en **Edit** en **Data sources** del nodo **Create
    generative answers**. Seleccione **Classic data** en el panel
    **Properties** que se abre.

> ![A screenshot of a computer Description automatically
> generated](./media/image94.png)

9.  En **Azure OpenAI Services on your data**, haga clic en **Connection
    properties**.

> ![](./media/image95.png)

10. Esto añade la conexión del servicio Azure OpenAI y abre el panel de
    propiedades de la conexión.

11. En el panel **Connection Properties**, en **General -\>
    Configuration**, complete los siguientes datos:

> Deployment – +++gpt-4 +++
>
> Api version – Seleccione la última versión
>
> ![](./media/image96.png)

12. En la pestaña **Model data**, haga clic en **+ Add** en Data sources
    y, a continuación, agregue los siguientes datos.

Index name - +++copilot-index+++

Content data – +++content+++

![](./media/image97.png)

13. Haga clic en **Save**.

![](./media/image98.png)

**Tarea 3: Pruebe el Copilot**

1.  Haga clic en **Test** para abrir el panel **Test your Copilot**.

![](./media/image99.png)

2.  Escriba +++What is Azure OpenAI?+++ y haga clic en **Send**.

![](./media/image100.png)

3.  Recibirá la respuesta de los datos cargados en **Azure OpenAI
    resource**. Además, observe que el mensaje **Surfaced with Azure
    OpenAI** aparece debajo de la respuesta.

![](./media/image101.png)

**Tarea 4: Elimine los recursos**

1.  Para eliminar la cuenta de almacenamiento, vaya a la página de
    inicio del portal de Azure, escriba **Resource groups** en la barra
    de búsqueda del portal de Azure, navegue y haga clic en **Resource
    groups** en **Services.**

![](./media/image102.png)

2.  Haga clic en el grupo de recursos asignado.

![](./media/image103.png)

3.  Seleccione cuidadosamente todos los recursos que ha creado.

![](./media/image104.png)

4.  En la página del grupo de recursos, vaya a la barra de comandos y
    haga clic en **Delete**.

**Nota importante:** No haga clic en **Delete resource group**. Si no ve
la opción **Delete** en la barra de comandos, haga clic en la elipsis
horizontal.

![](./media/image105.png)

5.  En el panel **Delete Resources** que aparece a la derecha, ingrese
    **delete** y haga clic en el botón **Delete.**

![](./media/image106.png)

6.  En el cuadro de diálogo **Delete confirmation**, haga clic en el
    botón **Delete**.

![](./media/image107.png)

7.  Haga clic en el icono de la campana, allí verá la notificación -
    **Executed delete command on 4 selected items**.

**Resumen**

Se ha creado una cuenta de almacenamiento, un contenedor y un servicio
cognitivo de Azure en el portal de Azure. Posteriormente, se desplegó el
modelo gpt-3-turbo en Azure AI Studio. Se añadieron datos en Chat
Playground y se probó la configuración del asistente enviando consultas
en una sesión de chat. A continuación, se lanzó una nueva aplicación y
se inició una conversación con el chatbot. Finalmente, se eliminaron el
modelo gpt-3-turbo, la cuenta de almacenamiento de Azure, el servicio de
búsqueda cognitiva y la nueva aplicación web para gestionar de manera
eficiente los recursos de Azure OpenAI.
