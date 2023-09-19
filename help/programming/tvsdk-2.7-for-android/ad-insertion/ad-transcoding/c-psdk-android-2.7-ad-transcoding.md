---
description: Algunos anuncios de terceros (o creativos) no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime ad insertion y TVSDK pueden intentar opcionalmente volver a empaquetar anuncios incompatibles en vídeos M3U8 compatibles.
title: Reempaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe (CRS)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Reempaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Algunos anuncios de terceros (o creativos) no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime ad insertion y TVSDK pueden intentar opcionalmente volver a empaquetar anuncios incompatibles en vídeos M3U8 compatibles.

Los anuncios ofrecidos por varios terceros, como un servidor de publicidad de una agencia, su partner de inventario o una red de publicidad, a menudo se entregan en formatos incompatibles, como el formato MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez un anuncio incompatible, el reproductor ignora el anuncio y envía una solicitud al servicio de reempaquetado creativo (CRS), que forma parte del back-end de inserción de anuncios de Primetime, para que vuelva a empaquetar el anuncio en un formato compatible. CRS intenta generar varias representaciones M3U8 de velocidad de bits de la publicidad y almacena estas representaciones en la red de entrega de contenido de Primetime (CDN). La próxima vez que TVSDK reciba una respuesta de anuncio que apunte a ese anuncio, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para activar esta función CRS opcional, póngase en contacto con el representante del Adobe.

>[!NOTE]
>
>Para los clientes de CRS versión 3.0 (y anteriores), a partir de CRS versión 3.1, los siguientes cambios han mejorado tanto la seguridad como el rendimiento:
>
>* CRS 3.1 continúa con `https:` si el contenido que se está reempaquetando utiliza `https:`. Esto reduce el potencial de algunos reproductores para presentar contenido no seguro.
>
>* CRS 3.1 minimiza considerablemente las llamadas de red, lo que mejora el tiempo de inicio del vídeo.
>

Para obtener más información sobre CRS, consulte [Servicio Creative Packaging (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf).

## Habilitar CRS en aplicaciones TVSDK{#enable-crs-in-tvsdk-applications}

Para habilitar CRS en las aplicaciones TVSDK, debe establecer la siguiente información en la configuración del Auditude:

1. Habilitar CRS en `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
