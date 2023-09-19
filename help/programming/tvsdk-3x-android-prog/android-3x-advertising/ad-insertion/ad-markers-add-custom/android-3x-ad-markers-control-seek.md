---
description: Puede anular el comportamiento predeterminado para el modo en que TVSDK gestiona las búsquedas sobre los anuncios al utilizar marcadores de anuncio personalizados.
title: Controle el comportamiento de reproducción para buscar sobre los marcadores de publicidad personalizados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Controle el comportamiento de reproducción para buscar sobre los marcadores de publicidad personalizados {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede anular el comportamiento predeterminado para el modo en que TVSDK gestiona las búsquedas sobre los anuncios al utilizar marcadores de anuncio personalizados.

De forma predeterminada, cuando un usuario busca dentro o fuera de las secciones de publicidad que resultan de la colocación de marcadores de publicidad personalizados, TVSDK omite los anuncios. Esto puede diferir del comportamiento de reproducción actual para las pausas publicitarias estándar. Puede configurar TVSDK para que cambie la posición del cabezal de reproducción al principio del anuncio personalizado omitido más recientemente cuando el usuario busque más allá de uno o más anuncios personalizados.

1. Llamada `CustomRangeMetadata.setAdjustSeekPosition` con `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Uso `customRangeMetadata` in `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
