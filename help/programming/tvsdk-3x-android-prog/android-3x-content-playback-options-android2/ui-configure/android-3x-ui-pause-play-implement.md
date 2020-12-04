---
description: Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.
seo-description: Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.
seo-title: Reproducción y pausa de un vídeo
title: Reproducción y pausa de un vídeo
uuid: 3778a1fb-929c-4579-a14c-561179473dea
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Reproducir y pausar un vídeo {#play-and-pause-a-video}

Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.

1. Para crear un botón de pausa o reproducción:
   1. Espere a que el reproductor esté al menos en el estado preparado.
   1. Para reproducir inicio, llame al método `play`:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar la reproducción, llame al método `pause()`:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilice la llamada de retorno de evento de estado modificado para comprobar si hay errores o para realizar otras acciones adecuadas.

   TVSDK llama a esta llamada de retorno para `pause()` o `play()` y pasa información sobre el cambio de estado, incluido el nuevo estado, como pausado o en reproducción.