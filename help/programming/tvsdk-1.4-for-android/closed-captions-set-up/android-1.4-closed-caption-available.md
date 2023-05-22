---
description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visualizador tiene dificultades auditivas.
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
exl-id: 75970604-c318-4621-bad3-caab292c8a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Seleccionar una pista de rótulo actual entre las pistas disponibles{#select-a-current-caption-track-from-among-available-tracks}

Puede seleccionar una pista de una lista de pistas de subtítulos cerrados disponibles actualmente. Esta se convierte en la pista actual, que se muestra cuando la visibilidad está activada. Es posible que algunas pistas no estén disponibles inicialmente, por lo que debe escuchar el evento que indica que hay más pistas disponibles.

>[!TIP]
>
>Los subtítulos opcionales siempre están activados. Se considera que están presentes todas las pistas predeterminadas de subtítulos. Las pistas predeterminadas (como CC1-CC4, CS1-CS6) se enumeran en `ClosedCaptionsTrack.DefaultCCTypes`. Cuando comienza la reproducción, TVSDK busca actividad en cualquiera de estos canales. Si encuentra actividad, establece el `isActive` método para esa pista y envía el `MediaPlayer.PlaybackEventListener.onUpdated` evento.

1. Espere a que el reproductor de contenidos esté al menos en estado PREPARADO.
1. Escuche estos eventos:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: la lista inicial de pistas de subtítulos está disponible

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

1. Implemente un detector para el evento que indique que hay más pistas disponibles. Cuando TVSDK envíe el evento, recupere la lista actual de pistas disponibles.

   Recupere la lista cada vez que se produce el evento para asegurarse de que siempre tiene la lista más actual.
