---
description: Puede añadir el comportamiento del SDK de TVSDK del explorador para pausar y reproducir botones.
title: Reproducir y pausar un vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede añadir el comportamiento del SDK de TVSDK del explorador para pausar y reproducir botones.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que el reproductor esté en al menos el estado PREPARADO.
   1. Para iniciar la reproducción, llame al método de reproducción TVSDK del explorador:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Para pausar la reproducción, llame al método TVSDK pause del explorador:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Escuche el evento `AdobePSDK.MediaPlayerStatusChangeEvent` para comprobar si hay errores o para realizar otras acciones adecuadas.

   El SDK de TVSDK del explorador déclencheur este evento cuando se llaman los métodos de pausa o reproducción y pasa información sobre el objeto de evento, incluido el nuevo estado, como `MediaPlayerStatus.PLAYING` o `MediaPlayerStatus.PAUSED`.

