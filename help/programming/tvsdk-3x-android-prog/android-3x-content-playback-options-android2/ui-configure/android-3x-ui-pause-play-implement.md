---
description: Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.
title: Reproducir y pausar un vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Reproducir y pausar un vídeo {#play-and-pause-a-video}

Puede agregar botones de pausa y reproducción para pausar o reproducir el vídeo.

1. Para crear un botón de pausa o reproducción:
   1. Espere a que el reproductor esté en al menos el estado preparado.
   1. Para iniciar la reproducción, llame al método `play` :

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar la reproducción, llame al método `pause()` :

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilice la llamada de retorno de evento de cambio de estado para comprobar si hay errores o para realizar otras acciones adecuadas.

   TVSDK llama a esta rellamada para `pause()` o `play()` y pasa información sobre el cambio de estado, incluido el nuevo estado, como pausado o reproducido.