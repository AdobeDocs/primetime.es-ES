---
description: Cuando Primetime ad decisioningencuentra un anuncio VAST (creativo) vacío o con un tipo de medio no válido para HLS, evalúa los anuncios de reserva para determinar qué se debe devolver.
title: Comportamiento de reserva de anuncio para VAST y VMAP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Comportamiento de reserva de anuncio para VAST y VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Cuando Primetime ad decisioningencuentra un anuncio VAST (creativo) vacío o con un tipo de medio no válido para HLS, evalúa los anuncios de reserva para determinar qué se debe devolver.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

En TVSDK, el único tipo de medio válido es `application/x-mpegURL` (M3U8).

Cuando hay anuncios de reserva independientes, el complemento Primetime ad decisioningexamina estos anuncios en el siguiente orden y devuelve el primer anuncio con un tipo de medio válido:

1. Si el reempaquetado está habilitado, la primera aparición de un anuncio con un tipo de medio no válido se trata como otros tipos de medio no válidos.

   Si falla el reempaquetado, este proceso se aplica a ocurrencias adicionales del anuncio.
1. Si TVSDK no encuentra anuncios de reserva válidos, devuelve el anuncio original con el tipo de medio no válido.
1. Si se devuelve un anuncio de reserva con un tipo MIME válido en lugar del anuncio original, Primetime ad decisioning envía el código de error 403 a la URL de error VAST, si está disponible.
1. Si un anuncio de reserva es un contenedor y devuelve varios anuncios, solo se devuelven los anuncios con el tipo de medio correcto.

>[!IMPORTANT]
>
>Este comportamiento siempre está habilitado para los anuncios en contenedores VAST. Para los anuncios VAST en línea en un VMAP, el comportamiento está deshabilitado de forma predeterminada, pero la aplicación puede habilitarlo.
