---
description: Puede omitir el comportamiento predeterminado en cuanto al modo en que TVSDK gestiona las búsquedas sobre las publicidades al utilizar marcadores de publicidad personalizados.
seo-description: Puede omitir el comportamiento predeterminado en cuanto al modo en que TVSDK gestiona las búsquedas sobre las publicidades al utilizar marcadores de publicidad personalizados.
seo-title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
uuid: 248e914e-81b7-4aa5-a4d5-06ca2666e006
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Controlar el comportamiento de reproducción para buscar marcadores de publicidad personalizados {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede omitir el comportamiento predeterminado en cuanto al modo en que TVSDK gestiona las búsquedas sobre las publicidades al utilizar marcadores de publicidad personalizados.

De forma predeterminada, cuando un usuario busca en secciones de publicidad anteriores o en secciones de publicidad que resultan de la colocación de marcadores de publicidad personalizados, TVSDK omite las publicidades. Esto puede diferir del comportamiento de reproducción actual de los saltos de publicidad estándar. Puede definir TVSDK para que vuelva a colocar el cursor de reproducción al principio de la última publicidad personalizada omitida cuando el usuario busque más anuncios personalizados.

1. Llame a `CustomRangeMetadata.setAdjustSeekPosition` con `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Utilice `customRangeMetadata` en `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```

