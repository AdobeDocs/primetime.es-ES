---
description: Cuando Primetime ad decisionesencuentra una publicidad VAST (creativa) vacía o con un tipo de medio no válido para HLS, evalúa las publicidades de reserva para determinar qué devolver.
seo-description: Cuando Primetime ad decisionesencuentra una publicidad VAST (creativa) vacía o con un tipo de medio no válido para HLS, evalúa las publicidades de reserva para determinar qué devolver.
seo-title: Comportamiento de reserva de anuncios para VAST y VMAP
title: Comportamiento de reserva de anuncios para VAST y VMAP
uuid: 50e17372-fd29-4792-aafa-8f9c21cc42c6
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Comportamiento de reserva de anuncios para VAST y VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Cuando Primetime ad decisionesencuentra una publicidad VAST (creativa) vacía o con un tipo de medio no válido para HLS, evalúa las publicidades de reserva para determinar qué devolver.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

En TVSDK, el único tipo de medio válido es `application/x-mpegURL` (M3U8).

Cuando hay publicidades de reserva independientes, el complemento Primetime ad decisioningexamina estas publicidades en el siguiente orden y devuelve el primer anuncio con un tipo de medio válido:

1. Si el reempaquetado está activado, la primera incidencia de una publicidad con un tipo de medio no válido se trata como otros tipos de medios no válidos.

   Si se produce un error en el reempaquetado, este proceso se aplica a otras incidencias de la publicidad.
1. Si TVSDK no encuentra anuncios alternativos válidos, devuelve la publicidad original con el tipo de medio no válido.
1. Si se devuelve una publicidad de reserva con un tipo MIME válido en lugar de la publicidad original, Primetime ad decisioningenvía el código de error 403 a la URL de error de VAST, si está disponible.
1. Si una publicidad de reserva es un envolvente y devuelve varias publicidades, solo se devuelven las publicidades con el tipo de medio correcto.

>[!IMPORTANT]
>
>Este comportamiento siempre está habilitado para anuncios en contenedores VAST. Para las publicidades VAST en línea en un VMAP, el comportamiento está deshabilitado de forma predeterminada, pero la aplicación puede habilitarlo.

