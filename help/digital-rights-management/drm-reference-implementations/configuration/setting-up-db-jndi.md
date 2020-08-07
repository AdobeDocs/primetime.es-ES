---
description: 'null'
seo-description: 'null'
seo-title: Configuración de la base de datos del servidor de licencias
title: Configuración de la base de datos del servidor de licencias
uuid: aa6185f2-8e9d-4b65-971a-b7534d910580
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Configuración de la base de datos del servidor de licencias{#set-up-the-license-server-database}

El servidor de licencias de implementación de referencia requiere una base de datos que admita lo siguiente:

* Autenticación de usuarios
* Modelo de uso demostración de reglas comerciales
* Conversión de metadatos
* Compatibilidad con dominios

La adquisición anónima de licencias no requiere que la base de datos se esté ejecutando.

>[!NOTE]
>
>Este procedimiento solo se aplica a Microsoft Windows. Para otros sistemas operativos, consulte la documentación de su sistema operativo o consulte la documentación de MySQL.

Para ejecutar el servidor de licencias, debe instalar y configurar MySQL:

1. En el DVD, vaya a la [!DNL Third Party\MySQL\Installer\5.1] carpeta y inicio el programa de instalación.
1. Complete la instalación de MySQL.
1. Seleccione **[!UICONTROL Configure MySQL Server Now]** para inicio del asistente de configuración.
1. Hasta la quinta pantalla, utilice la configuración predeterminada o seleccione la configuración específica para la prueba.
1. En la quinta pantalla, seleccione **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** introduzca el número máximo de conexiones permitidas.
1. Anote la contraseña raíz.
1. Para reinstalar MySQL, si necesita inicio del servidor más adelante, complete los siguientes pasos:
   1. Elimine la unidad *del sistema:* carpeta.

      Esta carpeta se encuentra en [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Elimine la carpeta de instalación antigua de MySQL.

      Por ejemplo, la unidad *del sistema:*, que se encuentra en [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Para instalar MySQL JDBC Driver 5.1.7, copie el [!DNL mysql-connector-java-5.1.7-bin.jar] archivo en la [!DNL Third Party\MySQL\Installer\5.1] carpeta del DVD al [!DNL ...\Tomcat6.0\lib] directorio de Tomcat Server.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 funciona con Tomcat 6.0. Ya no se admiten versiones anteriores de Tomcat.

