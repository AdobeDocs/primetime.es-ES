---
description: Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.
title: Reproducir y pausar un vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Reproducir y pausar un vídeo{#play-and-pause-a-video}

Puede añadir el comportamiento de TVSDK para pausar y reproducir botones.

1. Cree un botón de pausa/reproducción que haga lo siguiente.
   1. Espere a que el reproductor esté en al menos el estado PREPARADO .
   1. Para iniciar la reproducción, llame al método TVSDK play :

      ```
      function play():void;
      ```

   1. Para pausar la reproducción, llame al método TVSDK pause:

      ```
      function pause():void;
      ```

1. Utilice la rellamada para el evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` para comprobar si hay errores o para realizar otras acciones adecuadas.

   TVSDK llama a esta rellamada cuando se llama al método de pausa o reproducción. TVSDK pasa información sobre el cambio de estado en la rellamada, incluido el nuevo estado, como PAUSA o REPRODUCCIÓN.
