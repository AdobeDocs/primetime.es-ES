---
description: El servicio de reenvasado creativo (CRS) garantiza que un creativo de publicidad que no sea de HLS pueda reproducir correctamente en flujos HLS. El servidor de manifiesto llama a CRS cuando encuentra un anuncio que no es HLS.
title: Información general de CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Información general de CRS {#overview-of-crs}

El servicio de reenvasado creativo (CRS) garantiza que un creativo de publicidad que no sea de HLS pueda reproducir correctamente en flujos HLS. El servidor de manifiesto llama a CRS cuando encuentra un anuncio que no es HLS.

>[!NOTE]
>
>De forma predeterminada, CRS está deshabilitado. Para habilitar CRS en su cuenta, póngase en contacto con el administrador técnico de cuentas de Adobe.
>
>Para obtener información sobre la activación de CRS en aplicaciones TVSDK, consulte la *Habilitar CRS en aplicaciones TVSDK* en la Guía del programador para su plataforma. Por ejemplo, para Android 3.4, consulte [Habilitar CRS en aplicaciones TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepara los anuncios creativos de HTTP Live Streaming (HLS) para el flujo de contenido e inserta paquetes ID3 para el seguimiento de anuncios del lado del cliente. Transcodifica los archivos MP4, FLV y WebM recibidos de servidores de publicidad de terceros, redes de publicidad y servidores de agencias al formato HLS.

Cuando la inserción de anuncios de Adobe Primetime encuentra un creativo de publicidad que no es HLS, lo envía a CRS para que lo reempaquete, lo que generalmente no dura más de tres minutos. CRS envía el anuncio transcodificado creativo al servidor CDN para su uso futuro. Esto se llama **`just-in-time (JIT) repackaging`**. También puede transcodificar anuncios creativos antes de que sean necesarios utilizando  [API de reempaquetado](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . Esto se llama *`asynchronous repackaging`*.

El administrador de cuentas técnico de Adobe también puede cambiar algunos comportamientos predeterminados de CRS si otro comportamiento es más adecuado para su aplicación. Estos son:

* Prioridad de los formatos creativos de publicidad.

   El `MediaFiles` de una respuesta VAST/VMAP puede contener elementos creativos con diferentes `MediaFile` tipos. De forma predeterminada, el servidor de manifiesto selecciona una de acuerdo con un conjunto fijo de prioridades ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). El Adobe puede cambiar las prioridades de su cuenta.
* Duración del objetivo del anuncio.

   El servidor de manifiesto detecta el destino y la duración de la lista de reproducción de contenido y la envía a CRS. Adobe puede cambiar este comportamiento para que CRS siempre utilice una duración fija que especifique para su cuenta.
