---
description: Puede añadir botones de pausa y reproducción para pausar o reproducir el vídeo.
title: Reproducir y pausar un vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Reproducir y pausar un vídeo {#play-and-pause-a-video}

Puede añadir botones de pausa y reproducción para pausar o reproducir el vídeo.

1. Para crear un botón de pausa o reproducción:
   1. Espere a que el reproductor esté en el estado preparado como mínimo.
   1. Para iniciar la reproducción, invoque el `play` método:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar la reproducción, invoque el método `pause()` método:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilice la llamada de retorno de evento de estado cambiado para comprobar si hay errores o realizar otras acciones adecuadas.

   TVSDK llama a esta llamada de retorno para `pause()` o `play()` y pasa información sobre el cambio de estado, incluido el nuevo estado, como en pausa o en reproducción.
