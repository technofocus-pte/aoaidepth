**Caso de uso 05 - Implementar y probar una solución de IA
conversacional con el acelerador Azure RAG**

**Introducción**

El acelerador de solución "Chat with your data" es una herramienta
poderosa que combina las capacidades de Azure AI Search y los Modelos de
Lenguaje Grande (LLMs) para crear una experiencia de búsqueda
conversacional.

Este acelerador de solución utiliza un modelo GPT de Azure OpenAI y un
índice de Azure AI Search generado a partir de sus datos, que se integra
en una aplicación web para proporcionar una interfaz de lenguaje
natural, incluida la funcionalidad de conversión de voz a texto, para
las consultas de búsqueda. Los usuarios pueden arrastrar y soltar
archivos, apuntar a almacenamiento y realizar la configuración técnica
para transformar documentos. Existe una aplicación web que los usuarios
pueden crear en su propia suscripción con seguridad y autenticación.

Los datos de muestra ilustran cómo este acelerador podría utilizarse en
la industria de servicios financieros (FSI).

En este escenario, un asesor financiero se está preparando para una
reunión con un cliente potencial que ha expresado interés en los fondos
de mercados emergentes de Woodgrove Investments. El asesor se prepara
para la reunión refrescando su comprensión de los objetivos generales de
los fondos de mercados emergentes y los riesgos asociados.

Ahora que el asesor financiero está más informado sobre los fondos de
mercados emergentes de Woodgrove, está mejor preparado para responder a
preguntas sobre este fondo de su cliente.

Nota: Algunos de los datos de muestra incluidos con este acelerador
fueron generados utilizando IA y son solo para fines ilustrativos.

En este caso de uso, implementará y probará una solución de IA
conversacional utilizando el Acelerador Azure RAG (Retrieval-Augmented
Generation). Esta solución aprovecha las potentes capacidades de IA de
Azure, que incluyen Azure OpenAI y Azure AI Search, para crear una
experiencia avanzada de búsqueda conversacional. Al final de este
laboratorio, tendrá una aplicación web completamente funcional que
utiliza procesamiento de lenguaje natural para interactuar y consultar
sus datos. Los pasos prácticos lo guiarán a través de la implementación
de la infraestructura necesaria, la verificación de los recursos, la
prueba de la solución y la limpieza del entorno. ![A computer screen
shot of a diagram AI-generated content may be
incorrect.](./media/image1.png)

**Objetivos**

- Implementar la infraestructura necesaria desde una plantilla
  personalizada en el portal de Azure.

- Verificar que todos los recursos Azure necesarios se han implementado
  correctamente.

- Probar la funcionalidad de la solución implementada cargando y
  procesando documentos e interactuando con la aplicación web.

- Eliminar los recursos y modelos implementados.

**Tarea 1: Implementar la infraestructura a partir de una plantilla**

1.  Abra su navegador, vaya a la barra de direcciones y escriba o pegue
    la siguiente URL: +++www.portal.azure.com/+++ y pulse el botón
    **Enter.**

2.  En la ventana de **Microsoft Azure**, ingrese sus credenciales de
    **inicio de sesión** y haga clic en el botón **Next**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)

3.  A continuación, ingrese la contraseña y haga clic en el botón **Sign
    in**\*\*.\*\*

> ![A screenshot of a login box AI-generated content may be
> incorrect.](./media/image3.png)

4.  En la ventana **Stay signed in?**, haga clic en el botón **Yes.**

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image4.png)

5.  Abra un nuevo navegador e ingrese la siguiente URL en la barra de
    direcciones:
    +++<https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json+++> para
    abrir el Portal Azure.

6.  En la ventana **Custom deployment**, en la pestaña **Basics**,
    ingrese los siguientes datos para implementar la plantilla
    personalizada y, a continuación, haga clic en **Review + create.**

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

7.  En la pestaña **Review + create**, una vez superada la validación,
    haga clic en el botón **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image6.png)

8.  Espere a que finalice la implementación. Este proceso tardará entre
    17 y 19 minutos.

9.  Haga clic en el botón **Go to Subscription**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

**Tarea 2: Verifique los recursos implementados en el portal Azure**

1.  En la página de inicio, haga clic en **Resource Groups**.

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image8.png)

2.  Haga clic en el nombre de su grupo de recursos **rg-RAGSolutionXX.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  Asegúrese de que el siguiente recurso se ha implementado
    correctamente en la región East US.

    - Azure App Service

    - Azure Application Insights

    - Azure Bot

    - Azure OpenAI

    - Azure Document Intelligence

    - Azure Function App

    - Azure Search Service

    - Azure Storage Account

    - Azure Speech Service

    - Azure Database for PostgreSQL - Flexible Server

    - Key vault

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

![](./media/image11.png) ![A screenshot of a computer AI-generated
content may be incorrect.](./media/image12.png)

**Tarea 3: Verifique la implementación**

1.  En el grupo de recursos, haga clic en el nombre del recurso **Web-
    {RESOURCE_TOKEN} - admin-docker.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)

2.  Navegue hasta el sitio de administración

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image14.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

3.  En la página **Chat with your data Solution Accelerator**, en el
    menú de navegación de la izquierda seleccione **Ingest Data.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image16.png)

4.  En el panel **Add documents Batch**, haga clic en **Browse file** y
    vaya a la ubicación **C:\Labfiles \data** y seleccione **todos los
    archivos**, a continuación, haga clic en el botón **Open.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image17.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  La carga de archivos tardará entre 1 y 2 minutos.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

6.  Haga clic en **Reprocess all documents in the Azure Storage
    account.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image21.png)

7.  En la página **Chat with your data Solution Accelerator**, en el
    menú de navegación de la izquierda, seleccione **Configuration** y
    marque la casilla de verificación **Enable post-answering prompt.**
    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image22.png)

8.  En el panel de configuración, haga clic en el botón **Save
    configuration.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image23.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image24.png)

9.  Vuelva a la página del grupo de recursos y haga clic en el nombre de
    la cuenta de almacenamiento **Storage account**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

10. En el menú de navegación de la izquierda, haga clic en
    **Containers.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

11. En la página contenedores, seleccione **documents**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

12. Asegúrese de que todos los archivos deben ser implementados con
    éxito.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

13. Regrese a la página del grupo de recursos.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

14. En la página del grupo de recursos, seleccione App service como
    **web-{RESOURCE_TOKEN}-docker.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

15. En el menú desplegable de la izquierda, debajo de **Settings**,
    seleccione **Authentication.** ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image31.png)

16. Haga clic en Add identify provider. ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image32.png)

17. Seleccione **Microsoft** como proveedor de identidad, actualice el
    nombre como **web-XXXXX-docker-new**, seleccione **Client secret
    expiration duration** como 90 días y haga clic en **Next**:
    **Permissions**. ![A screenshot of a computer AI-generated content
    may be incorrect.](./media/image33.png)

18.  Haga clic en **Add permission**. Desplácese hacia abajo en la lista
    para expandir la aplicación y seleccione
    **Application.ReadWrite.All**. A continuación, haga clic en **Update
    permission**.

> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](./media/image34.png)

19. Ahora, haga clic en **Add.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image35.png)

20. Haga clic en la página de descripción general de la aplicación.
    Espere a que se cargue la página y haga clic en **Restart**.
    Confirme el reinicio haciendo clic en **Yes.** ![A screenshot of a
    computer AI-generated content may be
    incorrect.](./media/image36.png) ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image37.png)

21. En la página **Web App Overview**, navegue hasta la barra de
    comandos y haga clic en **Browse**; esto lo llevará a la aplicación
    web.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image38.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

22. En la página de la aplicación web **Azure AI**, ingrese el siguiente
    texto y haga clic en **Submit icon**, como se muestra en la
    siguiente imagen.

+++ Describa con más detalle los riesgos derivados de la volatilidad de
los mercados+++ 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png) 

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

17. En **Chat session**, seleccione el enlace de referencias y observe
    los detalles del documento de búsqueda en el lado derecho de la
    página.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

18. En la página de la aplicación web **Azure AI**, ingrese el siguiente
    texto y haga clic en **Submit icon** como se muestra en la siguiente
    imagen.

+++How does Woodgrove Financial handle payroll taxes for employees
outside the U.S.?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png) ![A screenshot of a chat AI-generated
content may be incorrect.](./media/image44.png)

19. En la página de la aplicación web **Azure AI**, ingrese el siguiente
    texto y haga clic en **Submit icon** como se muestra en la siguiente
    imagen.

+++What is FORM 10-K and explain?+++ 

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image45.png)

**Tarea 4: Elimine el recurso Azure OpenAI**

1.  Para eliminar el recurso Azure OpenAI, escriba **Resource
    groups** en la barra de búsqueda del portal Azure, navegue y haga
    clic en **Resource groups** bajo **Services.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

2.  Haga clic en su grupo de recursos.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

3.  En una página de resumen del grupo de recursos, seleccione **Delete
    resource group.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

4.  En el panel **Delete Resources** que aparece a la derecha, ingrese
    el **resource group name** y haga clic en el botón **Delete.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image48.png)

5.  En el cuadro de diálogo **Delete confirmation**, haga clic en el
    botón D**elete**.

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image49.png)

**Resumen**:

Este laboratorio proporcionó experiencia práctica en la implementación
de una solución de IA conversacional utilizando el Azure RAG
Accelerator. El laboratorio comenzó con la implementación de la
infraestructura requerida utilizando una plantilla personalizada.
Después de verificar la implementación exitosa de varios recursos de
Azure, se probó la solución subiendo documentos y utilizando la
aplicación web para realizar consultas y recuperar información.
Finalmente, se eliminó el grupo de recursos para gestionar los recursos
de manera eficiente. Este laboratorio demostró cómo mejorar la
interacción y recuperación de datos utilizando tecnologías avanzadas de
IA.

.
