---
description: 'null'
seo-description: 'null'
seo-title: Configurar la base de datos del servidor de licencias
title: Configurar la base de datos del servidor de licencias
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurar la base de datos del servidor de licencias{#configure-the-license-server-database}

Para configurar la base de datos de ejemplo configurando el esquema de base de datos y rellenando la base de datos con datos de ejemplo:

1. Sube la línea de comandos de MySQL.

   **En Windows -** Haga clic **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **En Linux, etc.** - Tipo `MySQL`.

1. Ejecute el siguiente script SQL:

   mysql> source &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Esta secuencia de comandos agrega la cuenta de usuario `dbuser`, establece una conexión a través de una aplicación web y crea un esquema de base de datos.

   >[!NOTE]
   >
   >Asegúrese de que no haya punto y coma ( `;`) al final de la secuencia de comandos.

1. Edite la `PopulateSampleDB.sql` secuencia de comandos que rellena los datos de ejemplo en las tablas para incluir datos para la prueba.

   Esta secuencia de comandos se encuentra en la `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` carpeta.
1. Ejecute la [!DNL PopulateSampleDB] secuencia de comandos para rellenar los datos como lo hizo en el paso 2.

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >La primera vez que ejecute la [!DNL CreateSampleDB.sql] secuencia de comandos se producirá el siguiente error:

   Puede ignorar este error con seguridad. Solo se produce la primera vez que ejecute esta secuencia de comandos.

Debe configurar el agrupamiento de conexiones de base de datos (DBCP), que utiliza el pool de conexiones de base de datos Jakarta-Commons. Se ha configurado una base de datos de origen de datos JNDI para aprovechar esta agrupación de conexiones del servidor de aplicaciones. Para cambiar la conexión de la base de datos para que apunte a un servidor MySQL que no esté en localhost, modifique uno de los siguientes archivos:

* El [!DNL META-INF\context.xml] archivo, que especifica la ubicación, el nombre de usuario y la contraseña de la base de datos del servidor de licencias que se encuentra en el [!DNL flashaccess.war] archivo.

* El `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` archivo.

y vuelva a crear el archivo WAR utilizando los archivos actualizados.

Para cambiar cualquiera de estos parámetros, edite el [!DNL context.xml] [!DNL WebContent] archivo en el directorio y utilice el script Ant para volver a crear el archivo WAR. Para ajustar la base de datos, cambie la configuración del origen de datos JNDI en este archivo.

Si depura el proyecto de implementación de referencia en Eclipse, agregue `$CATALINA_HOME\lib\tomcat-dbcp.jar` a la configuración de ejecución/depuración.

>[!NOTE]
>
>Si ejecuta el [!DNL flashaccess.war] archivo en un servidor Tomcat 6.0 independiente, este paso no es necesario.

