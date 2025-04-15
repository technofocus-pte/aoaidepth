**Caso de uso 01- Análisis de tendencias de moda con GPT-4 Turbo y
Vision en Azure OpenAI**

**Introducción:**

GPT-4 Turbo con Visión en el servicio Azure OpenAI ya está en vista
previa pública. GPT-4 Turbo con Vision es un gran modelo multimodal
(LMM) desarrollado por OpenAI que puede analizar imágenes y proporcionar
respuestas textuales a preguntas sobre ellas. Incorpora tanto el
procesamiento del lenguaje natural como la comprensión visual. Con el
modo mejorado, puede utilizar las funciones de Azure AI Vision para
generar conocimientos adicionales a partir de las imágenes

**Objetivos:**

- Para implementar recursos Azure OpenAI y configurarlos.

- Implementar un modelo específico de Azure OpenAI como GPT-4 Vision.

- Configurar el entorno de desarrollo con Python, Jupyter Notebook y las
  bibliotecas necesarias.

- Este caso de uso está relacionado con los casos de uso de la moda.
  Pueden incluir análisis de imágenes, generación de texto u otras
  tareas de IA.

## Tarea 0: Conozca la máquina virtual y las credenciales

1\. En esta tarea, identificaremos y comprenderemos las credenciales que
utilizaremos a lo largo del laboratorio.

1.  La pestaña instrucciones contiene la guía del laboratorio con las
    instrucciones a seguir a lo largo del mismo.

2.  La pestaña recursos contiene las credenciales necesarias para
    ejecutar el laboratorio.

    - **URL** – URL del portal Azure.

    - **Subscription** – Este es el ID de la suscripción que se le ha
      asignado.

    - **Username** – El identificador de usuario con el que debe iniciar
      sesión en los servicios Azure.

    - **Password** – Contraseña para el inicio de sesión de Azure. Vamos
      a llamar a este nombre de usuario y contraseña como credenciales
      de inicio de sesión de Azure. Utilizaremos estas credenciales
      siempre que mencionemos las credenciales de inicio de sesión de
      Azure.

    - **Resource Group** – El **grupo de recursos** que se le ha
      asignado.

\[!Alerta\] **Importante:**  Asegúrese de crear todos sus recursos en
este grupo de recursos.

> ![](./media/image1.png)

2\. La pestaña **Help** contiene la información de Soporte. El valor
**ID** es el **Lab instance ID** que se utilizará durante la ejecución
del laboratorio.

> ![](./media/image2.png)

##  Tarea 1: Registre el proveedor de servicios 

1.  Abra un navegador, vaya a +++https://portal.azure.com+++ e inicie
    sesión con su cuenta de Cloud Slice a continuación:

> Usuario: <+++@lab.CloudPortalCredential>(User1).Username+++
>
> Contraseña: +++
>
> ![A screenshot of a computer Description automatically
> generated](./media/image3.png)
>
> ![A screenshot of a login box Description automatically
> generated](./media/image4.png)

2.  Haga clic en **Subscriptions.** 

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

3.  Haga clic en el nombre de la suscripción.

> ![](./media/image6.png)

4.  Expanda la configuración en el menú de navegación izquierdo. Haga
    clic en **Resource providers**, ingrese
    +++Microsoft.AlertsManagement+++ y selecciónelo. A continuación,
    haga clic en **Register**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

5.  Haga clic en **Resource providers**, ingrese
    +++**Microsoft.DBforPostgreSQL**+++ selecciónelo y, a continuación,
    haga clic en **Register.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

6.  Repita los pasos 10 y 11 para registrar los siguientes proveedores
    de recursos.

- Microsoft.Search

- Microsoft.Web

- Microsoft.ManagedIdentity

## **Tarea 2: Cree un recurso Azure OpenAI**

1.  En el portal Azure, haga clic en el **menú del portal** representado
    por tres barras horizontales en la esquina superior izquierda de la
    página, como se muestra en la siguiente imagen.

> ![A screenshot of a computer Description automatically
> generated](./media/image13.png)

2.  Navegue y haga clic en **+ Create a resource**.

> ![A screenshot of a computer Description automatically
> generated](./media/image14.png)

3.  En la página **Crear un recurso**, en la barra de búsqueda **Search
    services and marketplace**, escriba **Azure OpenAI** y, a
    continuación, pulse el botón **Intro**.

> ![A screenshot of a computer Description automatically
> generated](./media/image15.png)

4.  En la página **Marketplace**, navegue hasta el mosaico **Azure
    OpenAI**, haga clic en el botón con forma de V situado junto a
    **Create** y, a continuación, navegue y haga clic en **Azure
    OpenAI,** como se muestra en la siguiente imagen.

> ![](./media/image16.png)

5.  En la ventana **Create Azure OpenAI**, en la pestaña **Basics**,
    ingrese los siguientes datos y haga clic en el botón **Next.**

    1.  **Subscription**: Seleccione la suscripción asignada.

    2.  **Resource group:** Seleccione el grupo de recursos asignado

    3.  Para este laboratorio, utilizará un modelo **gpt-4-vision**.
        Este modelo sólo está disponible en [algunas
        regiones](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models).
        Por favor, seleccione una región de esta lista, En este
        laboratorio **Sweden Central,** se está utilizando para este
        recurso.

    4.  **Name**: **aoai-gpt4-visionXXXXX** (XXXXX puede ser el **Lab
        instance ID**)

    5.  **Pricing tier**: Seleccione **Standard S0**

> **Nota**: Para encontrar el **Lab instance ID**, seleccione **Help** y
> copie el **instance ID** .
>
> .
>
> ![A screenshot of a computer Description automatically
> generated](./media/image17.png)
>
> ![](./media/image18.png)
>
> ![](./media/image19.png)

6.  En la pestaña **Network**, deje todos los botones de opción en el
    estado predeterminado y haga clic en el botón **Next.**

> ![A screenshot of a computer Description automatically
> generated](./media/image20.png)

7.  En la pestaña **Tags**, deje todos los campos en el estado
    predeterminado y haga clic en el botón **Next.**

> ![A screenshot of a computer Description automatically
> generated](./media/image21.png)

8.  En la pestaña **Review + submit**, una vez superada la validación,
    haga clic en el botón **Create.**

> ![](./media/image22.png)

9.  Espere a que se complete la implementación. La instalación tardará
    unos 2-3 minutos.

10. En la ventana **Microsoft.CognitiveServicesOpenAI**, una vez
    finalizada la implementación, haga clic en el botón **Go to
    resource.**

> ![](./media/image23.png)

11. Haga clic en **Keys and Endpoints** en el menú de navegación de la
    izquierda y, a continuación, copie el valor del endpoint en un bloc
    de notas en **AzureAI ENDPOINT** y la clave en una variable
    **AzureAIKey.**

> ![](./media/image24.png)

12. En la ventana **aoai-gpt4-visionXX**, haga clic en **Overview** en
    el menú de navegación de la izquierda, desplácese hacia abajo hasta
    el mosaico **Get Started** y haga clic en el botón **Go to
    AzureOpenAI Studio** como se muestra en la siguiente imagen para
    abrir **Azure OpenAI Studio** en un nuevo navegador.

![](./media/image25.png)

## **Tarea 3: Implemente un modelo Azure OpenAI gpt-4-vision** 

1.  En la página de inicio de **Azure AI Foundry | Azure Open AI
    Service**, vaya a la sección **Components** y haga clic en
    **Deployments**.

2.  En la ventana **Deployments,** implemente el +**Deploy model** y
    seleccione **Deploy base** **model.**

![](./media/image26.png)

3.  En el cuadro de diálogo, **Seleccione un modelo**, navegue y
    seleccione cuidadosamente **gpt-4,** después haga clic en el botón
    **Confirm.**

![](./media/image27.png)

4.  En el cuadro de diálogo **Deploy model gpt-4**, en el campo
    **Deployment name**, asegúrese de que **gpt-4**, seleccione el tipo
    de implementación como **Standard** y seleccione versión del modelo
    como Vision- preview. A continuación, haga clic en el botón
    **Deploy.**

![](./media/image28.png)

![](./media/image29.png)

## Tarea 4: Demostración de GPT-4 Turbo con Vision

1.  En el cuadro de búsqueda de Windows, escriba **Visual Studio** y, a
    continuación, haga clic en **Visual Studio Code**.

> ![A screenshot of a computer Description automatically
> generated](./media/image30.png)

2.  En el editor de **Visual Studio Code**, haga clic en **File**, luego
    navegue y haga clic en **Open Folder**.

> ![A screenshot of a computer Description automatically
> generated](./media/image31.png)

3.  Navegue y seleccione la carpeta **GPT4V-Fashion** de **C:\LabFiles**
    y haga clic en el botón **Select Folder.**

![](./media/image32.png)

4.  Si aparece un cuadro de diálogo - **Do you trust the authors of the
    files in this folder?**, a continuación, haga clic en **Yes, I trust
    the author**.

![A screenshot of a computer Description automatically generated with
medium confidence](./media/image33.png)

5.  En el menú desplegable Visual Studio Code **Gpt 4V-FASHION**, haga
    clic en el archivo **azure.env.**

![](./media/image34.png)

1.  Actualice los parámetros, sustituya **Azure OpenAI Endpoint, Azure
    OpenAI Key** (los valores que ha guardado en el bloc de notas en la
    **tarea 1**) y guarde el archivo.

![](./media/image35.png)

2.  En Visual Studio Code despliegue el **GPT 4V-FASHION** y seleccione
    **GPT-4** **with Vision demo with Azure Open AI** - **Fashion
    usecase.ipynb** notebook.

> ![](./media/image36.png)

3.  En la página principal del editor Visual Studio Code, desplácese
    hacia abajo hasta el encabezado **install requirements** y ejecute
    la primera celda. Si se le pide que seleccione el entorno,
    seleccione **Python Environments** como se muestra en la imagen.

> ![](./media/image37.png)
>
> ![](./media/image38.png)

4.  Si se le pide que seleccione la ruta, seleccione la ruta de **Python
    version 3.11.5** como se muestra en la imagen.

> ![](./media/image39.png)

5.  Si aparece un cuadro de diálogo de alerta de seguridad de Windows,
    haga clic en **Allow access**.

> ![](./media/image40.png)
>
> ![](./media/image41.png)
>
> ![](./media/image42.png)
>
> ![](./media/image43.png)

6.  Para reiniciar el núcleo Jupyter, haga clic en el botón **Restart**.

> ![](./media/image44.png)

7.  Para importar las bibliotecas, seleccione la celda número **4**. A
    continuación, ejecute la celda haciendo clic en el botón **start
    icon**.

> ![](./media/image45.png)

8.  Seleccione la celda número **5**. A continuación, ejecute la celda
    haciendo clic en el botón **start icon**.

> ![](./media/image46.png)

9.  Para verificar las versiones del sistema OpenAI, seleccione las
    celdas **6**, **7, 8** y **9**.

A continuación, ejecute las celdas haciendo clic en el botón **start
icon**.

> ![](./media/image47.png)

10. Para cargar los valores de configuración, seleccione y ejecute las
    celdas **10**, **11** y **12** haciendo clic en el botón **Play.**

> ![A screenshot of a computer program Description automatically
> generated](./media/image48.png)

11. Defina una función de ayuda para crear embeddings, seleccione y
    ejecute las celdas 13 y 14 haciendo clic en el botón **Play.**

> ![](./media/image49.png)
>
> ![](./media/image50.png)

12. Para ejecutar el ejemplo, seleccione y ejecute las celdas 15 y 16,
    haciendo clic en el botón **Play.**

> ![](./media/image51.png)
>
> ![](./media/image52.png)

13. Para ejecutar el ejemplo, seleccione y ejecute las celdas **17** y
    **18,** haciendo clic en el botón **Play.**

> ![](./media/image53.png)
>
> ![](./media/image54.png)

14. Para ejecutar el ejemplo, seleccione y ejecute las celdas **19** y
    **20,** haciendo clic en el botón **Play.**

> ![](./media/image55.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image56.png)

15. Para ejecutar el ejemplo, seleccione y ejecute las celdas **21** y
    **22,** haciendo clic en el botón **Play.**

> ![](./media/image57.png)
>
> ![](./media/image58.png)

16. Para ejecutar el ejemplo, seleccione y ejecute las celdas **23** y
    **24,** haciendo clic en el botón **Play.**

> ![](./media/image59.png)

![](./media/image60.png)

17. Para ejecutar el ejemplo, seleccione y ejecute las celdas **25** y
    **26,** haciendo clic en el botón **Play.**

> ![](./media/image61.png)
>
> ![](./media/image62.png)

18. Para ejecutar el ejemplo, seleccione y ejecute las celdas **27** y
    **28,** haciendo clic en el botón **Play**.

> ![](./media/image63.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image64.png)

19. Para ejecutar el ejemplo, seleccione y ejecute las celdas **29** y
    **30,** haciendo clic en el botón **Play**.

> ![](./media/image65.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image66.png)

20. Para generar la WebApp, seleccione y ejecute la **29** celda,
    haciendo clic en el botón **Play**.

> ![](./media/image67.png)

21. Para generar la WebApp, seleccione y ejecute la celda **30,**
    haciendo clic en el botón **Play.**

> ![](./media/image68.png)

22. Cuando la aplicación se haya desplegado correctamente, verá una URL
    en la terminal. Copie la **URL.**

![](./media/image69.png)

23. Abra su navegador, vaya a la barra de direcciones y pegue el enlace
    URL de Publick. ![](./media/image70.png)

24. Abra su navegador, vaya a la barra de direcciones y pegue el enlace
    URL local. Seleccione cualquier elemento.

![](./media/image71.png)

25. Haga clic en el botón **Submit.**

> ![](./media/image72.png)

![](./media/image73.png)

## Tarea 5: Elimine los recursos

1.  Para eliminar la cuenta de almacenamiento, vaya a la **página de
    inicio del portal Azure** y haga clic en **Resource groups.**

> ![A screenshot of a computer Description automatically
> generated](./media/image74.png)

2.  Haga clic en el grupo de recursos **ResourceGroup1.**

> ![](./media/image75.png)

3.  En la página de inicio del **grupo de recursos**, seleccione
    **delete resource group.**

![](./media/image76.png)

4.  En el panel **Delete Resources** que aparece a la derecha,
    desplácese hasta el campo **Enter “resource group name” to confirm
    deletion** para confirmar la eliminación y, a continuación, haga
    clic en el botón **Delete**.

![](./media/image77.png)

5.  En el cuadro de diálogo **Delete confirmation**, haga clic en el
    botón **Delete**.

> ![](./media/image78.png)

6.  Haga clic en el icono de la campana, verá la notificación –**Deleted
    resource group AOAI-RG89.**

![A screenshot of a computer Description automatically
generated](./media/image79.png)

**Resumen**

En este laboratorio práctico, los participantes exploran las capacidades
avanzadas de IA mediante Azure OpenAI. Comenzando con la configuración
de los recursos esenciales de Azure, se despliegan modelos de IA como
GPT-4-vision. El laboratorio se enfoca específicamente en cómo GPT-4,
con capacidades de visión, puede transformar las tareas relacionadas con
la moda, tales como el reconocimiento de imágenes, las recomendaciones
de estilo personalizadas y el análisis de tendencias.
