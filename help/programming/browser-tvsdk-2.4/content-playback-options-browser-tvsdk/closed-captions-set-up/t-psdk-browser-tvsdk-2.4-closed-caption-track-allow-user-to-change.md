---
description: A continuación se muestra un ejemplo de cómo un usuario puede seleccionar una pista de subtítulos opcionales.
seo-description: A continuación se muestra un ejemplo de cómo un usuario puede seleccionar una pista de subtítulos opcionales.
seo-title: Permitir al usuario cambiar el seguimiento
title: Permitir al usuario cambiar el seguimiento
uuid: bd3d4d20-9b52-4365-b656-83ec2a405a1c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Permitir al usuario cambiar el seguimiento{#allow-the-user-to-change-the-track}

A continuación se muestra un ejemplo de cómo un usuario puede seleccionar una pista de subtítulos opcionales.

1. Para mostrar las pistas de subtítulos opcionales disponibles, utilice la propiedad `MediaPlayerItem.closedCaptionsTracks`.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Para establecer qué seguimiento de subtítulos cerrados es actual, utilice el método `MediaPlayerItem.selectClosedCaptionsTrack`.
1. Una vez preparado el elemento del reproductor multimedia, recuperarlo del reproductor multimedia mediante el método ` MediaPlayer.  currentItem `.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

