---
description: Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.
seo-description: Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.
seo-title: Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe (CRS)
title: Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe (CRS)
uuid: c3961628-39aa-444c-9c93-9f1e267d9cd4
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Volver a empaquetar anuncios incompatibles mediante el servicio de reempaquetado creativo (CRS) de Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.

Las publicidades que se proporcionan desde varios terceros, como un servidor de publicidad de la agencia, su socio de inventario o una red de publicidad, suelen entregarse en formatos incompatibles, como el formato MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez una publicidad incompatible, el reproductor ignora la publicidad y envía una solicitud al servicio creativo de reempaquetado (CRS), que forma parte del back-end de inserción y Primetime, para volver a empaquetar la publicidad en un formato compatible. CRS intenta generar varias representaciones M3U8 de velocidad de bits del anuncio y almacena estas representaciones en la red de Envío de contenido Primetime (CDN). La próxima vez que TVSDK reciba una respuesta de publicidad que apunte a esa publicidad, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para activar esta función de CRS opcional, póngase en contacto con su representante de Adobe.

>[!NOTE]
>
>Para los clientes de CRS versión 3.0 (y anteriores), a partir de CRS versión 3.1, los siguientes cambios han mejorado tanto la seguridad como el rendimiento:
>
>* CRS 3.1 continúa con `https:` si el contenido que se reempaqueta utiliza `https:`. Esto reduce el potencial de algunos reproductores para presentar contenido no seguro.
   >
   >
* CRS 3.1 minimiza en gran medida las llamadas de red, lo que mejora el tiempo de inicio del vídeo.

>



Para obtener más información sobre CRS, consulte [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf).

## Habilitar CRS en aplicaciones TVSDK{#enable-crs-in-tvsdk-applications}

Para habilitar CRS en las aplicaciones TVSDK, debe definir la siguiente información en la configuración de Auditude:

1. Habilite CRS en `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
