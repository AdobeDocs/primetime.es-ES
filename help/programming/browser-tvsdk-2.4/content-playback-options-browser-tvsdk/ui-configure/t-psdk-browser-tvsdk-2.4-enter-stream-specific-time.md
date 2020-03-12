---
description: De forma predeterminada, cuando se inicia la reproducción, el medio VOD comienza en 0 y el medio activo se inicia en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
seo-description: De forma predeterminada, cuando se inicia la reproducción, el medio VOD comienza en 0 y el medio activo se inicia en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
seo-title: Escriba una secuencia a una hora específica
title: Escriba una secuencia a una hora específica
uuid: 5db73b50-0629-4fb1-8f12-6c88e4cd7109
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Escriba una secuencia a una hora específica{#enter-a-stream-at-a-specific-time}

De forma predeterminada, cuando se inicia la reproducción, el medio VOD comienza en 0 y el medio activo se inicia en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pasa una posición a `MediaPlayer.prepareToPlay`.
1. El SDK del explorador utiliza esta posición como punto de partida para el recurso.

   >[!NOTE]
   >
   >No se requiere ninguna operación de búsqueda.

1. Si la posición no está dentro del rango buscable, se utilizan las posiciones predeterminadas.

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

