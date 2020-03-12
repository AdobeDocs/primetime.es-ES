---
description: Puede habilitar la reserva cuando una publicidad en línea VMAP contenga un tipo de medio no válido.
seo-description: Puede habilitar la reserva cuando una publicidad en línea VMAP contenga un tipo de medio no válido.
seo-title: Definir el comportamiento de las publicidades de reserva para las publicidades en línea de VMAP
title: Definir el comportamiento de las publicidades de reserva para las publicidades en línea de VMAP
uuid: a7b5c9a6-f546-4d3a-9d49-7e5484acff7a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Definir el comportamiento de las publicidades de reserva para las publicidades en línea de VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Puede habilitar la reserva cuando una publicidad en línea VMAP contenga un tipo de medio no válido.

1. Establezca `setFallbackOnInvalidCreativeEnabled` en `true` que VMAP se devuelva cuando el tipo de medio de un anuncio lineal/en línea no sea válido para HLS.

   El valor predeterminado es `false`. Si un anuncio lineal falla porque tiene un tipo de medio no válido o porque no se puede volver a empaquetar el anuncio, este indicador permite que Primetime y la decisión de la publicidad sigan el mismo comportamiento de reserva que si el anuncio fuera un contenedor VAST vacío.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

