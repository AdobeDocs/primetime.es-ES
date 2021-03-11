---
description: Puede rastrear el uso de vídeo en la implementación de referencia de Android de Primetime configurándola para que funcione con su cuenta de Adobe Analytics.
title: Configurar Video Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Configurar Video Analytics {#configure-video-analytics}

Puede rastrear el uso de vídeo en la implementación de referencia de Android de Primetime configurándola para que funcione con su cuenta de Adobe Analytics. La implementación de referencia de Android está diseñada para enviar datos de uso de vídeo y latidos a Adobe Analytics. Para habilitar esta función, primero debe ponerse en contacto con su representante de Adobe Primetime y crear una cuenta de Adobe Analytics.

Para habilitar la integración de Adobe Analytics, debe configurar dos lugares dentro de la Implementación de referencia. Las configuraciones de Video Analytics en tiempo de ejecución surten efecto una vez que se selecciona un nuevo vídeo para la reproducción (es decir, una vez que se crea una nueva PlayerActivity).

1. Configure las opciones de tiempo de carga en el archivo de activos `ADBMobileConfig.json`.

   Este archivo lo proporciona su representante de Adobe. No se incluye en el paquete del SDK de Primetime de forma predeterminada. Para obtener más información sobre la configuración de este archivo de configuración, consulte la guía del programador de Android aquí: Inicialice y configure Video Analytics.
1. Configure las opciones en tiempo de ejecución en el menú Ajustes de implementación de referencia

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opciones en tiempo de ejecución | Descripción |
   |---|---|
   | Servidor de seguimiento de Video Analytics | URL del punto final de recopilación del back-end de video analytics. Aquí es donde se envían todas las llamadas de seguimiento de Video Heartbeat. |
   | ID de trabajo | Identificador del trabajo de procesamiento. Esto indica al extremo back-end qué tipo de procesamiento aplicar para las llamadas de seguimiento de vídeo. |
   | Canal | Nombre del canal donde el usuario ve el contenido. Para una aplicación móvil, suele ser el nombre de la aplicación. |
   | Editor | Nombre del editor de contenido |
   | Registro de Debug | Activa el registro extenso. Deshabilitado de forma predeterminada, esto puede afectar al rendimiento cuando está habilitado, por lo que se desactiva para un entorno de producción. |
   | Modo silencioso | Cuando esto está habilitado, no se realiza ninguna llamada de red, por lo que sería útil para la depuración local, pero debe deshabilitarse para un entorno de producción. |