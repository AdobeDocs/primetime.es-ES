---
description: De forma predeterminada, cuando se inicia la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
title: Introducir un flujo a una hora específica
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Introducir un flujo a una hora específica{#enter-a-stream-at-a-specific-time}

De forma predeterminada, cuando se inicia la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pasar una posición a `MediaPlayer.prepareToPlay`.
1. El TVSDK del explorador utiliza esta posición como punto de partida para el recurso.

   >[!NOTE]
   >
   >No se requiere ninguna operación de búsqueda.

1. Si la posición no se encuentra dentro del rango en el que se puede buscar, se utilizan las posiciones predeterminadas.

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
