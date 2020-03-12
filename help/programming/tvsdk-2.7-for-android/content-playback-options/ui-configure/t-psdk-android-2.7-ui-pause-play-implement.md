---
description: Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.
seo-description: Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.
seo-title: Reproducción y pausa de un vídeo
title: Reproducción y pausa de un vídeo
uuid: 66fefead-7f1d-46ed-a23e-381f25697978
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Reproducción y pausa de un vídeo {#play-and-pause-a-video}

Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.

1. Para crear un botón de pausa o reproducción:
   1. Espere a que el reproductor esté al menos en el estado preparado.
   1. Para iniciar la reproducción, llame al `play` método:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar la reproducción, llame al `pause()` método:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilice la llamada de retorno de evento de cambio de estado para comprobar si hay errores o para realizar otras acciones apropiadas.

   TVSDK llama a esta llamada de retorno para `pause()` o `play()` pasa información sobre el cambio de estado, incluido el nuevo estado, como pausado o reproducido.

