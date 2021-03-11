---
description: Puede realizar un seguimiento del uso de vídeo integrando TVSDK con Adobe Analytics.
title: Integración de Video Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Integración de Video Analytics {#video-analytics-integration}

Puede realizar un seguimiento del uso de vídeo integrando TVSDK con Adobe Analytics.

El seguimiento de vídeo en TVSDK utiliza el servicio **Adobe Analytics Video Essentials**, que proporciona métricas de participación en el vídeo, como vistas de vídeo, vídeos completados, impresiones de anuncios, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con su representante de Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de vídeo en el reproductor:

1. Inicialice y/o configure los siguientes componentes de seguimiento de vídeo:

   En iOS, estos componentes forman parte de TVSDK:

   * Archivo de configuración JSON
   * Objeto de metadatos de Video Analytics
   * Objeto de metadatos global
   * Objeto Rastreador de Video Analytics

1. Configure informes de análisis de vídeo en el servidor mediante las herramientas de administración de Adobe Analytics.