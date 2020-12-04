---
seo-title: Configuración de la base de datos y de la fuente de datos JNDI
title: Configuración de la base de datos y de la fuente de datos JNDI
uuid: 1326523f-c053-4169-a934-1b2d3907b1f4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Configuración de la base de datos y configuración del origen de datos JNDI {#setting-up-the-database-and-configuring-the-jndi-datasource}

El servidor de licencias de implementación de referencia requiere una base de datos para admitir las siguientes funciones:

* Autenticación de usuarios
* Modelo de uso demostración de reglas comerciales
* Conversión de metadatos
* Compatibilidad con dominios

La adquisición anónima de licencias no requiere que se ejecute una base de datos.

>[!NOTE]
>
>Las instrucciones de esta sección son para la plataforma Microsoft Windows. Para otros sistemas operativos, consulte la documentación de su sistema operativo o consulte la documentación de MySQL.

Para ejecutar el servidor de licencias, deberá instalar y configurar MySQL 5.1.34:

1. Ejecute el programa de instalación de MySQL (que se encuentra en la tercera carpeta Party\MySQL\Installer\5.1 del DVD).
1. Al final del procedimiento de instalación, marque **[!UICONTROL Configure MySQL Server Now]** para inicio del asistente de configuración. Utilice la configuración predeterminada o seleccione la configuración específica para realizar pruebas, con la excepción de que en la quinta pantalla debe seleccionar **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e introducir el número máximo de conexiones permitidas.

1. Anote la contraseña raíz.
1. Si necesita reinstalar MySQL, siga estos pasos para evitar problemas al iniciar el servidor después:

   * Elimine la carpeta *unidad del sistema:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Elimine la carpeta de instalación antigua de MySQL: por ejemplo, *unidad del sistema:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

A continuación, deberá instalar MySQL JDBC Driver 5.1.7. Para ello, copie [!DNL mysql-connector-java-5.1.7-bin.jar] (que se encuentra en la carpeta [!DNL Third Party\MySQL\Installer\5.1] del DVD) en el directorio de biblioteca de Tomcat Server: [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC Driver 5.1.7 funciona con Tomcat 6.0. No se admiten versiones anteriores de Tomcat.

Configure la base de datos de ejemplo configurando el esquema de la base de datos y rellenando la base de datos con datos de ejemplo. Para ello, lleve a cabo los siguientes pasos:

1. Vaya a **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**.
1. Después de escribir la contraseña, ejecute la siguiente secuencia de comandos SQL para agregar la cuenta de usuario `dbuser` para establecer una conexión a través de una aplicación Web y crear un esquema de base de datos (asegúrese de que no haya &quot;;&quot; al final. Pulse Intro.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Edite la secuencia de comandos que rellena los datos de ejemplo en las tablas para incluir datos con fines de prueba: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Ejecute esta secuencia de comandos para rellenar los datos como lo hizo en el paso 2.

>[!NOTE]
>
>La primera vez que ejecute la secuencia de comandos [!DNL CreateSampleDB.sql], recibirá el siguiente error:

*ERROR 1396 (HY000): Error de la operación DROP USER para la Consulta &#39;dbuser&#39;@&#39;localhost&#39;, 0 filas afectadas (0,00 seg.).*

Puede ignorar este error con seguridad. Esto solo sucede la primera vez que ejecute esta secuencia de comandos.

En este punto deberá configurar el agrupamiento de conexiones de base de datos (DBCP). DBCP utiliza el Pool de Conexiones de Base de Datos Jakarta-Commons. Se ha configurado una base de datos de origen de datos JNDI para aprovechar esta agrupación de conexiones del servidor de aplicaciones. Para cambiar la conexión de base de datos para que apunte a un servidor MySQL que no esté en localhost, modifique el archivo [!DNL META-INF\context.xml] (que especifica la ubicación, el nombre de usuario y la contraseña de la base de datos del servidor de licencias) ubicado en [!DNL flashaccess.war], o modifique [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] y vuelva a crear el archivo WAR usando los archivos actualizados. Para cambiar cualquiera de estos parámetros, edite el [!DNL context.xml] ubicado en el directorio WebContent y utilice el script Ant para volver a crear el archivo WAR. Para ajustar la base de datos, cambie la configuración del origen de datos JNDI en este archivo.

Si depura el proyecto de implementación de referencia dentro de Eclipse, debe agregar `$CATALINA_HOME\lib\tomcat-dbcp.jar` a la configuración de ejecución/depuración. Este paso no es necesario si ejecuta el archivo [!DNL flashaccess.war] en un servidor Tomcat 6.0 independiente.
