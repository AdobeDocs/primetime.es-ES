---
description: Puede habilitar la reserva cuando una publicidad en línea VMAP contenga un tipo de medio no válido.
seo-description: Puede habilitar la reserva cuando una publicidad en línea VMAP contenga un tipo de medio no válido.
seo-title: Definir el comportamiento de las publicidades de reserva para las publicidades en línea de VMAP
title: Definir el comportamiento de las publicidades de reserva para las publicidades en línea de VMAP
uuid: bc8cb0b4-5ea9-429b-ab5d-746c6f03e74b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Definir el comportamiento de las publicidades de reserva para las publicidades en línea de VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Puede habilitar la reserva cuando una publicidad en línea VMAP contenga un tipo de medio no válido.

1. Establezca `setFallbackOnInvalidCreativeEnabled` en `true` que VMAP se devuelva cuando el tipo de medio de un anuncio lineal/en línea no sea válido para HLS.

   El valor predeterminado es `false`. Si un anuncio lineal falla porque tiene un tipo de medio no válido o porque no se puede volver a empaquetar el anuncio, este indicador permite que Primetime y la decisión de la publicidad sigan el mismo comportamiento de reserva que si el anuncio fuera un contenedor VAST vacío.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
