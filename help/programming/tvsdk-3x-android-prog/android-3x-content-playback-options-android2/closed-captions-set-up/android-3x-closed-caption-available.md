---
description: Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Esta se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe escuchar el evento que indica que hay más pistas disponibles.
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Seleccionar una pista de rótulo actual entre las pistas disponibles {#select-a-current-caption-track-from-among-available-tracks}

Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Esta se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe escuchar el evento que indica que hay más pistas disponibles.

1. Espere a que el reproductor de contenidos esté, al menos, en el `PREPARED` estado.
1. Escuche estos eventos:

   * `MediaPlayerEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.INITIALIZED`: la lista inicial de pistas de subtítulos está disponible.

1. Obtenga una lista de todas las pistas de subtítulos cerrados disponibles actualmente.

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

1. Implemente un detector para el evento que indique que hay más pistas disponibles. Cuando TVSDK envíe el evento, recupere la lista actual de pistas disponibles.

   Recupere la lista cada vez que se produce el evento para asegurarse de que siempre tiene la lista más actual.
