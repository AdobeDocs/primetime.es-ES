---
description: De forma predeterminada, al iniciar la reproducción, el contenido de VOD se inicia en 0 (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
title: Introduzca una emisión a una hora específica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# Introduzca un flujo a una hora específica {#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, el contenido de VOD se inicia en 0 (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pase una posición a `MediaPlayer.prepareToPlay`.

   TVSDK considera que la posición dada es el punto de partida del recurso. No se requiere ninguna operación de búsqueda. Si la posición no se encuentra dentro del rango en el que se puede buscar, TVSDK utiliza la posición predeterminada.

   Por ejemplo:

   ```java
   long desiredPostion = //TODO : choose a value; 
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
               case PREPARING: 
               showBufferingSpinner(); 
               break; 
           ... 
       } 
   } 
   ```

