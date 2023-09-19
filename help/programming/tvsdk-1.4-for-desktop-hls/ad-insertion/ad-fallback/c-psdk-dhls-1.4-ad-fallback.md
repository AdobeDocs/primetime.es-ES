---
description: En el caso de los anuncios (o creativos) de plantilla de servicio de anuncios de vídeo digital (VAST) que tienen la regla de reserva habilitada, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
title: Anuncio alternativo para anuncios VAST y VMAP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Anuncio alternativo para anuncios VAST y VMAP {#ad-fallback-for-vast-and-vmap-ads}

En el caso de los anuncios (o creativos) de plantilla de servicio de anuncios de vídeo digital (VAST) que tienen la regla de reserva habilitada, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

La especificación VAST/Digital Video Multiple Ad Playlist (VMAP) indica que, para los anuncios en los que la opción de reserva VAST está activada, los anuncios vacíos déclencheur automáticamente el uso de anuncios de reserva. Cuando un anuncio VAST está vacío, TVSDK busca un reemplazo de tipo de medios HLS válido entre los anuncios de reserva. Cuando un anuncio VAST de un contenedor tiene un tipo de medios no válido, TVSDK trata este anuncio como vacío. Puede configurar si TVSDK debe hacer lo mismo para los anuncios en línea en un VMAP. Para obtener más información sobre VAST `fallbackOnNoAd` función, consulte [Plantilla de servicio de anuncios de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definir comportamiento de anuncios de reserva para anuncios en línea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Puede activar la reserva cuando un anuncio en línea de VMAP contenga un tipo de medio no válido.

1. Establecer `fallbackOnInvalidCreative` a true para que VMAP se recupere cuando el tipo de medio de un anuncio lineal/en línea no sea válido para HLS.

   El valor predeterminado es false. Si un anuncio lineal falla porque tiene un tipo de medio no válido o porque no se puede volver a empaquetar, este indicador permite que Primetime y Decisioning sigan el mismo comportamiento de reserva que si el anuncio fuera un contenedor VAST vacío.

   ```
   var auditudeMetadata:AuditudeSettings = new AuditudeSettings(); 
   auditudeMetadata.fallbackOnInvalidCreative = true;
   ```

## Comportamiento de reserva de anuncio para VAST y VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Cuando Primetime ad Decisioning encuentra un anuncio VAST (creativo) vacío o con un tipo de medio no válido para HLS, evalúa los anuncios de reserva para determinar qué se debe devolver.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

En TVSDK, los únicos tipos de medios válidos son `application/x-shockwave-flash` (VPAID) y `application/x-mpegURL` (m3u8).

Cuando hay anuncios de reserva independientes, el complemento Primetime ad decisioning examina estos anuncios en el siguiente orden y devuelve el primer anuncio con un tipo de medio válido:

1. Si el reempaquetado está habilitado, la primera aparición de un anuncio con un tipo de medio no válido se trata como otros tipos de medio no válidos.

   Si falla el reempaquetado, este proceso se aplica a ocurrencias adicionales del anuncio.
1. Si TVSDK no encuentra anuncios de reserva válidos, devuelve el anuncio original con el tipo de medio no válido.
1. Si se devuelve un anuncio de reserva con un tipo MIME válido en lugar del anuncio original, Primetime ad decisioning enviará el código de error 403 a la URL de error VAST, si está disponible.
1. Si un anuncio de reserva es un contenedor y devuelve varios anuncios, solo se devuelven los anuncios con el tipo de medio correcto.

>[!IMPORTANT]
>
>Este comportamiento siempre está habilitado para los anuncios en contenedores VAST. Para los anuncios VAST en línea en un VMAP, el comportamiento está deshabilitado de forma predeterminada, pero la aplicación puede habilitarlo.
