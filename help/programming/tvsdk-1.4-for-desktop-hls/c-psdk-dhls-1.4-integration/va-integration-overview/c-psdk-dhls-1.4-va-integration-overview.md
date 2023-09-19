---
description: Puede rastrear el uso de vídeo integrando TVSDK con Adobe Analytics.
title: Análisis de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Análisis de vídeo{#video-analytics}

Puede rastrear el uso de vídeo integrando TVSDK con Adobe Analytics.

El seguimiento de vídeo en TVSDK utiliza **Adobe Analytics Video Essentials** El servicio, que proporciona métricas de participación de vídeo, como vistas de vídeo, visualizaciones de vídeo completas, impresiones de publicidad, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con el representante del Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de vídeo en el reproductor:

1. Inicialice o configure los siguientes componentes de seguimiento de vídeo:

   * **biblioteca de AppMeasurementes** : contiene la lógica principal de recopilación de datos de bajo nivel. Aquí es donde se acumulan los datos de Video Heartbeat y se envían a través de la red.
   * **Biblioteca de Video Heartbeat** : contiene la lógica principal de recopilación de datos de Video-Heartbeat. La biblioteca de latidos de vídeo accede a un subconjunto del `AppMeasurement` API de biblioteca.

     >[!TIP]
     >
     >La aplicación no interactúa directamente con el código de Video Heartbeat. En su lugar, la aplicación utiliza las API de TVSDK para configurar las funcionalidades de seguimiento de vídeo del reproductor.

   * **Biblioteca VisitorID** : Identifica de forma exclusiva a los visitantes de la página web que aloja el reproductor de vídeo.

   >[!IMPORTANT]
   >
   >La capacidad de seguimiento de vídeo integrada de TVSDK depende de un configurado correctamente `AppMeasurement` ejemplo. Los elementos de seguimiento suponen que la variable `AppMeasurement` La biblioteca de ya está instanciada y configurada antes de configurar y activar el seguimiento de vídeo. Las funcionalidades de seguimiento de vídeo de TVSDK dependen de la existencia de una instancia de totalmente funcional y correctamente configurada de `AppMeasurement` biblioteca.

1. Configure los informes de análisis de vídeo en el servidor mediante las Herramientas de administración de Adobe Analytics.
