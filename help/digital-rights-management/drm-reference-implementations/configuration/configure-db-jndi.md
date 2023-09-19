---
title: Configurar la base de datos del servidor de licencias
description: Configurar la base de datos del servidor de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Configurar la base de datos del servidor de licencias{#configure-the-license-server-database}

Para configurar la base de datos de ejemplo configurando el esquema de la base de datos y rellenando la base de datos con datos de ejemplo:

1. Muestra la línea de comandos MySQL.

   **En Windows:** Clic  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **En Linux, etc.** - Tipo `MySQL`.

1. Ejecute el siguiente script SQL:

   mysql> source &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Esta secuencia de comandos agrega la cuenta de usuario `dbuser`, establece una conexión a través de una aplicación web y crea un esquema de base de datos.

   >[!NOTE]
   >
   >Asegúrese de que no haya ningún punto y coma ( `;`) al final del script.

1. Edite el `PopulateSampleDB.sql` secuencia de comandos que rellena datos de ejemplo en las tablas para incluir datos para la prueba.

   Esta secuencia de comandos se encuentra en `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` carpeta.
1. Ejecute el [!DNL PopulateSampleDB] para rellenar los datos como lo hizo en el paso 2.

   >[!NOTE]
   >
   >La primera vez que ejecute el [!DNL CreateSampleDB.sql] se produce el siguiente error:

   Puede ignorar este error de forma segura. Solo se produce la primera vez que ejecuta este script.

Debe configurar el pool de conexiones de base de datos (DBCP), que utiliza el pool de conexiones de base de datos de Jakarta-Commons. Se ha configurado una base de datos de origen de datos JNDI TestDB para aprovechar esta agrupación de conexiones del servidor de aplicaciones. Para cambiar la conexión de base de datos para que apunte a un servidor MySQL que no está en localhost, modifique uno de los siguientes archivos:

* El [!DNL META-INF\context.xml] , que especifica la ubicación, el nombre de usuario y la contraseña de la base de datos del servidor de licencias que se encuentra en [!DNL flashaccess.war] archivo.

* El `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` archivo.

y vuelva a crear el archivo WAR utilizando los archivos actualizados.

Para cambiar cualquiera de estos parámetros, edite el [!DNL context.xml] archivo en el [!DNL WebContent] y utilice el script Ant para volver a crear el archivo WAR. Para ajustar la base de datos, cambie la configuración del origen de datos JNDI en este archivo.

Si depura el proyecto Implementación de referencia en Eclipse, agregue `$CATALINA_HOME\lib\tomcat-dbcp.jar` a la configuración de ejecución/depuración.

>[!NOTE]
>
>Si ejecuta el [!DNL flashaccess.war] en un servidor Tomcat 6.0 independiente, este paso no es obligatorio.
