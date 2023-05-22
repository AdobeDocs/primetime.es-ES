---
title: Configurar la base de datos del servidor de licencias
description: Configurar la base de datos del servidor de licencias
copied-description: true
exl-id: be6232b4-bf51-486f-9c85-ab6f6ec6d9bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Configurar la base de datos del servidor de licencias{#set-up-the-license-server-database}

El servidor de licencias de implementación de referencia requiere una base de datos que admita lo siguiente:

* Autenticación de usuario
* Modelo de uso de reglas empresariales de demostración
* Conversión de metadatos
* Compatibilidad con dominios

La adquisición anónima de licencias no requiere que la base de datos se esté ejecutando.

>[!NOTE]
>
>Este procedimiento sólo se aplica a Microsoft Windows. Para otros sistemas operativos, consulte la documentación de su sistema operativo o consulte la documentación de MySQL.

Para ejecutar el servidor de licencias, debe instalar y configurar MySQL:

1. En el DVD, vaya a la [!DNL Third Party\MySQL\Installer\5.1] e inicie el programa de instalación.
1. Complete la instalación de MySQL.
1. Seleccionar **[!UICONTROL Configure MySQL Server Now]** para iniciar el asistente de configuración.
1. Hasta la quinta pantalla, utilice la configuración predeterminada o seleccione una configuración específica para la prueba.
1. En la quinta pantalla, seleccione **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e introduzca el número máximo de conexiones permitidas.
1. Anote la contraseña de root.
1. Para volver a instalar MySQL, si necesita iniciar el servidor más tarde, complete los siguientes pasos:
   1. Elimine el *unidad del sistema:* carpeta.

      Esta carpeta se encuentra en [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Elimine la carpeta de instalación de MySQL anterior.

      Por ejemplo, *unidad del sistema:*, que se encuentra en [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Para instalar MySQL JDBC Driver 5.1.7, copie el [!DNL mysql-connector-java-5.1.7-bin.jar] archivo en el [!DNL Third Party\MySQL\Installer\5.1] en el DVD a la carpeta [!DNL ...\Tomcat6.0\lib] en el servidor Tomcat.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 funciona con Tomcat 6.0. Ya no se admiten versiones anteriores de Tomcat.
