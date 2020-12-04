---
description: Puede realizar el seguimiento del uso del vídeo integrando TVSDK con Adobe Analytics.
seo-description: Puede realizar el seguimiento del uso del vídeo integrando TVSDK con Adobe Analytics.
seo-title: Análisis de vídeo
title: Análisis de vídeo
uuid: c3cb0574-1117-409c-8aa7-641363d8d85f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Análisis de vídeo{#video-analytics}

Puede realizar el seguimiento del uso del vídeo integrando TVSDK con Adobe Analytics.

El seguimiento de vídeo en TVSDK utiliza el servicio **Adobe Analytics Video Essentials**, que proporciona métricas de participación en vídeo, como vistas de vídeo, vídeos completos, impresiones de publicidad, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con su representante de Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de videos en el reproductor:

1. Inicialice y/o configure los siguientes componentes de seguimiento de vídeo:

   * **Biblioteca**  de AppMeasurement: contiene la lógica principal de recopilación de datos de bajo nivel. Aquí es donde los datos de Video Heartbeat se acumulan y envían a través de la red.
   * **Video Heartbeat Library** : contiene la lógica principal de recopilación de datos de Video Heartbeat. Video Heartbeat Library accede a un subconjunto de las API de biblioteca `AppMeasurement`.

      >[!TIP]
      >
      >La aplicación no interactúa directamente con el código de Video Heartbeat. En su lugar, la aplicación utiliza las API de TVSDK para configurar las funciones de seguimiento de vídeo del reproductor.

   * **Biblioteca**  VisitorID: identifica de forma exclusiva los visitantes a la página web que aloja el reproductor de vídeo.
   >[!IMPORTANT]
   >
   >La capacidad de seguimiento de vídeo integrada de TVSDK depende de una instancia `AppMeasurement` configurada correctamente. Los elementos de seguimiento suponen que la biblioteca `AppMeasurement` ya está creada y configurada antes de configurar y activar el seguimiento de video. Las funciones de seguimiento de vídeo TVSDK dependen de la existencia de una instancia de la biblioteca `AppMeasurement` completamente funcional y configurada correctamente.

1. Configure el sistema de informes de análisis de vídeo en el servidor mediante las herramientas de administración de Adobe Analytics.

