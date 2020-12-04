---
description: Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.
seo-description: Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.
seo-title: Reproducción y pausa de un vídeo
title: Reproducción y pausa de un vídeo
uuid: 04b3b23f-5ef1-4cc4-a22f-f6ffa9cefce5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que el reproductor esté al menos en el estado PREPARADO.
   1. Para reproducir en inicio, llame al método de reproducción TVSDK:

      ```
      function play():void;
      ```

   1. Para pausar la reproducción, llame al método de pausa TVSDK:

      ```
      function pause():void;
      ```

1. Utilice la rellamada del evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` para comprobar si hay errores o para realizar otras acciones apropiadas.

   TVSDK llama a esta llamada de retorno cuando se llama al método de pausa o reproducción. TVSDK pasa información sobre el cambio de estado en la llamada de retorno, incluido el nuevo estado, como PAUSED o PLAYING.
