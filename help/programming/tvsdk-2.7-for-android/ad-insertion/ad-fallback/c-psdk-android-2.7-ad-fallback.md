---
description: En el caso de los anuncios (o creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tengan habilitada la regla de reserva, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
keywords: anuncio de longitud cero;anuncio vacío
title: Devolución de anuncios para anuncios VAST y VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Información general {#ad-fallback-for-vast-and-vmap-ads-overview}

En el caso de los anuncios (o creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tengan habilitada la regla de reserva, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

La especificación VAST/Digital Video Multiple Ad Playlist (VMAP) indica que, para los anuncios que tienen habilitada la alternativa VAST, los anuncios vacíos déclencheur automáticamente el uso de anuncios de reserva. Cuando un anuncio VAST está vacío, TVSDK busca un reemplazo de tipo de medio HLS válido entre los anuncios de reserva. Cuando un anuncio VAST en un contenedor tiene un tipo de medio no válido, TVSDK lo considera vacío. Puede configurar si TVSDK debe hacer lo mismo con los anuncios en línea en un VMAP. Para obtener más información sobre la función VAST `fallbackOnNoAd`, consulte [Plantilla de servicio de publicidad de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Anuncios de longitud cero** : cuando TVSDK encuentra una respuesta VAST que contiene un anuncio de duración cero o una pausa publicitaria sin anuncios, activa eventos AD_BREAK_START / AD_BREAK_COMPLETE para esas pausas publicitarias de longitud cero. *Este comportamiento solo se aplica a los flujos de VOD.* TVSDK activa estos eventos incluso cuando la aplicación utiliza la directiva de publicidad SKIP.
>
>TVSDK desencadena eventos *not* AD_BREAK_START / AD_BREAK_COMPLETE para transmisiones en directo, o cuando un usuario utiliza trickplay o busca pasar el anuncio de longitud cero.

