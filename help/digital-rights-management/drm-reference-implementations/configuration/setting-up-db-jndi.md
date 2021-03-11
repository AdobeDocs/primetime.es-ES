---
title: Configuración de la base de datos del servidor de licencias
description: Configuración de la base de datos del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Configuración de la base de datos del servidor de licencias{#set-up-the-license-server-database}

El servidor de licencias de implementación de referencia requiere una base de datos para admitir lo siguiente:

* Autenticación de usuarios
* Modelo de uso de demostración de reglas de negocio
* Conversión de metadatos
* Compatibilidad con dominios

La adquisición de licencias anónimas no requiere que la base de datos se esté ejecutando.

>[!NOTE]
>
>Este procedimiento sólo se aplica a Microsoft Windows. Para otros sistemas operativos, consulte la documentación de su sistema operativo o consulte la documentación de MySQL.

Para ejecutar el servidor de licencias, debe instalar y configurar MySQL:

1. En el DVD, vaya a la carpeta [!DNL Third Party\MySQL\Installer\5.1] e inicie el programa de instalación.
1. Complete la instalación de MySQL.
1. Seleccione **[!UICONTROL Configure MySQL Server Now]** para iniciar el asistente de configuración.
1. Hasta la quinta pantalla, utilice la configuración predeterminada o seleccione una configuración específica para la prueba.
1. En la quinta pantalla, seleccione **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e introduzca el número máximo de conexiones permitidas.
1. Escriba la contraseña raíz.
1. Para reinstalar MySQL, si necesita iniciar el servidor más tarde, complete los siguientes pasos:
   1. Elimine la carpeta *unidad del sistema:*.

      Esta carpeta se encuentra en [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Elimine la antigua carpeta de instalación de MySQL.

      Por ejemplo, *unidad del sistema:*, que se encuentra en [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Para instalar el controlador JDBC de MySQL 5.1.7, copie el archivo [!DNL mysql-connector-java-5.1.7-bin.jar] en la carpeta [!DNL Third Party\MySQL\Installer\5.1] del DVD en el directorio [!DNL ...\Tomcat6.0\lib] del servidor Tomcat.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 funciona con Tomcat 6.0. Ya no se admiten versiones anteriores de Tomcat.

