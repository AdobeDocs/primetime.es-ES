---
title: Configuración de la base de datos del servidor de licencias
description: Configuración de la base de datos del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Configurar la base de datos del servidor de licencias{#configure-the-license-server-database}

Para configurar la base de datos de ejemplo configurando el esquema de base de datos y rellenando la base de datos con datos de ejemplo:

1. Abre la línea de comandos de MySQL.

   **En Windows:** haga clic en   **[!UICONTROL Window's Start Menu]** >  **[!UICONTROL MySQL]** >  **[!UICONTROL MySQL Server 5.1]** >  **[!UICONTROL MySQL Command Line Client]**

   **En Linux, etc.** - Tipo  `MySQL`.

1. Ejecute el siguiente script SQL:

   mysql> fuente &quot;`"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Esta secuencia de comandos agrega la cuenta de usuario `dbuser`, establece una conexión a través de una aplicación web y crea un esquema de base de datos.

   >[!NOTE]
   >
   >Asegúrese de que no haya ningún punto y coma ( `;`) al final de la secuencia de comandos.

1. Edite la secuencia de comandos `PopulateSampleDB.sql` que rellena los datos de ejemplo en las tablas para incluir datos para la prueba.

   Esta secuencia de comandos se encuentra en la carpeta `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\`.
1. Ejecute la secuencia de comandos [!DNL PopulateSampleDB] para rellenar los datos como hizo en el paso 2.

   >[!NOTE]
   >
   >La primera vez que ejecute el script [!DNL CreateSampleDB.sql], se producirá el siguiente error:

   Puede ignorar este error de forma segura. Solo ocurre la primera vez que ejecuta esta secuencia de comandos.

Debe configurar el agrupamiento de conexiones de base de datos (DBCP), que utiliza el pool de conexiones de base de datos Jakarta-Commons. Se ha configurado una base de datos JNDI Datasource TestDB para aprovechar esta agrupación de conexiones del servidor de aplicaciones. Para cambiar la conexión de la base de datos para que apunte a un servidor MySQL que no está en localhost, modifique uno de los siguientes archivos:

* El archivo [!DNL META-INF\context.xml], que especifica la ubicación, el nombre de usuario y la contraseña de la base de datos del servidor de licencias que se encuentra en el archivo [!DNL flashaccess.war].

* El archivo `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml`.

y vuelva a crear el archivo WAR utilizando los archivos actualizados.

Para cambiar cualquiera de estos parámetros, edite el archivo [!DNL context.xml] en el directorio [!DNL WebContent] y use el script Ant para recrear el archivo WAR. Para ajustar la base de datos, cambie la configuración de la fuente de datos JNDI en este archivo.

Si depura el proyecto de implementación de referencia en Eclipse, agregue `$CATALINA_HOME\lib\tomcat-dbcp.jar` a la configuración de ejecución/depuración.

>[!NOTE]
>
>Si ejecuta el archivo [!DNL flashaccess.war] en un servidor Tomcat 6.0 independiente, este paso no es necesario.

