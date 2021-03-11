---
description: En el caso de los anuncios (o creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tengan habilitada la regla de reserva, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
title: Devolución de anuncios para anuncios VAST y VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Devolución de anuncios para anuncios VAST y VMAP {#ad-fallback-for-vast-and-vmap-ads}

En el caso de los anuncios (o creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tengan habilitada la regla de reserva, TVSDK trata un anuncio con un tipo de medio no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

La especificación VAST/Digital Video Multiple Ad Playlist (VMAP) indica que, para los anuncios en los que está habilitada la alternativa VAST, los anuncios vacíos déclencheur automáticamente el uso de anuncios de reserva. Cuando un anuncio VAST está vacío, TVSDK busca un reemplazo de tipo de medio HLS válido entre los anuncios de reserva. Cuando un anuncio VAST en un contenedor tiene un tipo de medio no válido, TVSDK lo considera vacío. Puede configurar si TVSDK debe hacer lo mismo con los anuncios en línea en un VMAP. Para obtener más información sobre la función VAST `fallbackOnNoAd`, consulte [Plantilla de servicio de publicidad de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Defina el comportamiento de los anuncios en línea de VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Puede activar la alternativa cuando un anuncio en línea VMAP contiene un tipo de medio no válido.

1. Configure `setFallbackOnInvalidCreativeEnabled` en `true` para que VMAP vuelva a aparecer cuando el tipo de medio de un anuncio lineal/en línea no sea válido para HLS.

   El valor predeterminado es false. Si un anuncio lineal falla porque tiene un tipo de medio no válido o porque no se puede volver a empaquetar, este indicador permite que la toma de decisiones de anuncios de Primetime siga el mismo comportamiento de reserva que si el anuncio fuera un envoltorio VAST vacío.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

## Comportamiento de reserva de anuncio para VAST y VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Cuando la toma de decisiones de anuncios de Primetime encuentra un anuncio VAST (creativo) vacío o con un tipo de medio no válido para HLS, evalúa los anuncios de reserva para determinar qué se debe devolver.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

En TVSDK, el único tipo de medio válido es `application/x-mpegURL` (M3U8).

Cuando hay anuncios de reserva independientes, el complemento Primetime ad decisioning busca estos anuncios en el siguiente orden y devuelve el primer anuncio con un tipo de medio válido:

1. Si el reempaquetado está habilitado, la primera incidencia de un anuncio con un tipo de medio no válido se trata como otros tipos de medios no válidos.

   Si el reempaquetado falla, este proceso se aplica a ocurrencias adicionales del anuncio.
1. Si TVSDK no encuentra anuncios de reserva válidos, devuelve el anuncio original con el tipo de medio no válido.
1. Si se devuelve un anuncio de reserva con un tipo MIME válido en lugar del anuncio original, Primetime ad decisioning envía el código de error 403 a la URL de error VAST, si está disponible.
1. Si un anuncio de reserva es un envoltorio y devuelve varios anuncios, solo se devuelven los anuncios con el tipo de medio correcto.

>[!IMPORTANT]
>
>Este comportamiento siempre está habilitado para los anuncios en contenedores VAST. Para los anuncios VAST en línea en un VMAP, el comportamiento está deshabilitado de forma predeterminada, pero la aplicación puede habilitarlo.