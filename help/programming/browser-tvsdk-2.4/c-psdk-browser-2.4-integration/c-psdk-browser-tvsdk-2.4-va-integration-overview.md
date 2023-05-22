---
description: Puede rastrear el uso de vídeo integrando el TVSDK del explorador con Adobe Analytics.
title: Análisis de vídeo
exl-id: b6fb39a9-6cb8-4498-a9fa-0ea19af52a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Análisis de vídeo{#video-analytics}

Puede rastrear el uso de vídeo integrando el TVSDK del explorador con Adobe Analytics.

El seguimiento de vídeo en el explorador TVSDK utiliza **Adobe Analytics Video Essentials** El servicio, que proporciona métricas de participación de vídeo, como vistas de vídeo, visualizaciones de vídeo completas, impresiones de publicidad, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con el representante del Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de vídeo en el reproductor:

1. Inicialice o configure los siguientes componentes de seguimiento de vídeo:

   * **Biblioteca de AppMeasurement** : contiene la lógica principal de recopilación de datos de bajo nivel. Aquí es donde se acumulan los datos de Video Heartbeat y se envían a través de la red.
   * **Biblioteca de Video Heartbeat** : contiene la lógica principal de recopilación de datos de Video-Heartbeat. La biblioteca de latidos de vídeo accede a un subconjunto de las API de biblioteca de AppMeasurement.

      >[!TIP]
      >
      >La aplicación no interactúa directamente con el código de Video Heartbeat. En su lugar, la aplicación utiliza las API de TVSDK del explorador para configurar las funcionalidades de seguimiento de vídeo del reproductor.

   * **Biblioteca VisitorID** : Identifica de forma exclusiva a los visitantes de la página web que aloja el reproductor de vídeo.
   >[!IMPORTANT]
   >
   >La capacidad de seguimiento de vídeo integrada del TVSDK del explorador depende de una instancia de AppMeasurement configurada correctamente. Los elementos de seguimiento suponen que la biblioteca AppMeasurement ya tiene instancias creadas y configuradas antes de configurar y activar el seguimiento de vídeo. Las funcionalidades de seguimiento de vídeo de TVSDK del explorador dependen de la existencia de una instancia totalmente funcional y configurada correctamente de la biblioteca de AppMeasurement.

1. Configure los informes de análisis de vídeo en el servidor mediante las Herramientas de administración de Adobe Analytics.
