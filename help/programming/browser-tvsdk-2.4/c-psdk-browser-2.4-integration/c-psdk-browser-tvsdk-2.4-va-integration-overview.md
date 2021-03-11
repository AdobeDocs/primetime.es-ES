---
description: Puede realizar un seguimiento del uso de vídeo integrando el SDK de TVSDK del explorador con Adobe Analytics.
title: Análisis de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Análisis de vídeo{#video-analytics}

Puede realizar un seguimiento del uso de vídeo integrando el SDK de TVSDK del explorador con Adobe Analytics.

El seguimiento de vídeo en el SDK de explorador utiliza el servicio **Adobe Analytics Video Essentials**, que proporciona métricas de participación en el vídeo, como vistas de vídeo, vídeos completados, impresiones de anuncios, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con su representante de Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de vídeo en el reproductor:

1. Inicialice y/o configure los siguientes componentes de seguimiento de vídeo:

   * **Biblioteca de AppMeasurement** : contiene la lógica principal de recopilación de datos de bajo nivel. Aquí es donde los datos de Video Heartbeat se acumulan y envían a través de la red.
   * **Video Heartbeat Library** : contiene la lógica principal de recopilación de datos de Video Heartbeat. Video Heartbeat Library accede a un subconjunto de las API de biblioteca de AppMeasurement.

      >[!TIP]
      >
      >La aplicación no interactúa directamente con el código de Video Heartbeat. En su lugar, la aplicación utiliza las API de TVSDK del explorador para configurar las capacidades de seguimiento de vídeo del reproductor.

   * **Biblioteca VisitorID** : identifica de forma exclusiva a los visitantes de la página web que aloja el reproductor de vídeo.
   >[!IMPORTANT]
   >
   >La capacidad de seguimiento de vídeo integrada TVSDK del explorador depende de una instancia AppMeasurement configurada correctamente. Los elementos de seguimiento suponen que la biblioteca AppMeasurement ya está creada y configurada antes de configurar y activar el seguimiento de vídeo. Las capacidades de seguimiento de vídeo TVSDK del explorador dependen de la existencia de una instancia de la biblioteca AppMeasurement completamente funcional y configurada correctamente.

1. Configure informes de análisis de vídeo en el servidor mediante las herramientas de administración de Adobe Analytics.