---
description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-title: Seleccionar una pista de rótulo actual entre las pistas disponibles
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 53924aa8ba90555d58d15ee10fb14221c7dffaff
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---


# Seleccione una pista de rótulo actual entre las pistas disponibles{#select-a-current-caption-track-from-among-available-tracks}

Puede seleccionar una pista de una lista de pistas de subtítulos opcionales disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles en un principio, por lo que debe tener en cuenta el evento que indica que hay más disponibles.

>[!TIP]
>
>Los subtítulos cerrados siempre están activados. Se considera que están presentes todas las pistas de subtítulos opcionales predeterminadas. Las pistas predeterminadas (como CC1-CC4, CS1-CS6) se enumeran en `ClosedCaptionsTrack.DefaultCCTypes`. Cuando comienza la reproducción, TVSDK busca la actividad en cualquiera de estos canales. Si encuentra actividad, establece el método `isActive` para esa pista y distribuye el evento `MediaPlayer.PlaybackEventListener.onUpdated`.

1. Espere a que el reproductor de medios esté al menos en el estado PREPARADO.
1. Escuchen estos eventos:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:: La lista inicial de las pistas de subtítulos opcionales está disponible

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implemente un detector para el evento que indique que hay más pistas disponibles. Cuando TVSDK distribuya el evento, recupere la lista actual de las pistas disponibles.

   Recupere la lista cada vez que se produzca el evento para asegurarse de que siempre tiene la lista más actual.
