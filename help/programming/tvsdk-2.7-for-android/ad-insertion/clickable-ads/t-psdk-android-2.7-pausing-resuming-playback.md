---
description: Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.
seo-description: Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.
seo-title: Pausar y reanudar la reproducción
title: Pausar y reanudar la reproducción
uuid: 229e2499-e30e-458c-bd6d-d035588c21cf
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Pausar y reanudar la reproducción {#pause-and-resume-playback}

Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.

1. Anule la actividad `onPause` y `onResume` de Android.

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

