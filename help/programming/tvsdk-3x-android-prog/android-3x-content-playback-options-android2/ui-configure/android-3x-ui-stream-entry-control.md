---
description: De forma predeterminada, al iniciar la reproducción, VOD media inicio en 0 y inicios de medios en directo en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
seo-description: De forma predeterminada, al iniciar la reproducción, VOD media inicio en 0 y inicios de medios en directo en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
seo-title: Escriba una secuencia a una hora específica
title: Escriba una secuencia a una hora específica
uuid: b315a967-77ad-4352-8a32-f228704d4b20
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# Escriba un flujo a una hora específica {#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, VOD media inicio en 0 y inicios de medios en directo en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pase una posición a `MediaPlayer.prepareToPlay`.

   TVSDK considera que la posición dada es el punto de partida del recurso y no se requiere ninguna operación de búsqueda. Si la posición no se encuentra dentro del rango buscable, TVSDK utiliza la posición predeterminada. Para obtener más información, consulte [Carga de un recurso de medios en el reproductor de medios](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

   Por ejemplo:

   ```java
   long desiredPostion = // TODO : choose a value; 
   @Override 
   public void onStatusChanged(MediaPlayerStatusChangedEvent statusChangedEvent) {   
       switch (statusChangedEvent.getStatus()) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
           case PREPARING: 
               showBufferingSpinner(); 
               break; 
       } 
   }
   ```
