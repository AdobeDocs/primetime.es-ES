---
description: 'null'
seo-description: 'null'
seo-title: Configurar la base de datos del servidor de licencias
title: Configurar la base de datos del servidor de licencias
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Configurar la base de datos del servidor de licencias{#configure-the-license-server-database}

Para configurar la base de datos de ejemplo, configure el esquema de la base de datos y rellene la base de datos con datos de ejemplo:

1. Sube la línea de comandos de MySQL.

   **En Windows -** Haga clic   **[!UICONTROL Window's Start Menu]** >  **[!UICONTROL MySQL]** >  **[!UICONTROL MySQL Server 5.1]** >  **[!UICONTROL MySQL Command Line Client]**

   **En Linux, etc.** - Tipo  `MySQL`.

1. Ejecute el siguiente script SQL:

   mysql> source &quot;`"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Esta secuencia de comandos agrega la cuenta de usuario `dbuser`, establece una conexión a través de una aplicación Web y crea un esquema de base de datos.

   >[!NOTE]
   >
   >Asegúrese de que no haya punto y coma ( `;`) al final de la secuencia de comandos.

1. Edite la secuencia de comandos `PopulateSampleDB.sql` que rellena los datos de ejemplo en las tablas para incluir datos para la prueba.

   Esta secuencia de comandos se encuentra en la carpeta `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\`.
1. Ejecute la secuencia de comandos [!DNL PopulateSampleDB] para rellenar los datos como lo hizo en el paso 2.

   >[!NOTE]
   >
   >La primera vez que ejecute la secuencia de comandos [!DNL CreateSampleDB.sql] se producirá el siguiente error:

   Puede ignorar este error con seguridad. Solo se produce la primera vez que ejecute esta secuencia de comandos.

Debe configurar el agrupamiento de conexiones de base de datos (DBCP), que utiliza el pool de conexiones de base de datos Jakarta-Commons. Se ha configurado una base de datos de origen de datos JNDI para aprovechar esta agrupación de conexiones del servidor de aplicaciones. Para cambiar la conexión de la base de datos para que apunte a un servidor MySQL que no esté en localhost, modifique uno de los siguientes archivos:

* El archivo [!DNL META-INF\context.xml], que especifica la ubicación, el nombre de usuario y la contraseña de la base de datos del servidor de licencias que se encuentra en el archivo [!DNL flashaccess.war].

* El archivo `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml`.

y vuelva a crear el archivo WAR utilizando los archivos actualizados.

Para cambiar cualquiera de estos parámetros, edite el archivo [!DNL context.xml] en el directorio [!DNL WebContent] y utilice la secuencia de comandos Ant para volver a crear el archivo WAR. Para ajustar la base de datos, cambie la configuración del origen de datos JNDI en este archivo.

Si depura el proyecto de implementación de referencia en Eclipse, agregue `$CATALINA_HOME\lib\tomcat-dbcp.jar` a la configuración de ejecución/depuración.

>[!NOTE]
>
>Si ejecuta el archivo [!DNL flashaccess.war] en un servidor Tomcat 6.0 independiente, este paso no es necesario.

