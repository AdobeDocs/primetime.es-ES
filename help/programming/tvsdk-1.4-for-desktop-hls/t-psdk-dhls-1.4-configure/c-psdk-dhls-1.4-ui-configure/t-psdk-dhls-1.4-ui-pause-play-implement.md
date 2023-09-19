---
description: Puede añadir el comportamiento de TVSDK a los botones de pausa y reproducción.
title: Reproducir y pausar un vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede añadir el comportamiento de TVSDK a los botones de pausa y reproducción.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que su reproductor esté en al menos el estado PREPARADO.
   1. Para iniciar la reproducción, invoque el método de reproducción TVSDK:

      ```
      function play():void;
      ```

   1. Para pausar la reproducción, llame al método pause de TVSDK:

      ```
      function pause():void;
      ```

1. Utilice la llamada de retorno para `MediaPlayerStatusChangeEvent.STATUS_CHANGED` para comprobar si hay errores o realizar otras acciones apropiadas.

   TVSDK llama a esta llamada de retorno cuando se llama al método de pausa o reproducción. TVSDK pasa información sobre el cambio de estado en la llamada de retorno, incluido el nuevo estado, como PAUSADO o EN REPRODUCCIÓN.
