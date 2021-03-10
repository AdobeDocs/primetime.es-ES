---
description: Este es un ejemplo de cómo un usuario puede seleccionar una pista de subtítulos.
title: Permitir al usuario cambiar la pista
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---


# Permitir al usuario cambiar el seguimiento{#allow-the-user-to-change-the-track}

Este es un ejemplo de cómo un usuario puede seleccionar una pista de subtítulos.

1. Para mostrar las pistas de subtítulos cerrados disponibles, utilice la propiedad `MediaPlayerItem.closedCaptionsTracks` .

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Para definir qué pista de subtítulos es actual, utilice el método `MediaPlayerItem.selectClosedCaptionsTrack`.
1. Una vez preparado el elemento del reproductor de contenidos, recuperarlo del reproductor de contenidos mediante el método ` MediaPlayer.  currentItem `.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

