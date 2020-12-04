---
description: Para las publicidades (o elementos creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tienen habilitada la regla de reserva, TVSDK trata a una publicidad con un tipo de medio no válido como una publicidad vacía e intenta utilizar las publicidades de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
keywords: zero length ad;empty ad
seo-description: Para las publicidades (o elementos creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tienen habilitada la regla de reserva, TVSDK trata a una publicidad con un tipo de medio no válido como una publicidad vacía e intenta utilizar las publicidades de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
seo-title: Devolución de anuncios para anuncios VAST y VMAP
title: Devolución de anuncios para anuncios VAST y VMAP
uuid: ecfeff31-b723-4a0d-99f2-48705a37b5f0
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Información general {#ad-fallback-for-vast-and-vmap-ads-overview}

Para las publicidades (o elementos creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tienen habilitada la regla de reserva, TVSDK trata a una publicidad con un tipo de medio no válido como una publicidad vacía e intenta utilizar las publicidades de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

La especificación VAST/Digital Video Multiple Ad Playlist (VMAP) establece que para las publicidades que tienen habilitada la opción de reserva VAST, las publicidades vacías activan automáticamente el uso de publicidades de reserva. Cuando un anuncio VAST está vacío, TVSDK busca un reemplazo válido de tipo de medio HLS entre las publicidades de reserva. Cuando un anuncio VAST en un contenedor tiene un tipo de medio no válido, TVSDK lo considera vacío. Puede configurar si TVSDK debe hacer lo mismo con las publicidades en línea en un VMAP. Para obtener más información sobre la función VAST `fallbackOnNoAd`, consulte [Plantilla de servicio de publicidad de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Anuncios**  de longitud cero: cuando TVSDK encuentra una respuesta VAST que contiene un anuncio de duración cero, o una pausa publicitaria sin anuncios, activa eventos AD_BREAK_INICIO / AD_BREAK_COMPLETE para esas pausas publicitarias de longitud cero. *Este comportamiento solo se aplica a flujos VOD.* TVSDK activa estos eventos incluso cuando la aplicación utiliza la directiva de anuncios SKIP.
>
>TVSDK *no* activa los eventos AD_BREAK_INICIO / AD_BREAK_COMPLETE para flujos en directo, o cuando un usuario emplea trickplay o intenta superar el anuncio de longitud cero.

