---
description: Puede anular el comportamiento predeterminado de cómo administra TVSDK las búsquedas en lugar de las publicidades al usar marcadores de anuncios personalizados.
title: Controlar el comportamiento de reproducción para buscar en marcadores de anuncios personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Controlar el comportamiento de reproducción para buscar en marcadores de anuncios personalizados {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede anular el comportamiento predeterminado de cómo administra TVSDK las búsquedas en lugar de las publicidades al usar marcadores de anuncios personalizados.

De forma predeterminada, cuando un usuario busca en secciones de anuncios anteriores o en secciones de anuncios anteriores resultantes de la colocación de marcadores de anuncios personalizados, TVSDK omite los anuncios. Esto puede diferir del comportamiento de reproducción actual de las pausas publicitarias estándar. Puede configurar TVSDK para que vuelva a colocar el cursor de reproducción al principio del anuncio personalizado que se haya omitido más recientemente cuando el usuario busque más anuncios personalizados.

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
