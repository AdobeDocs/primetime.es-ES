---
description: Puede realizar un seguimiento del uso de vídeo en la Implementación de referencia de Primetime Android configurándola para que funcione con su cuenta de Adobe Analytics.
title: Configuración de Video Analytics
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Configuración de Video Analytics {#configure-video-analytics}

Puede realizar un seguimiento del uso de vídeo en la Implementación de referencia de Primetime Android configurándola para que funcione con su cuenta de Adobe Analytics. La implementación de referencia de Android está diseñada para enviar datos de uso de vídeo y latidos a Adobe Analytics. Para habilitar esta función, primero debe ponerse en contacto con su representante de Adobe Primetime y crear una cuenta de Adobe Analytics.

Existen dos lugares dentro de la Implementación de referencia que debe configurar para habilitar la integración de Adobe Analytics. Las configuraciones de Video Analytics en tiempo de ejecución se aplican una vez que se selecciona un nuevo vídeo para su reproducción (es decir, una vez que se crea una nueva actividad del reproductor).

1. Configure las opciones de tiempo de carga en `ADBMobileConfig.json` archivo de recursos.

   Este archivo lo proporciona el representante del Adobe. No se incluye en el paquete de SDK de Primetime de forma predeterminada. Para obtener más información sobre la configuración de este archivo de configuración, consulte la Guía del programador de Android aquí: Inicialización y configuración de Video Analytics.
1. Configure las opciones en tiempo de ejecución en el menú Configuración de implementación de referencia

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opciones de tiempo de ejecución | Descripción |
   |---|---|
   | Servidor de seguimiento de Video Analytics | URL del punto final de recopilación del back-end de Video Analytics. Aquí es donde se envían todas las llamadas de seguimiento de Video Heartbeat. |
   | ID de trabajo | El identificador del trabajo de procesamiento. Esto indica al extremo back-end qué tipo de procesamiento se aplica a las llamadas de seguimiento de vídeo. |
   | Canal | Nombre del canal en el que el usuario ve el contenido. En el caso de las aplicaciones móviles, suele ser el nombre de la aplicación. |
   | Editor | Nombre del editor de contenido |
   | Registro de depuración | Activa el registro extenso. Deshabilitado de forma predeterminada, esto puede afectar al rendimiento cuando está habilitado, por lo que lo deshabilita para un entorno de producción. |
   | Modo silencioso | Cuando está habilitada, no se realizan llamadas de red, por lo que sería útil para la depuración local, pero debe deshabilitarse para un entorno de producción. |
