---
description: Algunos anuncios (o elementos creativos) de terceros no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo es incompatible con HLS. La inserción de anuncios de Primetime y TVSDK pueden, opcionalmente, intentar volver a empaquetar anuncios incompatibles en vídeos compatibles de M3U8.
title: Volver a empaquetar anuncios incompatibles mediante el servicio de reempaquetado creativo de Adobe (CRS)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Volver a empaquetar anuncios incompatibles mediante el servicio de reempaquetado creativo de Adobe (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Algunos anuncios (o elementos creativos) de terceros no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo es incompatible con HLS. La inserción de anuncios de Primetime y TVSDK pueden, opcionalmente, intentar volver a empaquetar anuncios incompatibles en vídeos compatibles de M3U8.

Los anuncios publicados por terceros, como un servidor de publicidad de agencia, su socio de inventario o una red de publicidad, suelen entregarse en formatos incompatibles, como el formato MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez un anuncio incompatible, el reproductor ignora el anuncio y envía una solicitud al servicio de reempaquetado creativo (CRS), que forma parte del back-end de inserción de anuncio de Primetime, para volver a empaquetar el anuncio en un formato compatible. CRS intenta generar varias representaciones M3U8 de velocidad de bits del anuncio y almacena estas representaciones en la red de entrega de contenido (CDN) de Primetime. La próxima vez que TVSDK reciba una respuesta de anuncio que apunte a ese anuncio, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para activar esta función opcional de CRS, póngase en contacto con su representante de Adobe.

>[!NOTE]
>
>Para los clientes de CRS versión 3.0 (y anteriores), a partir de CRS versión 3.1, los siguientes cambios han mejorado tanto la seguridad como el rendimiento:
>
>* CRS 3.1 continúa con `https:` si el contenido que se reempaqueta utiliza `https:`. Esto reduce el potencial de algunos reproductores para presentar contenido no seguro.
   >
   >
* CRS 3.1 minimiza en gran medida las llamadas de red, lo que mejora el tiempo de inicio del vídeo.

>



## Habilitar CRS en aplicaciones TVSDK {#enable-crs-in-tvsdk-applications}

Para habilitar CRS en las aplicaciones TVSDK, debe establecer la siguiente información en la configuración de Auditude:

1. Habilitar CRS en `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
