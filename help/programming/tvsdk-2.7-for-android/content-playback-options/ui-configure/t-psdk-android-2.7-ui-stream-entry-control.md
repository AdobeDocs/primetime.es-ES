---
description: De forma predeterminada, al iniciar la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.
title: Introducir un flujo a una hora específica
exl-id: 2914d837-c773-42db-b744-42793e80cb95
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Introducir un flujo a una hora específica {#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (MediaPlayer.LIVE_POINT). Puede anular el comportamiento predeterminado.

1. Pasar una posición a `MediaPlayer.prepareToPlay`.

   TVSDK considera que la posición dada es el punto de partida del recurso y no se requiere ninguna operación de búsqueda. Si la posición no está dentro del rango en el que se puede buscar, TVSDK utiliza la posición predeterminada. Para obtener más información, consulte [Carga de un recurso multimedia en el reproductor de contenidos](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

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
