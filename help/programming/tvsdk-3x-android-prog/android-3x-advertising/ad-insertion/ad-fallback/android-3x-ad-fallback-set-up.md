---
description: Puede activar la reserva cuando un anuncio en línea de VMAP contenga un tipo de medio no válido.
title: Definir comportamiento de anuncios de reserva para anuncios en línea VMAP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Definir comportamiento de anuncios de reserva para anuncios en línea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Puede activar la reserva cuando un anuncio en línea de VMAP contenga un tipo de medio no válido.

1. Establecer `setFallbackOnInvalidCreativeEnabled` hasta `true` para que VMAP retroceda cuando el tipo de medio de un anuncio lineal/en línea no sea válido para HLS.

   El valor predeterminado es `false`. Si un anuncio lineal falla porque tiene un tipo de medio no válido o porque no se puede volver a empaquetar, este indicador permite que Primetime y Decisioning sigan el mismo comportamiento de reserva que si el anuncio fuera un contenedor VAST vacío.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
