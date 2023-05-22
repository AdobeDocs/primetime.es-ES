---
description: Puede activar la reserva cuando un anuncio en línea de VMAP contenga un tipo de medio no válido.
title: Definir comportamiento de anuncios de reserva para anuncios en línea VMAP
exl-id: 50de85b0-df2b-422f-893c-dfa641b4901e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
