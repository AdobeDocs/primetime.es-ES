---
description: El servicio de reempaquetado creativo (CRS) garantiza que un creativo de publicidad que no sea HLS pueda reproducirse correctamente en los flujos HLS. El servidor de manifiesto llama en CRS cuando encuentra un anuncio que no es de HLS.
title: Información general sobre CRS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Información general sobre CRS {#overview-of-crs}

El servicio de reempaquetado creativo (CRS) garantiza que un creativo de publicidad que no sea HLS pueda reproducirse correctamente en los flujos HLS. El servidor de manifiesto llama en CRS cuando encuentra un anuncio que no es de HLS.

>[!NOTE]
>
>De forma predeterminada, CRS está deshabilitado. Para habilitar CRS para su cuenta, póngase en contacto con el administrador técnico de cuentas de Adobe.
>
>Para obtener información sobre cómo habilitar CRS en aplicaciones TVSDK, consulte el tema *Habilitar CRS en aplicaciones TVSDK* en la Guía del programador para su plataforma. Por ejemplo, para Android 3.4, consulte [Habilitar CRS en aplicaciones TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepara los creativos publicitarios de HTTP Live Streaming (HLS) para el flujo de contenido e inyecta paquetes ID3 para el seguimiento de anuncios del lado del cliente. Transcodifica los archivos MP4, FLV y WebM recibidos de servidores de publicidad de terceros, redes de anuncios y servidores de agencias al formato HLS.

Cuando la inserción de publicidad de Adobe Primetime encuentra un creativo de publicidad que no es de HLS, lo envía a CRS para su reempaquetado, que normalmente no tarda más de tres minutos. CRS envía el creativo de anuncios transcodificados al servidor de CDN para su uso futuro. Esto se llama **`just-in-time (JIT) repackaging`**. También puede transcodificar los creativos de anuncios antes de que sean necesarios mediante la [API de reempaquetado](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . Esto se llama *`asynchronous repackaging`*.

El administrador técnico de cuentas de Adobe también puede cambiar algunos comportamientos predeterminados de CRS si otro comportamiento es más adecuado para su aplicación. Estos son:

* Prioridad de los formatos creativos de publicidad.

   La sección `MediaFiles` de una respuesta VAST/VMAP puede contener elementos creativos con diferentes tipos de `MediaFile`. De forma predeterminada, el servidor de manifiesto selecciona uno según un conjunto fijo de prioridades ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe puede cambiar las prioridades de su cuenta.
* Duración del objetivo del anuncio.

   El servidor de manifiestos detecta el destino y la duración de la publicidad de la lista de reproducción de contenido y la envía a CRS. El Adobe puede cambiar este comportamiento para que CRS siempre utilice una duración fija que especifique para su cuenta.
