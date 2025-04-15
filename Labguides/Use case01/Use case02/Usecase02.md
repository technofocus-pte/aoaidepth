Caso de uso 02: Integración de capacidades de IA generativa con Azure
Database for PostgreSQL Flexible Server para evaluar reseñas de listados
de IA específicos  
**Introducción**

En este laboratorio, aprenderá a integrar los servicios de Azure AI con
PostgreSQL para mejorar su base de datos con funcionalidades avanzadas
de IA. Al aprovechar el poder de Azure OpenAI y las extensiones de
PostgreSQL como pgvector y PostGIS, habilitará sofisticados análisis de
texto, búsquedas de similitud vectorial y consultas geoespaciales
directamente dentro de su base de datos. Este laboratorio le guiará a
través del aprovisionamiento de los recursos Azure necesarios, la
configuración de su base de datos y la ejecución de consultas complejas
que combinan conocimientos basados en IA con datos
geoespaciales.**Objetivos**

- Aprovisionar y configurar Azure Database for PostgreSQL Flexible
  Server.

- Crear y gestionar incrustaciones vectoriales utilizando el servicio
  Azure OpenAI.

- Realizar búsquedas de similitud vectorial para encontrar datos de
  texto semánticamente similares.

- Utilizar la extensión PostGIS para el análisis de datos geoespaciales.

- Integrar los servicios Azure AI Language para el análisis de
  sentiments y otras funciones cognitivas.

- Optimizar y analizar el rendimiento de las consultas mediante
  herramientas de indexación y planificación de consultas.

# Ejercicio 1: Aprovisionar una Azure Database for PostgreSQL Flexible Server

1.  

![](./media/image1.png)

## Tarea 1: Aprovisione una Azure Database for PostgreSQL Flexible Server

1.  Abra su navegador, vaya a la barra de direcciones y escriba o pegue
    la siguiente URL: +++https://portal.azure.com/+++, y, a
    continuación, pulse el botón **Enter**.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)

2.  En la ventana de **Microsoft Azure**, utilice las **User
    Credentials** para iniciar sesión en Azure.

![A screenshot of a computer Description automatically
generated](./media/image3.png)

3.  A continuación, ingrese la contraseña y haga clic en el botón **Sign
    in.**

> ![A screenshot of a login box Description automatically
> generated](./media/image4.png)

4.  En la ventana **Stay signed in?**, haga clic en el botón **Yes.**

> ![Graphical user interface, application Description automatically
> generated](./media/image5.png)

5.  Seleccione el icono **Cloud Shell** en la barra de herramientas del
    portal Azure para abrir un nuevo panel Cloud Shell en la parte
    superior de la ventana del navegador.

![](./media/image6.png)

6.  La primera vez que abra Cloud Shell, es posible que se le pida que
    elija el tipo de shell que desea utilizar (**Bash** o
    **PowerShell**). Seleccione **Bash.**

![](./media/image7.png)

7.  En el cuadro de diálogo **Getting started**, seleccione **Mount
    storage account** y seleccione su suscripción azure. Haga clic en el
    botón **Apply.**

![A screenshot of a computer Description automatically
generated](./media/image8.png)

8.  En el cuadro de diálogo **Mount storage account**, seleccione **we
    will create a storage account for you** y haga clic en el botón
    **Next.**

> ![](./media/image9.png)
>
> ![](./media/image10.png)

1.  En el cloud shell prompt, ejecute los siguientes comandos para
    definir variables para crear recursos. Las variables representan los
    nombres que se asignarán al grupo de recursos y a la base de datos,
    y especifican la región de Azure en la que se implementarán los
    recursos.

2.  El nombre del grupo de recursos especificado es
    **rg-postgresql-labs**, pero puede proporcionar cualquier nombre que
    desee utilizar para alojar los recursos asociados a este
    laboratorio.

> **+++RG_NAME=ResourceGroup1**
>
> ![A screenshot of a search engine Description automatically
> generated](./media/image11.png)

3.  En el nombre de la base de datos, sustituya el símbolo {SUFFIX} por
    un valor único, como sus iniciales, para garantizar que el nombre
    del servidor de la base de datos sea único en todo el mundo.

> **+++DATABASE_NAME=pgsql-flex-{SUFFIX}+++**

4.  Sustituya la región por la ubicación que desee utilizar para los
    recursos del laboratorio.

> **+++REGION=eastus2+++**

![A screenshot of a computer Description automatically
generated](./media/image12.png)

5.  Aprovisione una instancia de base de datos Azure Database for
    PostgreSQL dentro del grupo de recursos que creó anteriormente
    ejecutando el siguiente comando Azure CLI (10 Min).

**az postgres flexible-server create --name $DATABASE_NAME --location
$REGION --resource-group $RG_NAME \\**

**--admin-user s2admin --admin-password Seattle123Seattle123
--database-name airbnb \\**

**--public-access 0.0.0.0-255.255.255.255 --version 16 \\**

**--sku-name Standard_D2s_v3 --storage-size 32 --yes**

![A screenshot of a computer program Description automatically
generated](./media/image13.png)

## Tarea 2: Conéctese a la base de datos mediante psql en Azure Cloud Shell

En esta tarea, utilizará la utilidad de línea de comandos psql de Azure
Cloud Shell para conectarse a su base de datos.

1.  Abra un navegador, vaya a <https://portal.azure.com> e inicie sesión
    con su cuenta de suscripción a Azure.

2.  En la página de inicio, haga clic en **Resource Groups**.

![](./media/image14.png)

3.  Haga clic en el nombre de su grupo de recursos.

> ![](./media/image15.png)

4.  En el grupo de recursos, seleccione el recurso **PostgreSQL Flexible
    Server**.

![](./media/image16.png)

5.  En el menú de navegación de la izquierda, seleccione **Connect** en
    **Settings.**

![](./media/image17.png)

6.  En la página **Connect** de la base de datos del portal Azure,
    seleccione **airbnb** como **Database name** y, a continuación,
    copie el bloque **Connection details** y péguelo en el bloc de notas
    para utilizar la información en las tareas siguientes.

> ![](./media/image18.png)

7.  En la página de inicio de Azure Database for PostgresSQL, haga clic
    en **Overview** en el menú de navegación de la izquierda y copie el
    nombre del servidor y póngalo en el bloc de notas, a continuación,
    **guarde** el bloc de notas para utilizar la información en el
    próximo laboratorio.

![](./media/image19.png)

8.  En la página de inicio de Azure Database for PostgreSQL, seleccione
    **Networking** en **settings** y seleccione **Allow public access to
    this resource through the internet using a public IP address**. Haga
    clic en el botón **Save.**

![](./media/image20.png)

![](./media/image21.png)

9.  Seleccione el icono **Cloud Shell** en la barra de herramientas del
    portal Azure para abrir un nuevo panel Cloud Shell en la parte
    superior de la ventana del navegador.

10. Pegue los **detalles de la conexión** en Cloud Shell.

![The Connection strings page of the Azure Cosmos DB Cluster resource is
highlighted. On the Connection strings page, the copy to clipboard
button to the right of the psql connection string is
highlighted.](./media/image22.png)

![A screenshot of a computer screen Description automatically
generated](./media/image23.png)

11. En el Cloud Shell prompt, sustituya el token **{your_password}** por
    la contraseña que asignó al usuario **s2admin** al crear su base de
    datos, la contraseña debe ser **Seattle123Seattle123**.

> ![](./media/image24.png)

12. Conéctese a su base de datos utilizando la utilidad de línea de
    comandos psql ingresando el siguiente prompt:

> **+++psql+++**

![A black background with a black square Description automatically
generated with medium confidence](./media/image25.png)

La conexión a la base de datos desde Cloud Shell requiere que la casilla
Allow public access from any Azure service within Azure to the server
esté marcada en la página de **Networking** de la base de datos. Si
recibe un mensaje que le indica que no puede conectarse, compruebe que
esta casilla está marcada e inténtelo de nuevo.

## Tarea 3: Añada datos a la base de datos

Utilizando el psql command prompt, creará tablas y las completará con
datos para su uso en el laboratorio.

1.  Ejecute los siguientes comandos para crear tablas temporales para
    importar datos JSON desde una cuenta de almacenamiento blob pública.

> !!CREATE TABLE temp_calendar (data jsonb);
>
> CREATE TABLE temp_listings (data jsonb);
>
> CREATE TABLE temp_reviews (data jsonb);!!

![](./media/image26.png)

2.  Utilizando el comando COPY, rellene cada tabla temporal con datos de
    archivos JSON en una cuenta de almacenamiento público.

+++\COPY temp_calendar (data) FROM PROGRAM 'curl
https://solliancepublicdata.blob.core.windows.net/ms-postgresql-labs/calendar.json'+++

!!\COPY temp_listings (data) FROM PROGRAM 'curl
https://solliancepublicdata.blob.core.windows.net/ms-postgresql-labs/listings.json'!!

\COPY temp_reviews (data) FROM PROGRAM 'curl
https://solliancepublicdata.blob.core.windows.net/ms-postgresql-labs/reviews.json'

![](./media/image27.png)

![](./media/image28.png)

3.  Ejecute el siguiente comando para crear las tablas necesarias para
    almacenar los datos en el formato utilizado en este laboratorio:

> CREATE TABLE listings (
>
> listing_id int,
>
> name varchar(50),
>
> street varchar(50),
>
> city varchar(50),
>
> state varchar(50),
>
> country varchar(50),
>
> zipcode varchar(50),
>
> bathrooms int,
>
> bedrooms int,
>
> latitude decimal(10,5),
>
> longitude decimal(10,5),
>
> summary varchar(2000),
>
> description varchar(2000),
>
> host_id varchar(2000),
>
> host_url varchar(2000),
>
> listing_url varchar(2000),
>
> room_type varchar(2000),
>
> amenities jsonb,
>
> host_verifications jsonb,
>
> data jsonb
>
> );
>
> ![](./media/image29.png)
>
> CREATE TABLE reviews (
>
> id int,
>
> listing_id int,
>
> reviewer_id int,
>
> reviewer_name varchar(50),
>
> date date,
>
> comments varchar(2000)
>
> );
>
> CREATE TABLE calendar (
>
> listing_id int,
>
> date date,
>
> price decimal(10,2),
>
> available boolean
>
> );
>
> ![](./media/image30.png)

4.  Por último, ejecute las siguientes sentencias INSERT INTO para
    cargar los datos de las tablas temporales en las tablas principales,
    extrayendo los datos del campo de datos JSON en columnas
    individuales:

> INSERT INTO listings
>
> SELECT
>
> data\['id'\]::int,
>
> replace(data\['name'\]::varchar(50), '"', ''),
>
> replace(data\['street'\]::varchar(50), '"', ''),
>
> replace(data\['city'\]::varchar(50), '"', ''),
>
> replace(data\['state'\]::varchar(50), '"', ''),
>
> replace(data\['country'\]::varchar(50), '"', ''),
>
> replace(data\['zipcode'\]::varchar(50), '"', ''),
>
> data\['bathrooms'\]::int,
>
> data\['bedrooms'\]::int,
>
> data\['latitude'\]::decimal(10,5),
>
> data\['longitude'\]::decimal(10,5),
>
> replace(data\['description'\]::varchar(2000), '"', ''),
>
> replace(data\['summary'\]::varchar(2000), '"', ''),
>
> replace(data\['host_id'\]::varchar(50), '"', ''),
>
> replace(data\['host_url'\]::varchar(50), '"', ''),
>
> replace(data\['listing_url'\]::varchar(50), '"', ''),
>
> replace(data\['room_type'\]::varchar(50), '"', ''),
>
> data\['amenities'\]::jsonb,
>
> data\['host_verifications'\]::jsonb,
>
> data::jsonb
>
> FROM temp_listings;
>
> INSERT INTO reviews
>
> SELECT
>
> data\['id'\]::int,
>
> data\['listing_id'\]::int,
>
> data\['reviewer_id'\]::int,
>
> replace(data\['reviewer_name'\]::varchar(50), '"', ''),
>
> to_date(replace(data\['date'\]::varchar(50), '"', ''), 'YYYY-MM-DD'),
>
> replace(data\['comments'\]::varchar(2000), '"', '')
>
> FROM temp_reviews;
>
> INSERT INTO calendar
>
> SELECT
>
> data\['listing_id'\]::int,
>
> to_date(replace(data\['date'\]::varchar(50), '"', ''), 'YYYY-MM-DD'),
>
> data\['price'\]::decimal(10,2),
>
> replace(data\['available'\]::varchar(50), '"', '')::boolean
>
> FROM temp_calendar;

![](./media/image31.png)

# Ejercicio 2: Agregar las extensiones Azure AI y Vector a la lista de permitidos

A lo largo de este laboratorio, se utilizan las extensiones azure_ai y
pgvector para agregar capacidades de IA generativa a la base de datos
PostgreSQL. En este ejercicio, agregue estas extensiones a la lista de
permisos del servidor, según lo descrito en la guía sobre el uso de
extensiones en PostgreSQL.

1.  En la página de inicio, haga clic en **Resource Groups**.

![](./media/image32.png)

2.  Haga clic en el nombre de su grupo de recursos.

> ![](./media/image33.png)

3.  En el grupo de recursos, seleccione el recurso **Servidor flexible
    PostgreSQL.**

![](./media/image34.png)

4.  En el menú de navegación izquierdo de la base de datos, seleccione
    **Server parameters** en **Settings** y, a continuación, ingrese
    azure.extensions en el cuadro de búsqueda. Expanda la lista
    desplegable **VALUE** y, a continuación, localice y marque la
    casilla situada junto a cada una de las siguientes extensiones:

    - AZURE_AI

    - POSTGIS (Tenga en cuenta que esto ya estará marcado si ha
      completado el laboratorio 3).

    - VECTOR

![](./media/image35.png)

![](./media/image36.png)

![](./media/image37.png)

5.  Seleccione **Save** en la barra de herramientas, lo que activará una
    implementación en la base de datos.

![](./media/image38.png)

![A screenshot of a computer Description automatically
generated](./media/image39.png)

# Ejercicio 3: Crear un recurso Azure OpenAI

La extensión azure_ai requiere un servicio Azure OpenAI subyacente para
crear embeddings vectoriales. En este ejercicio, se aprovisionará un
recurso Azure OpenAI en el portal Azure y se implementará un modelo de
embedding en ese servicio.

## Tarea 1: Aprovisione un servicio Azure OpenAI

En esta tarea, se crea un nuevo servicio Azure OpenAI.

1.  En la página de inicio del portal Azure, haga clic en el menú del
    **portal Azure**, representado por tres barras horizontales en la
    parte izquierda de la barra de comandos de Microsoft Azure, como se
    muestra en la siguiente imagen.

> ![A screenshot of a computer Description automatically
> generated](./media/image40.png)

2.  Navegue y haga clic en **+ Create a resource**.

> ![A screenshot of a computer Description automatically
> generated](./media/image41.png)

3.  En la página **Create a resource**, en la barra de búsqueda **Search
    services and marketplace**, escriba **Azure OpenAI** y, a
    continuación, pulse el botón **Enter**.

> ![A screenshot of a computer Description automatically
> generated](./media/image42.png)

4.  En la página del Marketplace, vaya a la sección **Azure OpenAI**,
    haga clic en el menú desplegable del botón **Create** y seleccione
    **Azure OpenAI**, como se muestra en la imagen. (Si ya ha
    seleccionado el mosaico de **Azure OpenAI**, haga clic en el botón
    **Create** en la página de **Azure OpenAI**).

> ![](./media/image43.png)

5.  En la pestaña **Create Azure OpenAI** **Basics**, ingrese la
    siguiente información y haga clic en el botón **Next.**

[TABLE]

> ![A screenshot of a computer Description automatically
> generated](./media/image44.png)

6.  En la pestaña **Network**, deje todos los botones de opción en el
    estado predeterminado y haga clic en el botón **Next.**

> ![](./media/image45.png)

7.  En la pestaña **Tags**, deje todos los campos en estado
    predeterminado, y haga clic en el botón **Next.**

> ![](./media/image46.png)

8.  En la pestaña **Review+submit**, una vez superada la validación,
    haga clic en el botón **Create.**

![A screenshot of a computer Description automatically
generated](./media/image47.png)

9.  Espere a que la implementación se complete. Este proceso tomará
    aproximadamente 2-3 minutos.

> **Nota:** Si aparece un mensaje indicando que el servicio Azure OpenAI
> está disponible solo mediante un formulario de solicitud y que la
> suscripción seleccionada no está habilitada ni tiene cuota para ningún
> nivel de precios, haga clic en el enlace para solicitar acceso al
> servicio y complete el formulario de solicitud.

## Tarea 2: Recupere la clave y el endpoint del servicio Azure OpenAI

1.  En la página **Overview** del recurso, seleccione el botón **Go to
    resource**. Si se le solicita, seleccione las credenciales del
    laboratorio.

![](./media/image48.png)

2.  En la ventana **Azure OpenAI home**, vaya a la sección **Resource
    Management** y haga clic en **Keys and Endpoints**.

![](./media/image49.png)

3.  En la página **Keys and Endpoints**, copie los valores de **KEY1,
    KEY 2** y **Endpoint** y péguelos en un bloc de notas como se
    muestra en la siguiente imagen, luego guarde el bloc de notas
    haciendo clic en **save** para utilizar la información en las
    próximas tareas.

![](./media/image50.png)

![](./media/image51.png)

***Nota:** Puede utilizar KEY1 o KEY2. Disponer siempre de dos llaves le
permite rotar y regenerar llaves de forma segura sin causar una
interrupción del servicio*.

## Tarea 3: Implemente un modelo de embedding

La extensión azure_ai permite la creación de embeddings vectoriales a
partir de texto. Para generar estos embeddings, se requiere un modelo
text-embedding-ada-002 (versión 2) implementado en el servicio Azure
OpenAI. En esta tarea, se utilizará Azure OpenAI Studio para crear una
implementación del modelo, que posteriormente podrá emplearse.

1.  En la página **Azure OpenAI**, haga clic en **Overview** en el menú
    de navegación de la izquierda, desplácese hacia abajo y haga clic en
    el botón **Go to Azure OpenAI** **Studio** como se muestra en la
    siguiente imagen.

> ![](./media/image52.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image53.png)

2.  En la página de **Azure AI Foundry | Azure Open AI Service**, vaya a
    la sección **Components** y haga clic en **Deployments**.

3.  En la ventana **Deployments**, implemente el modelo + **Deploy
    model** y seleccione **Deploy base model.**

![](./media/image54.png)

4.  En el cuadro de diálogo **Select a model**, navegue y seleccione
    cuidadosamente **text-embedding-ada-002**, después haga clic en el
    botón **Confirm.**

![](./media/image55.png)

4.  En el cuadro de diálogo **Deploy model**, configure lo siguiente y
    seleccione **Create** para implementar el modelo.

    - **Seleccione un modelo**: Seleccione **text-embedding-ada-002** de
      la lista.

    - **Versión del modelo:** Asegúrese de que está seleccionada la
      opción 2 (Predeterminada).

    - **o Nombre la implementación:** Ingrese+++**embeddings**+++

> ![](./media/image56.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image57.png)

5.  En la ventana **Deployments**, copie el **Deployment name** y
    péguelo en un bloc de notas (como se muestra en la imagen) y, a
    continuación, haga clic en **Save,** para guardar el bloc de notas y
    utilizar la información en la siguiente tarea.

![](./media/image58.png)

# Ejercicio 4: Instalación y configuración de la extensión azure_ai

En este ejercicio, se instalará la extensión azure_ai en la base de
datos y se configurará para conectarse al servicio Azure OpenAI.

## Tarea 1: Conéctese a la base de datos utilizando psql en Azure Cloud Shell

En esta tarea, utilizará la utilidad de línea de comandos psql de Azure
Cloud Shell para conectarse a su base de datos.

1.  Seleccione el icono **Cloud Shell** en la barra de herramientas del
    portal Azure para abrir un nuevo panel Cloud Shell en la parte
    superior de la ventana del navegador.

2.  Pegue los **detalles de la conexión** en Cloud Shell.

![The Connection strings page of the Azure Cosmos DB Cluster resource is
highlighted. On the Connection strings page, the copy to clipboard
button to the right of the psql connection string is
highlighted.](./media/image22.png)

3.  En el indicador Cloud Shell, sustituya el token **{your_password}**
    por la contraseña que asignó al usuario **s2admin** al crear su base
    de datos, la contraseña debe ser **Seattle123Seattle123.**

![A screenshot of a computer Description automatically
generated](./media/image24.png)

4.  Conéctese a su base de datos utilizando la utilidad de línea de
    comandos psql ingresando lo siguiente en la línea de prompt:

> **!!psql!!**

![A black background with a black square Description automatically
generated with medium confidence](./media/image25.png)

## Tarea 2: Instalación de la extensión azure_ai

La extensión azure_ai te permite integrar Azure OpenAI y Azure Cognitive
Services en su base de datos. Para habilitar la extensión en su base de
datos, siga estos pasos:

1.  Compruebe que la extensión se ha añadido correctamente a la lista
    permitida ejecutando lo siguiente desde el símbolo del sistema psql:

> **!!SHOW azure.extensions;!!**

![](./media/image59.png)

2.  Instale la extensión azure_ai utilizando el comando CREATE
    EXTENSION.

> **!!CREATE EXTENSION IF NOT EXISTS azure_ai;!!**

![](./media/image60.png)

## Tarea 3: Revise los objetos contenidos en la extensión azure_ai

La revisión de los objetos dentro de la extensión azure_ai puede
proporcionar una mejor comprensión de sus capacidades. En esta tarea, se
inspeccionan los distintos esquemas, funciones definidas por el usuario
(UDF) y tipos compuestos añadidos a la base de datos por la extensión.

1.  Puede utilizar el metacomando \dx desde la línea de comandos
    **psql** para listar los objetos contenidos en la extensión.

> **+++\dx+ azure_ai+++**
>
> ![](./media/image61.png)
>
> ![A screenshot of a computer program Description automatically
> generated](./media/image62.png)
>
> Los resultados del metacomando muestra que la extensión azure_ai crea
> tres esquemas, múltiples funciones definidas por el usuario (UDF) y
> varios tipos compuestos en la base de datos. La siguiente tabla
> enumera los esquemas añadidos por la extensión y describe cada uno de
> ellos.

[TABLE]

2.  Las funciones y tipos están asociados a uno de los esquemas. Para
    revisar las funciones definidas en el esquema azure_ai, utilice el
    meta-comando \df, especificando el esquema cuyas funciones deben
    mostrarse. El comando \x auto antes de \df permite aplicar
    automáticamente la visualización expandida cuando sea necesario,
    facilitando la lectura del resultado en Azure Cloud Shell.

> **!!\x auto!!**
>
> **\df+ azure_ai.\***

![](./media/image63.png)

La función azure_ai.set_setting() permite configurar el endpoint y la
clave para los servicios de Azure AI. Acepta una clave y el valor que se
le asignará.

La función azure_ai.get_setting() permite recuperar los valores
establecidos con set_setting(). Acepta la clave de la configuración que
se desea consultar.

Para ambos métodos, la clave debe ser una de las siguientes:

## Tarea 4: Configure el endpoint y la clave de Azure OpenAI

Antes de utilizar las funciones azure_openai, configure la extensión
para su endpoint y clave del servicio Azure OpenAI.

1.  En el siguiente comando, sustituya los tokens {endpoint} y {api-key}
    por los valores que recuperó del portal de Azure y, a continuación,
    ejecute los comandos desde el símbolo del sistema psql en el panel
    Shell de la nube para añadir sus valores a la tabla de
    configuración.

> **!!SELECT
> azure_ai.set_setting('azure_openai.endpoint','{endpoint}');**
>
> **SELECT azure_ai.set_setting('azure_openai.subscription_key',
> '{api-key}');!!**

![](./media/image64.png)

2.  Verifique los ajustes escritos en la tabla de configuración mediante
    las siguientes consultas:

> +++SELECT azure_ai.get_setting('azure_openai.endpoint');

SELECT azure_ai.get_setting('azure_openai.subscription_key');+++

La extensión azure_ai ya está conectada a su cuenta Azure OpenAI y lista
para generar los embeddings vectoriales.

![](./media/image65.png)

# Ejercicio 5: Generar embeddings vectoriales con Azure OpenAI

El esquema azure_openai de la extensión azure_ai permite a Azure OpenAI
generar embeddings vectoriales a partir de valores de texto. Mediante
este esquema, es posible crear representaciones vectoriales del texto
directamente desde la base de datos, lo que facilita búsquedas por
similitud vectorial y su uso en modelos de machine learning.

Los embeddings son un concepto en machine learning y procesamiento de
lenguaje natural (NLP) que representan objetos, como palabras,
documentos o entidades, como vectores en un espacio multidimensional.
Esto permite a los modelos evaluar la relación entre los datos,
identificar patrones y mejorar la precisión de las predicciones.

## Tarea 1: Habilite el soporte vectorial con la extensión pgvector

La extensión azure_ai permite generar embeddings vectoriales a partir de
texto. Para almacenar estos vectores junto con el resto de los datos en
la base de datos, es necesario instalar la extensión pgvector, siguiendo
las indicaciones de la documentación sobre la habilitación del soporte
vectorial en la base de datos.

1.  Instale la extensión pgvector utilizando el comando CREATE
    EXTENSION.

> **!!CREATE EXTENSION IF NOT EXISTS vector;!!**
>
> ![](./media/image66.png)

2.  Con el soporte vectorial habilitado en la base de datos, agregue una
    nueva columna a la tabla listings utilizando el tipo de datos vector
    para almacenar los embeddings. El modelo text-embedding-ada-002
    genera vectores con 1536 dimensiones, por lo que se debe especificar
    1536 como el tamaño del vector.

> +++**ALTER TABLE listings**

**ADD COLUMN description_vector vector(1536);+++**

![](./media/image67.png)

## Tarea 2: Genere y almacene embeddings vectoriales

La tabla listings está lista para almacenar embeddings. Utilizando la
función azure_openai.create_embeddings(), se pueden generar vectores a
partir del campo description e insertarlos en la columna
description_vector recién creada en la tabla listings.

1.  Antes de utilizar la función create_embeddings(), ejecute el
    siguiente comando para inspeccionarla y revisar los argumentos
    requeridos:

> **+++\df+ azure_openai.\*+++**

![](./media/image68.png)

La propiedad **Argument data types** en la salida del comando \df+
azure_openai.\* muestra la lista de argumentos que la función espera.

[TABLE]

2.  Utilizando el nombre de la implementación, ejecute la siguiente
    consulta para actualizar cada registro en la tabla listings,
    insertando los embeddings vectoriales generadas a partir del campo
    description en la columna description_vector, mediante la función
    azure_openai.create_embeddings(). Reemplace {your-deployment-name}
    con el **nombre de la implementación** copiado desde la página de
    **Deployments** en Azure OpenAI Studio.

**Nota:** Esta consulta puede tardar aproximadamente cinco minutos en
completarse.

> **DO $$**
>
> **DECLARE counter integer := (SELECT COUNT(\*) FROM listings WHERE
> description \<\> '' AND description_vector IS NULL);**
>
> **DECLARE r record;**
>
> **BEGIN**
>
> **RAISE NOTICE 'Total descriptions to embed: %', counter;**
>
> **WHILE counter \> 0 LOOP**
>
> **BEGIN**
>
> **FOR r IN**
>
> **SELECT listing_id FROM listings WHERE description \<\> '' AND
> description_vector IS NULL**
>
> **LOOP**
>
> **BEGIN**
>
> **UPDATE listings**
>
> **SET description_vector =
> azure_openai.create_embeddings('{your-deployment-name}',
> description)**
>
> **WHERE listing_id = r.listing_id;**
>
> **EXCEPTION**
>
> **WHEN OTHERS THEN**
>
> **RAISE NOTICE 'Waiting 1 second before trying again...';**
>
> **PERFORM pg_sleep(1);**
>
> **END;**
>
> **counter := (SELECT COUNT(\*) FROM listings WHERE description \<\> ''
> AND description_vector IS NULL);**
>
> **IF counter % 25 = 0 THEN**
>
> **RAISE NOTICE 'Remaining descriptions to embed: %', counter;**
>
> **END IF;**
>
> **END LOOP;**
>
> **END;**
>
> **END LOOP;**
>
> **END;**
>
> **$$;!!**
>
> ![](./media/image69.png)
>
> La consulta anterior utiliza un bucle **WHILE** para recuperar
> registros de la tabla listings donde el campo description_vector es
> NULL y el campo description no está vacío. Luego, intenta actualizar
> la columna description_vector con una representación vectorial del
> campo description, utilizando la función
> azure_openai.create_embeddings().
>
> El uso del bucle es necesario para evitar que las llamadas a la
> función de generación de embeddings superen el límite de tasa de
> solicitudes del servicio Azure OpenAI. Si se excede este límite,
> aparecerán advertencias similares a las siguientes en el resultado:
>
> **NOTICE**: Waiting 1 second before trying again...

![](./media/image70.png)

> ![A screenshot of a computer program Description automatically
> generated](./media/image71.png)

3.  Para verificar que la columna description_vector ha sido poblada
    para todos los registros de la tabla listings, ejecute la siguiente
    consulta:

> **!!SELECT COUNT(\*) FROM listings WHERE description_vector IS NULL
> AND description \<\> '';!!**
>
> El resultado de la consulta debe ser un recuento de 0.

![A black screen with white text Description automatically
generated](./media/image72.png)

## Tarea 3: Realice una búsqueda por similitud vectorial

La similitud vectorial es un método utilizado para medir la similitud de
dos elementos representándolos como vectores, una serie de números. Los
vectores se utilizan a menudo para realizar búsquedas con LLMs. La
similitud vectorial se calcula comúnmente utilizando métricas de
distancia, como la distancia euclidiana o la similitud coseno. La
distancia euclidiana mide la distancia en línea recta entre dos vectores
en el espacio n-dimensional, mientras que la similitud coseno mide el
coseno del ángulo entre dos vectores. Cada embedding es un vector de
números de punto flotante, por lo que la distancia entre dos embeddings
en el espacio vectorial se correlaciona con la similitud semántica entre
dos entradas en el formato original.

1.  Antes de ejecutar una búsqueda por similitud vectorial, ejecute la
    siguiente consulta utilizando la cláusula **ILIKE** para observar
    los resultados de búsqueda de registros con una consulta en lenguaje
    natural, sin aplicar similitud vectorial:

**!!SELECT listing_id, name, description FROM listings WHERE description
ILIKE '%Properties with a private room near Discovery Park%';!!**

![](./media/image73.png)

> La consulta devuelve cero resultados porque está intentando hacer
> coincidir el texto del campo de descripción con la consulta en
> lenguaje natural proporcionada.

2.  Ahora, ejecute una consulta de búsqueda por similitud coseno en la
    tabla listings para realizar una búsqueda por similitud vectorial en
    las descripciones de los listados. Los embeddings se generan para
    una pregunta de entrada y luego se convierten en un array vectorial
    (:vector), lo que permite compararlas con los vectores almacenados
    en la tabla listings. Reemplace {your-deployment-name} por el valor
    del **nombre de la implementación** que ha copiado de la página
    **Deployments** de Azure OpenAI Studio.

> **!!SELECT listing_id, name, description FROM listings**
>
> **ORDER BY description_vector \<=\>
> azure_openai.create_embeddings('{your-deployment-name}', 'Properties
> with a private room near Discovery Park')::vector**
>
> **LIMIT 3;!!**

![](./media/image74.png)

La consulta utiliza el operador vectorial \<=\>, que representa el
operador “distancia coseno” utilizado para calcular la distancia entre
dos vectores en un espacio multidimensional.

3.  Ejecute de nuevo la misma consulta utilizando la cláusula EXPLAIN
    ANALYZE para ver los tiempos de planificación y ejecución de la
    consulta. Reemplace {your-deployment-name} por el valor del **nombre
    de la implementación** que ha copiado de la página **Deployments**
    de Azure OpenAI Studio.

> **!!EXPLAIN ANALYZE**
>
> **SELECT listing_id, name, description FROM listings**
>
> **ORDER BY description_vector \<=\>
> azure_openai.create_embeddings('{your-deployment-name}', 'Properties
> with a private room near Discovery Park')::vector**
>
> **LIMIT 3;!!**

![](./media/image75.png)

![](./media/image76.png)

![A screen shot of a computer Description automatically
generated](./media/image77.png)

En los resultados, observe el plan de consulta, que comenzará con algo
similar a:

> Limit (cost=1098.54..1098.55 rows=3 width=261) (actual
> time=10.505..10.507 rows=3 loops=1)
>
> -\> Sort (cost=1098.54..1104.10 rows=2224 width=261) (actual
> time=10.504..10.505 rows=3 loops=1)
>
> ...
>
> Sort Method: top-N heapsort Memory: 27kB
>
> -\> Seq Scan on listings (cost=0.00..1069.80 rows=2224 width=261)
> (actual time=0.005..9.997 rows=2224 loops=1)
>
> La consulta utiliza una ordenación secuencial para realizar la
> búsqueda. Los tiempos de planificación y ejecución se mostrarán al
> final de los resultados, con un aspecto similar al siguiente:
>
> Planning Time: 62.020 ms
>
> Execution Time: 10.530 ms

4.  Para mejorar la eficiencia de la búsqueda en el campo vectorial,
    cree un índice en listings utilizando distancia coseno y HNSW
    (*Hierarchical Navigable Small World*). HNSW permite que pgvector
    utilice los algoritmos más recientes basados en grafos para
    aproximar consultas de vecinos más cercanos.

> **!!CREATE INDEX ON listings USING hnsw (description_vector
> vector_cosine_ops);!!**

![](./media/image78.png)

5.  Para observar el impacto del índice hnsw en la tabla, ejecute de
    nuevo la consulta con la cláusula EXPLAIN ANALYZE para comparar los
    tiempos de planificación y ejecución de la consulta. Reemplace
    {your-deployment-name} por el valor del **nombre de la
    implementación** que ha copiado de la página **Deployments** de
    Azure OpenAI Studio.  
    .

> EXPLAIN ANALYZE
>
> SELECT listing_id, name, description FROM listings
>
> ORDER BY description_vector \<=\>
> azure_openai.create_embeddings('{your-deployment-name}', 'Properties
> with a private room near Discovery Park')::vector
>
> LIMIT 3;

![A screenshot of a computer Description automatically
generated](./media/image79.png)

![A screenshot of a computer Description automatically
generated](./media/image80.png)

![A screenshot of a computer screen Description automatically
generated](./media/image81.png)

En los resultados, observe que el plan de consulta incluye ahora una
exploración de índices más eficiente:

Limit (cost=116.48..119.33 rows=3 width=261) (actual time=1.112..1.130
rows=3 loops=1)

-\> Index Scan using listings_description_vector_idx on listings
(cost=116.48..2228.28 rows=2224 width=261) (actual time=1.111..1.128
rows=3 loops=1)

Los tiempos de ejecución de la consulta deben reflejar una reducción
significativa del tiempo necesario para planificar y ejecutar la
consulta:

Planning Time: 56.802 ms

Execution Time: 1.167 ms

# Ejercicio 6: Integrar los servicios Azure AI

Las integraciones de Azure AI Services incluidas en el esquema
azure_cognitive de la extensión azure_ai proporcionan un conjunto
avanzado de funciones de AI Language accesibles directamente desde la
base de datos. Estas funcionalidades incluyen análisis de sentiment,
detección de idioma, extracción de frases clave, reconocimiento de
entidades y resumen de texto.

Estas capacidades están habilitadas a través del servicio Azure AI
Language.

Para revisar la lista completa de funciones de Azure AI accesibles
mediante la extensión, consulte la documentación sobre la integración de
Azure Database for PostgreSQL Flexible Server con Azure Cognitive
Services.

## Tarea 1: Aprovisione un servicio de Azure AI Language

Se requiere un servicio de Azure AI Language para aprovechar las
funciones cognitivas de la extensión azure_ai. En este ejercicio, se
creará un servicio de Azure AI Language.

1.  Desde la página de inicio del **Azure Portal**, haga clic en el menú
    de Azure, representado por tres barras horizontales en el lado
    izquierdo de la barra de comandos de Microsoft Azure, como se
    muestra en la imagen a continuación.

![](./media/image82.png)

2.  En la página **Create a resource**, seleccione AI + Machine Learning
    en el menú lateral izquierdo y, a continuación, elija **Language
    service.**

![](./media/image83.png)

![](./media/image84.png)

3.  En el cuadro de diálogo **Select additional features**,
    seleccione **Continue to create your resource**.

> ![The continue to create your resource button is highlighted on the
> select additional features dialog.](./media/image85.png)

4.  En la pestaña **Create Language** **Basics**, ingrese lo siguiente:

[TABLE]

> ![](./media/image86.png)
>
> ![](./media/image87.png)

5.  La configuración por defecto se utilizará para el resto de pestañas
    de la configuración del servicio de idiomas, así que seleccione el
    botón **Review + create**.

6.  Seleccione el botón **Create** en la pestaña **Review +
    create** para aprovisionar el servicio Idioma.

> ![](./media/image88.png)

7.  Seleccione **Go to resource group** en la página de implementación
    cuando la implementación del servicio de lenguaje se haya
    completado.

![](./media/image89.png)

## Tarea 2: Configure el endpoint y la clave del servicio Azure AI Language

Al igual que con las funciones de azure_openai, para realizar llamadas a
los servicios de Azure AI mediante la extensión azure_ai, es necesario
proporcionar el endpoint y una clave del servicio Azure AI Language.

1.  En la página de inicio de **Language**, seleccione **Keys and
    Endpoint** en la sección **Resource Management** del menú de
    navegación lateral.

2.  En la página **Keys and Endpoints**, copie los valores de **KEY1**,
    **KEY2** y **Endpoint**, péguenos en un archivo de **Notepad** como
    se muestra en la imagen a continuación y **guarde** el archivo para
    utilizar esta información en las próximas tareas.

![](./media/image90.png)

3.  Copie los valores de su **endpoint** y clave de acceso. Luego,
    reemplace los marcadores {endpoint} y {api-key} en el siguiente
    comando con los valores obtenidos del **Azure Portal**.

Ejecute los comandos desde el **psql command prompt** en **Cloud Shell**
para agregar sus valores a la tabla de configuración:

> !!SELECT
> azure_ai.set_setting('azure_cognitive.endpoint','{endpoint}');
>
> SELECT azure_ai.set_setting('azure_cognitive.subscription_key',
> '{api-key}');!!

![](./media/image91.png)

## Tarea 3: Analice el sentiment de las reseñas

En esta tarea, se utilizará la función azure_cognitive.analyze_sentiment
para evaluar el **sentiment** de las reseñas de listados de **Airbnb**.

1.  Para realizar análisis de sentiment utilizando el esquema
    azure_cognitive en la extensión azure_ai, se utiliza la función
    analyze_sentiment. Ejecute el siguiente comando para revisar esta
    función:

> **!!\df azure_cognitive.analyze_sentiment!!**

![](./media/image92.png)

La salida muestra el esquema, el nombre, el tipo de dato del resultado y
los tipos de datos de los argumentos de la función. Esta información
permite comprender cómo utilizar la función correctamente.

2.  También es fundamental comprender la estructura del tipo de dato de
    resultado que devuelve la función para manejar correctamente su
    valor de retorno. Ejecute el siguiente comando para inspeccionar el
    tipo sentiment_analysis_result:

> **+++\dT+ azure_cognitive.sentiment_analysis_result+++**

![](./media/image93.png)

3.  La salida del comando anterior revela que el tipo
    sentiment_analysis_result es una **tupla**.

Para comprender la estructura de esta tupla, ejecute el siguiente
comando para ver las columnas contenidas en el tipo compuesto
sentiment_analysis_result:

> **!!\d+ azure_cognitive.sentiment_analysis_result!!**

![](./media/image94.png)

El resultado de ese comando debería ser similar a la siguiente:

> Composite type "azure_cognitive.sentiment_analysis_result"
>
> Column | Type | Collation | Nullable | Default | Storage | Description
>
> ----------------+------------------+-----------+----------+---------+----------+-------------
>
> sentiment | text | | | | extended |
>
> positive_score | double precision | | | | plain |
>
> neutral_score | double precision | | | | plain |
>
> negative_score | double precision | | | | plain |

El tipo compuesto azure_cognitive.sentiment_analysis_result contiene las
predicciones de sentiment del texto de entrada.

Incluye el sentiment, que puede ser positivo, negativo, neutral o mixyo,
y las puntuaciones para los aspectos positivo, neutral y negativo
encontrados en el texto.

Las puntuaciones se representan como números reales entre 0 y 1.

Por ejemplo, en (neutral,0.26,0.64,0.09), el sentiment es neutral, con
una puntuación positiva de 0.26, neutral de 0.64 y negativa de 0.09.

4.  Ahora que ya sabe cómo analizar el sentiment utilizando la extensión
    y la forma del tipo de retorno, ejecute la siguiente consulta que
    busca opiniones abrumadoramente positivas:

WITH cte AS (

SELECT id, azure_cognitive.analyze_sentiment(comments, 'en') AS
sentiment FROM reviews LIMIT 100

)

SELECT

id,

(sentiment).sentiment,

(sentiment).positive_score,

(sentiment).neutral_score,

(sentiment).negative_score,

comments

FROM cte

WHERE (sentiment).positive_score \> 0.98

LIMIT 10;

![](./media/image95.png)

La consulta anterior utiliza una expresión común de tabla o CTE para
obtener las puntuaciones de sentiment de los tres primeros registros de
la tabla de opiniones. A continuación, selecciona las columnas de tipo
compuesto de sentiment de la CTE para extraer los valores individuales
de la tabla sentiment_analysis_result.

# Ejercicio 7: Ejecutar una consulta final para integrar todo 

En este ejercicio, conéctese a su base de datos en **pgAdmin** y ejecute
una consulta final que integre su trabajo con las extensiones azure_ai,
postgis y pgvector a lo largo de los laboratorios 3 y 4.

## Tarea 1: Instale pgAdmin

1.  Abra un navegador web y vaya a la página
    !!https://www.pgadmin.org/download/pgadmin-4-windows/!!

2.  Haga clic en la última versión de **pgAdmin.**

![](./media/image96.png)

3.  Seleccione **pgadmin4-8.9-x64.exe.**

![](./media/image97.png)

4.  Ejecute e instale el archivo descargado.

![](./media/image98.png)

5.  En la pestaña Select Setup Install Mode, seleccione **Install for me
    only(recommended).**

![](./media/image99.png)

6.  Haga clic en el botón **Next.**

![](./media/image100.png)

7.  Seleccione la opción **I accept the agreement** y haga clic en el
    botón **Next.**

![](./media/image101.png)

8.  Seleccione la ruta y haga clic en el botón **Next**.

![](./media/image102.png)

9.  En la ventana **Setup-pgAdmin 4**, haga clic en el botón **Next**.

![](./media/image103.png)

10. Haga clic en el botón **Install.**

![](./media/image104.png)

11. En la ventana **Setup - pgAdmin 4**, haga clic en el botón
    **Finish.**

![](./media/image105.png)

## Tarea 2: Conéctese a la base de datos usando pgAdmin

En esta tarea, abrirá pgAdmin y se conectará a su base de datos.

1.  En el cuadro de búsqueda de Windows, escriba **pgAdmin** y luego
    haga clic en **pgAdmin.**

![](./media/image106.png)

![A screenshot of a computer Description automatically
generated](./media/image107.png)

2.  Registre su servidor haciendo clic con el botón derecho del ratón en
    **Servers** en el Explorador de objetos y seleccionando **Register
    \> Server**.

![](./media/image108.png)

3.  En el cuadro de diálogo **Register - Server**, pegue el nombre de su
    servidor Azure Database for PostgreSQL Flexible Server (que ha
    guardado en el Ejercicio 1\> Tarea 1) en el campo **Name** de la
    pestaña **General**.

> ![](./media/image109.png)

4.  A continuación, seleccione la pestaña **Connection** y pegue el
    nombre de su servidor en el campo **Hostname/address**. Ingrese
    **s2admin** en el campo **Username**, **Seattle123Seattle123** en el
    campo **Password** y, opcionalmente, seleccione **Save password.**

> ![](./media/image110.png)

3.  Finalmente, seleccione la pestaña **Parameters** y configure el
    **SSL mode** en **require**. Seleccione **Save** para registrar su
    servidor.

> ![](./media/image111.png)
>
> ![](./media/image112.png)

4.  Una vez conectado a su servidor, expanda el nodo **Databases** y
    seleccione la base de datos **airbnb**. Haga clic derecho en la base
    de datos **airbnb** y seleccione **Query Tool** en el menú
    contextual.

> ![](./media/image113.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image114.png)

## Tarea 3: Verifique que la extensión PostGIS esté instalada en su base de datos

Para instalar la extensión postgis en su base de datos, utilice el
comando CREATE EXTENSION.

1.  En la ventana de consulta que ha abierto anteriormente, ejecute el
    comando CREATE EXTENSION con la cláusula IF NOT EXISTS para instalar
    la extensión postgis en su base de datos.

> CREATE EXTENSION IF NOT EXISTS postgis;
>
> ![](./media/image115.png)
>
> Con la extensión PostGIS ahora cargada, ya puede comenzar a trabajar
> con datos geoespaciales en la base de datos. La tabla listings que
> creó y pobló anteriormente contiene la latitud y longitud de todas las
> propiedades listadas. Para utilizar estos datos en análisis
> geoespaciales, debe modificar la tabla listings para agregar una
> columna de tipo geometry que acepte el tipo de datos point. Estos
> nuevos tipos de datos están incluidos en la extensión postgis.

2.  Para admitir datos de tipo punto, agregue una nueva columna de tipo
    geometry a la tabla que acepte datos de punto. Copie y pegue la
    siguiente consulta en la ventana de consulta abierta en pgAdmin:

> !!ALTER TABLE listings
>
> ADD COLUMN listing_location geometry(point, 4326);!!

3.  A continuación, actualice la tabla con los datos geoespaciales
    asociados a cada listado agregando los valores de longitud y latitud
    en la columna de tipo de geometría.

> !!UPDATE listings
>
> SET listing_location = ST_SetSRID(ST_Point(longitude, latitude),
> 4326);!!

![A screenshot of a computer Description automatically
generated](./media/image116.png)

## Tarea 4: Ejecute una consulta y visualice los resultados en un mapa

En esta tarea, ejecute una consulta final que integra su trabajo en los
laboratorios 3 y 4.

1.  Ejecute la siguiente consulta que incorpora elementos de las
    extensiones azure_ai, pgvector y PostGIS con las que ha trabajado en
    los laboratorios 3 y 4. Reemplace {your-deployment-name} con el
    valor del **nombre de implementación** que copió de la página de
    **Deployments** de Azure OpenAI Studio.

> !!WITH listings_cte AS (
>
> SELECT l.listing_id, name, listing_location, summary FROM listings l
>
> INNER JOIN calendar c ON l.listing_id = c.listing_id
>
> WHERE ST_DWithin(
>
> listing_location,
>
> ST_GeomFromText('POINT(-122.410347 47.655598)', 4326),
>
> 0.025
>
> )
>
> AND c.date = '2016-01-13'
>
> AND c.available = 't'
>
> AND c.price \<= 75.00
>
> AND l.listing_id IN (SELECT listing_id FROM reviews)
>
> ORDER BY description_vector \<=\>
> azure_openai.create_embeddings('{your-deployment-name}', 'Properties
> with a private room near Discovery Park')::vector
>
> LIMIT 3
>
> ),
>
> sentiment_cte AS (
>
> SELECT r.listing_id, comments,
> azure_cognitive.analyze_sentiment(comments, 'en') AS sentiment
>
> FROM reviews r
>
> INNER JOIN listings_cte l ON r.listing_id = l.listing_id
>
> )
>
> SELECT
>
> l.listing_id,
>
> name,
>
> listing_location,
>
> summary,
>
> avg((sentiment).positive_score) as avg_positive_score,
>
> avg((sentiment).neutral_score) as avg_neutral_score,
>
> avg((sentiment).negative_score) as avg_negative_score
>
> FROM sentiment_cte s
>
> INNER JOIN listings_cte l on s.listing_id = l.listing_id
>
> GROUP BY l.listing_id, name, listing_location, summary;!!

2.  En el panel de **Data Output**, seleccione el botón **View all
    geometries in this column** que se muestra en la columna
    listing_location de los resultados de la consulta.

![](./media/image117.png)

El botón **View all geometries in this column** abre el **Geometry
Viewer**, que permite ver los resultados de la consulta en un mapa.

3.  Seleccione uno de los tres puntos mostrados en el mapa para ver
    detalles sobre la ubicación, incluidos los puntajes promedio de
    sentiment positivo, neutral y negativo en todas las calificaciones
    de la propiedad.

![](./media/image118.png)

![](./media/image119.png)

![A screenshot of a map Description automatically
generated](./media/image120.png)

## Tarea 5: Elimine los recursos 

Es fundamental eliminar los recursos creados en estos laboratorios una
vez finalizados. Se le cobrará por la capacidad configurada, no por el
uso de la base de datos. Para eliminar su grupo de recursos y todos los
recursos creados en este laboratorio, siga las instrucciones a
continuación:

Para evitar costos innecesarios en Azure, elimine los recursos creados
en este inicio rápido si ya no los necesita. Puede administrar los
recursos a través del portal de Azure.

1.  Para eliminar la cuenta de almacenamiento, vaya a la página de
    **Azure portal Home** y haga clic en **Resource groups**.

> ![A screenshot of a computer Description automatically
> generated](./media/image121.png)

2.  Haga clic en el grupo de recursos que ha creado.

> ![](./media/image122.png)

3.  En la página de inicio del **Resource group**, seleccione la opción
    **delete resource group.**

![](./media/image123.png)

![A screenshot of a computer Description automatically
generated](./media/image124.png)

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image125.png)

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image126.png)

![](./media/image127.png)

![](./media/image128.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image129.png)

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image130.png)

![A screenshot of a computer Description automatically
generated](./media/image131.png)

4.  En el panel **Delete Resources** que aparece en el lado derecho,
    vaya al campo **Enter “resource group name” to confirm deletion**,
    ingrese el nombre del grupo de recursos para confirmar la
    eliminación y luego haga clic en el botón **Delete**.

![A screenshot of a computer Description automatically
generated](./media/image132.png)

5.  En el cuadro de diálogo **Delete confirmation**, haga clic en el
    botón **Delete**.

> ![A screenshot of a computer error Description automatically
> generated](./media/image133.png)

6.  Haga clic en el icono de la campaña, verá la notificación –**Deleted
    resource group AOAI-RG89.**

![A screenshot of a computer Description automatically
generated](./media/image134.png)

**Resumen**

En este laboratorio, se ha integrado con éxito Azure AI Services con
PostgreSQL para crear un entorno de base de datos mejorado con
inteligencia artificial. Se inició con la provisión de recursos en Azure
y la configuración de PostgreSQL con las extensiones necesarias. Luego,
se generaron embeddings vectoriales para datos textuales y se realizaron
búsquedas de similitud vectorial para identificar registros
semánticamente similares. Además, se utilizó la extensión PostGIS para
el análisis de datos geoespaciales y el servicio Azure AI Language para
el análisis de sentiments. Finalmente, se optimizaron las consultas
mediante indexación y se analizó su rendimiento, demostrando la
eficiencia y capacidad de esta solución integrada para el análisis
avanzado de datos.
