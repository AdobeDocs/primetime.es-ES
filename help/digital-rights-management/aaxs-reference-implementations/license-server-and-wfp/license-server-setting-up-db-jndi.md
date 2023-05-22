---
title: Configuración de la base de datos y de la fuente de datos JNDI
description: Configuración de la base de datos y de la fuente de datos JNDI
copied-description: true
exl-id: ed22f095-924b-4792-8a10-e7548fab2c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Configuración de la base de datos y de la fuente de datos JNDI {#setting-up-the-database-and-configuring-the-jndi-datasource}

El servidor de licencias de implementación de referencia necesita una base de datos que admita las siguientes funciones:

* Autenticación de usuario
* Modelo de uso de reglas empresariales de demostración
* Conversión de metadatos
* Compatibilidad con dominios

La adquisición anónima de licencias no requiere que se esté ejecutando una base de datos.

>[!NOTE]
>
>Las instrucciones de esta sección son para la plataforma Microsoft Windows. Para otros sistemas operativos, consulte la documentación de su sistema operativo o consulte la documentación de MySQL.

Para ejecutar el servidor de licencias, deberá instalar y configurar MySQL 5.1.34:

1. Ejecute el instalador de MySQL (que se encuentra en la tercera carpeta Party\MySQL\Installer\5.1 del DVD).
1. Al final del procedimiento de instalación, compruebe **[!UICONTROL Configure MySQL Server Now]** para iniciar el asistente de configuración. Utilice la configuración predeterminada o seleccione una configuración específica para las pruebas, con la excepción de que en la quinta pantalla debe seleccionar **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e introduzca el número máximo de conexiones permitidas.

1. Anote la contraseña de la raíz.
1. Si necesita volver a instalar MySQL, siga estos pasos para evitar problemas al iniciar el servidor después:

   * Eliminar la carpeta *unidad del sistema:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Elimine la carpeta de instalación de MySQL anterior: por ejemplo, *unidad del sistema:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

A continuación, deberá instalar MySQL JDBC Driver 5.1.7. Para ello, copie [!DNL mysql-connector-java-5.1.7-bin.jar] (se encuentra en la [!DNL Third Party\MySQL\Installer\5.1] en el DVD) al directorio de biblioteca del servidor Tomcat: [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC Driver 5.1.7 funciona con Tomcat 6.0. No se admiten versiones anteriores de Tomcat.

Configure la base de datos de ejemplo configurando el esquema de la base de datos y rellenando la base de datos con datos de ejemplo. Para ello, realice los siguientes pasos:

1. Ir a  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. Después de escribir la contraseña, ejecute el siguiente script SQL para agregar la cuenta de usuario `dbuser` para establecer una conexión a través de una aplicación web y crear un esquema de base de datos (asegúrese de que no haya &quot;;&quot; al final. Presione Intro.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Edite el script que rellena los datos de ejemplo en las tablas para incluir datos para las pruebas: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Ejecute esta secuencia de comandos para rellenar los datos como lo hizo en el paso 2.

>[!NOTE]
>
>La primera vez que ejecute el [!DNL CreateSampleDB.sql] recibirá el siguiente error:

*ERROR 1396 (HY000): error de la operación DROP USER para la consulta &#39;dbuser&#39;@&#39;localhost&#39;. Correcto, 0 filas afectadas (0,00 s).*

Puede ignorar este error de forma segura. Esto solo ocurre la primera vez que ejecuta este script.

En este punto deberá configurar la agrupación de conexiones de base de datos (DBCP). DBCP utiliza el grupo de conexiones de base de datos Jakarta-Commons. Se ha configurado una base de datos de origen de datos JNDI TestDB para aprovechar esta agrupación de conexiones del servidor de aplicaciones. Para cambiar la conexión de la base de datos para que apunte a un servidor MySQL que no esté en localhost, modifique el [!DNL META-INF\context.xml] (que especifica la ubicación, el nombre de usuario y la contraseña de la base de datos del servidor de licencias) ubicado en [!DNL flashaccess.war], o modificar [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] y vuelva a crear el archivo WAR utilizando los archivos actualizados. Para cambiar cualquiera de estos parámetros, edite el [!DNL context.xml] ubicado en el directorio WebContent y utilice el script Ant para volver a crear el archivo WAR. Para ajustar la base de datos, cambie la configuración del origen de datos JNDI en este archivo.

Si depura el proyecto Implementación de referencia en Eclipse, debe agregar lo siguiente `$CATALINA_HOME\lib\tomcat-dbcp.jar` a la configuración de ejecución/depuración. Este paso no es necesario si ejecuta el [!DNL flashaccess.war] en un servidor Tomcat 6.0 independiente.
