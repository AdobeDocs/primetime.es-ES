---
description: Puede agregar el comportamiento de TVSDK del explorador para pausar y reproducir los botones.
seo-description: Puede agregar el comportamiento de TVSDK del explorador para pausar y reproducir los botones.
seo-title: Reproducción y pausa de un vídeo
title: Reproducción y pausa de un vídeo
uuid: 4053ea9e-6b74-41e9-ad04-087ad13e3698
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede agregar el comportamiento de TVSDK del explorador para pausar y reproducir los botones.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que el reproductor esté en al menos el estado PREPARADO.
   1. Para reproducir en inicio, llame al método de reproducción TVSDK del explorador:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Para pausar la reproducción, llame al método de pausa TVSDK del explorador:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Escuche el evento `AdobePSDK.MediaPlayerStatusChangeEvent` para comprobar si hay errores o para realizar otras acciones apropiadas.

   El SDK TVSDK del explorador activa este evento cuando se llaman los métodos de pausa o reproducción y pasa información sobre el objeto de evento, incluido el nuevo estado, como `MediaPlayerStatus.PLAYING` o `MediaPlayerStatus.PAUSED`.

