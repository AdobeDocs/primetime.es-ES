---
description: En el caso de los anuncios (o creativos) de plantilla de servicio de anuncios de vídeo digital (VAST) que tienen la regla de reserva habilitada, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
keywords: anuncio de longitud cero;anuncio vacío
title: Anuncio alternativo para anuncios VAST y VMAP
exl-id: 5cabb5f6-b895-48bc-9c9e-b22dd47539bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Anuncio alternativo para anuncios VAST y VMAP {#ad-fallback-for-vast-and-vmap-ads}

En el caso de los anuncios (o creativos) de plantilla de servicio de anuncios de vídeo digital (VAST) que tienen la regla de reserva habilitada, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

La especificación VAST/Digital Video Multiple Ad Playlist (VMAP) indica que, para los anuncios que tienen habilitada la opción de reserva VAST, los anuncios vacíos déclencheur automáticamente el uso de anuncios de reserva. Cuando un anuncio VAST está vacío, TVSDK busca un reemplazo de tipo de medios HLS válido entre los anuncios de reserva. Cuando un anuncio VAST de un contenedor tiene un tipo de medios no válido, TVSDK trata este anuncio como vacío. Puede configurar si TVSDK debe hacer lo mismo para los anuncios en línea en un VMAP. Para obtener más información sobre VAST `fallbackOnNoAd` función, consulte [Plantilla de servicio de anuncios de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Anuncios de longitud cero** : Cuando TVSDK encuentra una respuesta VAST que contiene un anuncio de duración cero o una pausa publicitaria sin anuncios, activa eventos AD_BREAK_START / AD_BREAK_COMPLETE para esas pausas publicitarias de longitud cero. *Este comportamiento solo se aplica a los flujos de VOD.* TVSDK activa estos eventos incluso cuando la aplicación utiliza la directiva de omisión de anuncios.
>
>TVSDK sí *no* desencadena eventos AD_BREAK_START / AD_BREAK_COMPLETE para emisiones en directo, o cuando un usuario emplea trickplay o intenta pasar el anuncio de longitud cero.
