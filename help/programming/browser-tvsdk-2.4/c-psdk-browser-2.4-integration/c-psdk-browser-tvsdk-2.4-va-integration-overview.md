---
description: Puede realizar el seguimiento del uso del vídeo integrando el SDK de TVSDK del explorador con Adobe Analytics.
seo-description: Puede realizar el seguimiento del uso del vídeo integrando el SDK de TVSDK del explorador con Adobe Analytics.
seo-title: Análisis de vídeo
title: Análisis de vídeo
uuid: 6351933b-c0f3-4e3e-ad27-bedc8eecc312
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Análisis de vídeo{#video-analytics}

Puede realizar el seguimiento del uso del vídeo integrando el SDK de TVSDK del explorador con Adobe Analytics.

El seguimiento de vídeo en el navegador TVSDK utiliza el servicio Video Essentials **de** Adobe Analytics, que proporciona métricas de participación en vídeo, como vistas de vídeo, vídeos completos, impresiones de publicidad, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con su representante de Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de videos en el reproductor:

1. Inicialice y/o configure los siguientes componentes de seguimiento de vídeo:

   * **Biblioteca** de AppMeasurement: contiene la lógica principal de recopilación de datos de bajo nivel. Aquí es donde los datos de Video Heartbeat se acumulan y envían a través de la red.
   * **Video Heartbeat Library** : contiene la lógica principal de recopilación de datos de Video Heartbeat. Video Heartbeat Library accede a un subconjunto de las API de biblioteca de AppMeasurement.

      >[!TIP]
      >
      >La aplicación no interactúa directamente con el código de Video Heartbeat. En su lugar, la aplicación utiliza las API de TVSDK del explorador para configurar las funciones de seguimiento de vídeo del reproductor.

   * **Biblioteca** VisitorID: identifica de forma exclusiva a los visitantes de la página web que aloja el reproductor de vídeo.
   >[!IMPORTANT]
   >
   >La capacidad de seguimiento de vídeo integrada TVSDK del explorador depende de una instancia de AppMeasurement configurada correctamente. Los elementos de seguimiento suponen que la biblioteca AppMeasurement ya está creada y configurada antes de configurar y activar el seguimiento de videos. Las funciones de seguimiento de vídeo TVSDK del explorador dependen de la existencia de una instancia de la biblioteca AppMeasurement completamente funcional y configurada correctamente.

1. Configure informes de análisis de vídeo en el servidor mediante las herramientas de administración de Adobe Analytics.