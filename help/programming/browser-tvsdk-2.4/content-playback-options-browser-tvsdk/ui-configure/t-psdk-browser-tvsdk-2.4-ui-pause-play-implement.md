---
description: Puede agregar el comportamiento del TVSDK del explorador a los botones de pausa y reproducción.
title: Reproducir y pausar un vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede agregar el comportamiento del TVSDK del explorador a los botones de pausa y reproducción.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que el reproductor esté en el estado PREPARADO.
   1. Para iniciar la reproducción, invoque el método de reproducción TVSDK del explorador:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Para pausar la reproducción, invoque el método Pause de TVSDK del explorador:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Escuche el `AdobePSDK.MediaPlayerStatusChangeEvent` para comprobar si hay errores o realizar otras acciones apropiadas.

   TVSDK del explorador almacena en déclencheur este evento cuando se llama a métodos de pausa o reproducción y pasa información sobre el objeto de evento, incluido el nuevo estado, como `MediaPlayerStatus.PLAYING` o `MediaPlayerStatus.PAUSED`.
