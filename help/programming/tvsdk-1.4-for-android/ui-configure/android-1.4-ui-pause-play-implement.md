---
description: Puede añadir el comportamiento de TVSDK a los botones de pausa y reproducción.
title: Reproducir y pausar un vídeo
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede añadir el comportamiento de TVSDK a los botones de pausa y reproducción.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que el reproductor esté en el estado PREPARADO.
   1. Para iniciar la reproducción, invoque el método de reproducción TVSDK:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Para pausar la reproducción, llame al método pause de TVSDK:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Utilice el `MediaPlayer.PlaybackEventListener.onStateChanged` llamada de retorno para comprobar si hay errores o realizar otras acciones adecuadas.

   TVSDK llama a esta llamada de retorno cuando se llama al método de pausa o reproducción. TVSDK pasa información sobre el cambio de estado en la llamada de retorno, incluido el nuevo estado, como PAUSED o PLAYING.
