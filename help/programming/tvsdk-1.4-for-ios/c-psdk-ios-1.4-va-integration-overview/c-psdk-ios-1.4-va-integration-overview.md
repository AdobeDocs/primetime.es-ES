---
description: Puede realizar el seguimiento del uso del vídeo integrando TVSDK con Adobe Analytics.
seo-description: Puede realizar el seguimiento del uso del vídeo integrando TVSDK con Adobe Analytics.
seo-title: Análisis de vídeo
title: Análisis de vídeo
uuid: 8f297316-f95e-4896-b489-a2d6b36e6b40
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Integración de análisis de vídeo {#video-analytics-integration}

Puede realizar el seguimiento del uso del vídeo integrando TVSDK con Adobe Analytics.

El seguimiento de vídeo en TVSDK utiliza el servicio **Adobe Analytics Video Essentials**, que proporciona métricas de participación en vídeo, como vistas de vídeo, vídeos completos, impresiones de publicidad, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con su representante de Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de videos en el reproductor:

1. Inicialice y/o configure los siguientes componentes de seguimiento de vídeo:

   En iOS, estos componentes forman parte de TVSDK:

   * Archivo de configuración JSON
   * Objeto de metadatos de análisis de vídeo
   * Objeto de metadatos global
   * Objeto de rastreador de análisis de vídeo

1. Configure el sistema de informes de análisis de vídeo en el servidor mediante las herramientas de administración de Adobe Analytics.