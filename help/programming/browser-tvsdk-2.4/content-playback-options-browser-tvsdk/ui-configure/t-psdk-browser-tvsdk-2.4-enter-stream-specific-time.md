---
description: De forma predeterminada, cuando se inicia la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
title: Introducir un flujo a una hora específica
exl-id: 2fb361c1-7133-4e17-a12b-e11f6f7c5479
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
