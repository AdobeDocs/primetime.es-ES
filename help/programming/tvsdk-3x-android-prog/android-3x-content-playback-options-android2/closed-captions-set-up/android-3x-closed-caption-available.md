---
description: Puede seleccionar una pista de una lista de pistas de subtítulos opcionales disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles en un principio, por lo que debe tener en cuenta el evento que indica que hay más disponibles.
seo-description: Puede seleccionar una pista de una lista de pistas de subtítulos opcionales disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles en un principio, por lo que debe tener en cuenta el evento que indica que hay más disponibles.
seo-title: Seleccionar una pista de rótulo actual entre las pistas disponibles
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
uuid: ee2bda5e-e398-4d09-bc5c-5a6adbf5f603
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# Seleccione una pista de rótulo actual entre las pistas disponibles {#select-a-current-caption-track-from-among-available-tracks}

Puede seleccionar una pista de una lista de pistas de subtítulos opcionales disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles en un principio, por lo que debe tener en cuenta el evento que indica que hay más disponibles.

1. Espere a que el reproductor de medios esté al menos en el estado `PREPARED`.
1. Escuchen estos eventos:

   * `MediaPlayerEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.INITIALIZED`: La lista inicial de las pistas de subtítulos opcionales está disponible.

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

1. Implemente un detector para el evento que indique que hay más pistas disponibles. Cuando TVSDK distribuya el evento, recupere la lista actual de las pistas disponibles.

   Recupere la lista cada vez que se produzca el evento para asegurarse de que siempre tiene la lista más actual.