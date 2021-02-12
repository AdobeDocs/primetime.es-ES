---
description: El servicio de reempaquetado creativo (CRS) garantiza que un creativo de publicidad que no sea HLS pueda reproducirse correctamente en flujos HLS. El servidor de manifiesto llama a CRS cuando encuentra una publicidad que no es HLS.
seo-description: El servicio de reempaquetado creativo (CRS) garantiza que un creativo de publicidad que no sea HLS pueda reproducirse correctamente en flujos HLS. El servidor de manifiesto llama a CRS cuando encuentra una publicidad que no es HLS.
seo-title: Descripción general de CRS
title: Descripción general de CRS
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Información general sobre CRS {#overview-of-crs}

El servicio de reempaquetado creativo (CRS) garantiza que un creativo de publicidad que no sea HLS pueda reproducirse correctamente en flujos HLS. El servidor de manifiesto llama a CRS cuando encuentra una publicidad que no es HLS.

>[!NOTE]
>
>De forma predeterminada, CRS está desactivado. Para habilitar CRS para su cuenta, póngase en contacto con el administrador técnico de su cuenta de Adobe.
>
>Para obtener información sobre cómo activar CRS en aplicaciones TVSDK, consulte el tema *Habilitar CRS en aplicaciones TVSDK* en la Guía del programador para su plataforma. Por ejemplo, para Android 3.4, consulte [Habilitar CRS en aplicaciones TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepara elementos creativos publicitarios de HTTP Live Streaming (HLS) para el flujo de contenido e inyecta paquetes ID3 para el seguimiento de anuncios del lado del cliente. Transcodifica archivos MP4, FLV y WebM recibidos de servidores de publicidad de terceros, redes de publicidad y servidores de agencias al formato HLS.

Cuando la inserción de anuncios de Adobe Primetime encuentra un elemento creativo de publicidad que no es HLS, lo envía a CRS para su reempaquetado, lo que no suele tardar más de tres minutos. CRS envía el elemento creativo de la publicidad transcodificada al servidor CDN para su uso futuro. Esto se denomina **`just-in-time (JIT) repackaging`**. También puede transcodificar los elementos creativos de publicidad antes de que sean necesarios mediante la [API de reempaquetado](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . Esto se denomina *`asynchronous repackaging`*.

El administrador de cuentas técnico de Adobe también puede cambiar algunos comportamientos predeterminados de CRS si se adapta mejor a la aplicación. Estos son:

* Prioridad de los formatos creativos de publicidad.

   La sección `MediaFiles` de una respuesta VAST/VMAP puede contener elementos creativos con diferentes tipos `MediaFile`. De forma predeterminada, el servidor de manifiesto selecciona una según un conjunto fijo de prioridades ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe puede cambiar las prioridades de su cuenta.
* Duración del destinatario de publicidad.

   El servidor de manifiesto detecta la duración de la publicidad de destinatario desde la lista de reproducción de contenido y la envía a CRS. Adobe puede cambiar este comportamiento para que CRS siempre utilice una duración fija que usted especifique para su cuenta.
