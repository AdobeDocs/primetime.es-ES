---
description: De forma predeterminada, cuando se inicia la reproducción, el contenido de VOD comienza en 0 y el contenido se inicia en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
title: Introduzca una emisión a una hora específica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# Introduzca un flujo a una hora específica{#enter-a-stream-at-a-specific-time}

De forma predeterminada, cuando se inicia la reproducción, el contenido de VOD comienza en 0 y el contenido se inicia en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pase una posición a `MediaPlayer.prepareToPlay`.
1. El SDK del explorador utiliza esta posición como punto de partida para el recurso.

   >[!NOTE]
   >
   >No se requiere ninguna operación de búsqueda.

1. Si la posición no se encuentra dentro del rango buscable, se utilizan las posiciones predeterminadas.

   Por ejemplo:

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```

