---
description: Puede rastrear el uso de vídeo integrando TVSDK con Adobe Analytics.
title: Integración de análisis de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Integración de análisis de vídeo {#video-analytics-integration}

Puede rastrear el uso de vídeo integrando TVSDK con Adobe Analytics.

El seguimiento de vídeo en TVSDK utiliza **Adobe Analytics Video Essentials** El servicio, que proporciona métricas de participación de vídeo, como vistas de vídeo, visualizaciones de vídeo completas, impresiones de publicidad, tiempo invertido en vídeo, etc. Para obtener más información sobre este servicio, póngase en contacto con el representante del Adobe.

El siguiente procedimiento resume los pasos para activar el seguimiento de vídeo en el reproductor:

1. Inicialice o configure los siguientes componentes de seguimiento de vídeo:

   En iOS, estos componentes forman parte de TVSDK:

   * Archivo de configuración JSON
   * Objeto de metadatos de análisis de vídeo
   * Objeto de metadatos globales
   * Objeto Rastreador de análisis de vídeo

1. Configure los informes de análisis de vídeo en el servidor mediante las Herramientas de administración de Adobe Analytics.
