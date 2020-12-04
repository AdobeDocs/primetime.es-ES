---
description: Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.
seo-description: Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.
seo-title: Pausar y reanudar la reproducción
title: Pausar y reanudar la reproducción
uuid: 87ba9f05-912d-4b85-8add-feb26a796a3a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Pausar y reanudar la reproducción {#pause-and-resume-playback}

Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.

1. Anule las Actividades `onPause` y `onResume` de Android.

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

