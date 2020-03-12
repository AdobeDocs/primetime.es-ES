---
description: Para las publicidades (o elementos creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tienen habilitada la regla de reserva, TVSDK trata a una publicidad con un tipo de medio no válido como una publicidad vacía e intenta utilizar las publicidades de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
seo-description: Para las publicidades (o elementos creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tienen habilitada la regla de reserva, TVSDK trata a una publicidad con un tipo de medio no válido como una publicidad vacía e intenta utilizar las publicidades de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.
seo-title: Devolución de anuncios para anuncios VAST y VMAP
title: Devolución de anuncios para anuncios VAST y VMAP
uuid: 5469cd22-7121-49f0-8833-2a525c7ef7d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Devolución de anuncios para anuncios VAST y VMAP {#ad-fallback-for-vast-and-vmap-ads}

Para las publicidades (o elementos creativos) de plantilla de servicio de publicidad de vídeo digital (VAST) que tienen habilitada la regla de reserva, TVSDK trata a una publicidad con un tipo de medio no válido como una publicidad vacía e intenta utilizar las publicidades de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

La especificación VAST/Digital Video Multiple Ad Playlist (VMAP) establece que para las publicidades en las que está habilitada la opción de reserva VAST, las publicidades vacías activan automáticamente el uso de las publicidades de reserva. Cuando un anuncio VAST está vacío, TVSDK busca un reemplazo válido de tipo de medio HLS entre las publicidades de reserva. Cuando un anuncio VAST en un contenedor tiene un tipo de medio no válido, TVSDK lo considera vacío. Puede configurar si TVSDK debe hacer lo mismo con las publicidades en línea en un VMAP. Para obtener más información sobre la función VAST `fallbackOnNoAd` , consulte Plantilla de servicio de publicidad de vídeo [digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definir el comportamiento de las publicidades de reserva para las publicidades en línea de VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Puede activar la opción de reserva cuando una publicidad en línea VMAP contenga un tipo de medio no válido.

1. Establezca `setFallbackOnInvalidCreativeEnabled` en `true` que VMAP se devuelva cuando el tipo de medio de un anuncio lineal/en línea no sea válido para HLS.

   El valor predeterminado es false. Si un anuncio lineal falla porque tiene un tipo de medio no válido o porque no se puede volver a empaquetar el anuncio, este indicador permite que Primetime y la toma de decisiones sigan el mismo comportamiento de reserva que si el anuncio fuera un contenedor VAST vacío.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

## Comportamiento de reserva de anuncios para VAST y VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Cuando Primetime y decisioning encuentra una publicidad VAST (creativa) vacía o con un tipo de medio no válido para HLS, evalúa las publicidades de reserva para determinar qué devolver.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

En TVSDK, el único tipo de medio válido es `application/x-mpegURL` (M3U8).

Cuando hay anuncios alternativos independientes, el complemento Primetime and decisioning busca estas publicidades en el siguiente orden y devuelve el primer anuncio con un tipo de medio válido:

1. Si el reempaquetado está activado, la primera incidencia de una publicidad con un tipo de medio no válido se trata como otros tipos de medios no válidos.

   Si se produce un error en el reempaquetado, este proceso se aplica a otras incidencias de la publicidad.
1. Si TVSDK no encuentra anuncios alternativos válidos, devuelve la publicidad original con el tipo de medio no válido.
1. Si se devuelve una publicidad de reserva con un tipo MIME válido en lugar de la publicidad original, Primetime ad decisioning envía el código de error 403 a la URL de error de VAST, si está disponible.
1. Si una publicidad de reserva es un envolvente y devuelve varias publicidades, solo se devuelven las publicidades con el tipo de medio correcto.

>[!IMPORTANT]
>
>Este comportamiento siempre está habilitado para anuncios en contenedores VAST. Para las publicidades VAST en línea en un VMAP, el comportamiento está deshabilitado de forma predeterminada, pero la aplicación puede habilitarlo.