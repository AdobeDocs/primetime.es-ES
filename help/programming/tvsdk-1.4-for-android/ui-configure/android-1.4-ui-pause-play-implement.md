---
description: Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.
seo-description: Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.
seo-title: Reproducción y pausa de un vídeo
title: Reproducción y pausa de un vídeo
uuid: 24b26364-5cb8-4a95-9574-cc52ddfa876b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que el reproductor esté en al menos el estado PREPARADO.
   1. Para reproducir en inicio, llame al método de reproducción TVSDK:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Para pausar la reproducción, llame al método de pausa TVSDK:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Utilice la llamada de retorno `MediaPlayer.PlaybackEventListener.onStateChanged` para comprobar si hay errores o para realizar otras acciones apropiadas.

   TVSDK llama a esta llamada de retorno cuando se llama al método de pausa o reproducción. TVSDK pasa información sobre el cambio de estado en la llamada de retorno, incluido el nuevo estado, como PAUSED o PLAYING.

