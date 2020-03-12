---
description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-title: Seleccionar una pista de rótulo actual entre las pistas disponibles
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Seleccionar una pista de rótulo actual entre las pistas disponibles{#select-a-current-caption-track-from-among-available-tracks}

Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe prestar atención al evento que indica que hay más disponibles.

>[!TIP]
>
>Los subtítulos cerrados siempre están activados. Se considera que están presentes todas las pistas de subtítulos opcionales predeterminadas. Las pistas predeterminadas (como CC1-CC4, CS1-CS6) se enumeran en `ClosedCaptionsTrack.DefaultCCTypes`. Cuando comienza la reproducción, TVSDK busca actividad en cualquiera de estos canales. Si encuentra actividad, establece el `isActive` método para esa pista y distribuye el `MediaPlayer.PlaybackEventListener.onUpdated` evento.

1. Espere a que el reproductor de medios esté al menos en el estado PREPARADO.
1. Escuchar estos eventos:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:: La lista inicial de pistas de subtítulos opcionales está disponible

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
}}

```
1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

Retrieve the list each time that the event occurs to ensure that you always have the most current list.

