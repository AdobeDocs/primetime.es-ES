---
description: Los subtítulos muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 1%

---


# Seleccionar una pista de rótulo actual entre las pistas disponibles{#select-a-current-caption-track-from-among-available-tracks}

Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe prestar atención al evento que indique que hay más disponibles.

>[!TIP]
>
>Los subtítulos están siempre activados. Se considera que están presentes todas las pistas de subtítulos opcionales predeterminadas. Las pistas predeterminadas (como CC1-CC4, CS1-CS6) se enumeran en `ClosedCaptionsTrack.DefaultCCTypes`. Cuando comienza la reproducción, TVSDK busca actividad en cualquiera de estos canales. Si encuentra actividad, establece el método `isActive` para ese seguimiento y envía el evento `MediaPlayer.PlaybackEventListener.onUpdated`.

1. Espere a que el reproductor de medios esté en al menos el estado PREPARADO.
1. Escuche estos eventos:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: La lista inicial de pistas de subtítulos cerrados está disponible

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implemente un oyente para el evento que indique que hay más pistas disponibles. Cuando TVSDK envíe el evento, recupere la lista actual de pistas disponibles.

   Recupere la lista cada vez que se produzca el evento para asegurarse de que siempre tiene la lista más actual.
