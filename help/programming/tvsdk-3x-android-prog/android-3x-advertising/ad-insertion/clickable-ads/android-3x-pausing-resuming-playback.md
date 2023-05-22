---
description: Cuando un usuario hace clic en un anuncio, la aplicación debe pausar la reproducción del contenido de vídeo principal.
title: Pausar y reanudar la reproducción
exl-id: 3c009439-e2d9-4443-bcb9-00ea18dac0c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Pausar y reanudar la reproducción {#pause-and-resume-playback}

Cuando un usuario hace clic en un anuncio, la aplicación debe pausar la reproducción del contenido de vídeo principal.

1. Anular la variable `onPause` y `onResume` de Actividad de Android.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayerStatus.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
   
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) { 
               _savedPlayerStatus = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayerStatus.PAUSED; 
           } 
       } 
   } 
   abandonAudioFocus(); 
   ```
