---
description: Puede omitir el comportamiento predeterminado en cuanto al modo en que TVSDK gestiona las búsquedas sobre las publicidades al utilizar marcadores de publicidad personalizados.
seo-description: Puede omitir el comportamiento predeterminado en cuanto al modo en que TVSDK gestiona las búsquedas sobre las publicidades al utilizar marcadores de publicidad personalizados.
seo-title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
uuid: ec95a22f-0143-4c80-826f-d6b40e77cf26
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede omitir el comportamiento predeterminado en cuanto al modo en que TVSDK gestiona las búsquedas sobre las publicidades al utilizar marcadores de publicidad personalizados.

De forma predeterminada, cuando un usuario busca en secciones de publicidad anteriores o en secciones de publicidad que resultan de la colocación de marcadores de publicidad personalizados, TVSDK omite las publicidades. Esto puede diferir del comportamiento de reproducción actual de los saltos de publicidad estándar. Puede definir TVSDK para que vuelva a colocar el cursor de reproducción al principio de la última publicidad personalizada omitida cuando el usuario busque más anuncios personalizados.

1. Llama `CustomRangeMetadata.setAdjustSeekPosition` con `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Utilícelo `customRangeMetadata` en `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
