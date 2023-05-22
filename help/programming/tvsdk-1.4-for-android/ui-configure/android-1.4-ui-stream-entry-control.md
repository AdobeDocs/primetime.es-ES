---
description: De forma predeterminada, al iniciar la reproducción, los medios de VOD comienzan en 0 (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
title: Introducir un flujo a una hora específica
exl-id: a16b6281-37d5-491c-a2d0-2090894c8a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Introducir un flujo a una hora específica {#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, los medios de VOD comienzan en 0 (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pasar una posición a `MediaPlayer.prepareToPlay`.

   TVSDK considera que la posición dada es el punto de partida del recurso. No se requiere ninguna operación de búsqueda. Si la posición no está dentro del rango en el que se puede buscar, TVSDK utiliza la posición predeterminada.

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
