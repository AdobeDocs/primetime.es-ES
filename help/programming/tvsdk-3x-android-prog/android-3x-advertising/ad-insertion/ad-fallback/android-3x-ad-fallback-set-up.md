---
description: Puede habilitar la reserva cuando un anuncio en línea VMAP contenga un tipo de medio no válido.
title: Definir el comportamiento de las publicidades de reserva para las publicidades en línea VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Defina el comportamiento de los anuncios en línea de VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Puede habilitar la reserva cuando un anuncio en línea VMAP contenga un tipo de medio no válido.

1. Configure `setFallbackOnInvalidCreativeEnabled` en `true` para que VMAP vuelva a aparecer cuando el tipo de medio de un anuncio lineal/en línea no sea válido para HLS.

   El valor predeterminado es `false`. Si un anuncio lineal falla porque tiene un tipo de medio no válido o porque no se puede volver a empaquetar, este indicador permite que la toma de decisiones de anuncio de Primetime siga el mismo comportamiento de reserva que si el anuncio fuera un envoltorio VAST vacío.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
