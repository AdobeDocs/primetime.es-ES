---
description: De forma predeterminada, al iniciar la reproducción, VOD media inicio en 0 y inicios de medios en directo en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
seo-description: De forma predeterminada, al iniciar la reproducción, VOD media inicio en 0 y inicios de medios en directo en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
seo-title: Escriba una secuencia a una hora específica
title: Escriba una secuencia a una hora específica
uuid: 65a19192-b890-4d69-9cb1-582a22988d2b
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Escriba un flujo a una hora específica {#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, VOD media inicio en 0 y inicios de medios en directo en el punto activo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pase una posición a `MediaPlayer.prepareToPlay`.

   TVSDK considera que la posición dada es el punto de partida del recurso y no se requiere ninguna operación de búsqueda. Si la posición no se encuentra dentro del rango buscable, TVSDK utiliza la posición predeterminada. Para obtener más información, consulte [Carga de un recurso de medios en el reproductor de medios](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

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

