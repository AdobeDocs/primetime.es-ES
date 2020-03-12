---
description: Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe prestar atención al evento que indica que hay más disponibles.
seo-description: Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe prestar atención al evento que indica que hay más disponibles.
seo-title: Seleccionar una pista de rótulo actual entre las pistas disponibles
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
uuid: d582779a-2789-4e2a-85f6-1a0b9b847382
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Seleccionar una pista de rótulo actual entre las pistas disponibles {#select-a-current-caption-track-from-among-available-tracks}

Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe prestar atención al evento que indica que hay más disponibles.

1. Espere a que el reproductor de medios tenga al menos el `PREPARED` estado.
1. Escuchar estos eventos:

   * `MediaPlayerEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.INITIALIZED`: La lista inicial de pistas de subtítulos opcionales está disponible.

1. Obtenga una lista de todas las pistas de subtítulos opcionales disponibles actualmente.

   Por ejemplo:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Seleccione una pista disponible para que sea la pista actual.

   Por ejemplo:

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
       <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implemente un detector para el evento que indique que hay más pistas disponibles. Cuando TVSDK distribuya el evento, recupere la lista actual de pistas disponibles.

   Recupere la lista cada vez que se produzca el evento para asegurarse de que siempre tiene la lista más reciente.