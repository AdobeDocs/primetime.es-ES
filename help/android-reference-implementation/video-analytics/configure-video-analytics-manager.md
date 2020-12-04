---
description: Puede rastrear el uso de vídeo en la implementación de referencia de Android de Primetime configurándola para que funcione con su cuenta de Adobe Analytics.
seo-description: Puede rastrear el uso de vídeo en la implementación de referencia de Android de Primetime configurándola para que funcione con su cuenta de Adobe Analytics.
seo-title: Configurar Video Analytics
title: Configurar Video Analytics
uuid: ce2ebab3-b3c8-472a-9c54-16ddb1c3cc4e
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Configurar Video Analytics {#configure-video-analytics}

Puede rastrear el uso de vídeo en la implementación de referencia de Android de Primetime configurándola para que funcione con su cuenta de Adobe Analytics. La implementación de referencia de Android está diseñada para enviar datos de uso de vídeo y latidos a Adobe Analytics. Para habilitar esta función, primero debe ponerse en contacto con su representante de Adobe Primetime y crear una cuenta de Adobe Analytics.

Hay dos lugares dentro de la implementación de referencia que debe configurar para habilitar la integración de Adobe Analytics. Las configuraciones de Video Analytics en tiempo de ejecución se aplican cuando se selecciona un nuevo vídeo para la reproducción (es decir, una vez creado un nuevo PlayerActiviy).

1. Configure las opciones de tiempo de carga en el archivo de recursos `ADBMobileConfig.json`.

   Este archivo lo proporciona su representante de Adobe. De forma predeterminada, no se incluye en el paquete Primetime SDK. Para obtener más información sobre la configuración de este archivo de configuración, consulte la Guía del programador de Android aquí: Inicialice y configure los análisis de vídeo.
1. Configure las opciones de tiempo de ejecución en el menú Ajustes de implementación de referencia

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opciones de tiempo de ejecución | Descripción |
   |---|---|
   | Servidor de seguimiento de Video Analytics | Dirección URL del punto final de la colección back-end de análisis de vídeo. Aquí es donde se envían todas las llamadas de seguimiento de Video Heartbeat. |
   | Id. de trabajo | Identificador del trabajo de procesamiento. Esto indica al punto final del back-end qué tipo de procesamiento aplicar para las llamadas de seguimiento de vídeo. |
   | Canal | Nombre del canal en el que el usuario está viendo el contenido. En el caso de una aplicación móvil, éste suele ser el nombre de la aplicación. |
   | Editor | El nombre del editor de contenido |
   | Registro de depuración | Activa el registro extenso. Deshabilitado de forma predeterminada, esto puede afectar al rendimiento cuando está habilitado, por lo que puede deshabilitarlo para un entorno de producción. |
   | Modo silencioso | Cuando está habilitada, no se realiza ninguna llamada de red, por lo que sería útil para la depuración local, pero debe deshabilitarse para un entorno de producción. |