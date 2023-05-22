---
description: A continuación se muestra un ejemplo de cómo un usuario puede seleccionar una pista de subtítulos.
title: Permitir al usuario cambiar la pista
exl-id: 103ca0ad-2707-4e4f-87ee-f55041e4527a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# Permitir al usuario cambiar la pista{#allow-the-user-to-change-the-track}

A continuación se muestra un ejemplo de cómo un usuario puede seleccionar una pista de subtítulos.

1. Para mostrar las pistas de subtítulos opcionales disponibles, utilice el `MediaPlayerItem.closedCaptionsTracks` propiedad.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Para definir qué pista de subtítulos está actualizada, use el `MediaPlayerItem.selectClosedCaptionsTrack` método.
1. Una vez preparado el elemento del reproductor de contenido, recupérelo del reproductor de contenido mediante el comando ` MediaPlayer.  currentItem ` método.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
