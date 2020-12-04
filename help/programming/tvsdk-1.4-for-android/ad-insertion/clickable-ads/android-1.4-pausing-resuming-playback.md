---
description: Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.
seo-description: Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.
seo-title: Pausar y reanudar la reproducción
title: Pausar y reanudar la reproducción
uuid: a8fec392-3a71-4086-abf1-23522d023680
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Pausar y reanudar la reproducción {#pause-and-resume-playback}

Cuando un usuario hace clic en una publicidad, la aplicación debe pausar la reproducción del contenido del vídeo principal.

Anule los valores `onPause` y `onResume` de la Actividad de Android.

```java
@Override 
public void onResume() { 
    super.onResume(); 
    requestAudioFocus(); 
    if (_lastKnownStatus == MediaPlayer.PlayerState.PAUSED) { 
        _mediaPlayer.play(); 
    } 
} 
... 
 
@Override 
public void onPause() { 
    super.onPause(); 
    if (_mediaPlayer != null) { 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING || 
          _mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) { 
            _savedPlayerState = _mediaPlayer.getStatus(); 
            _lastKnownTime = _mediaPlayer.getCurrentTime(); 
        } 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING) { 
            _mediaPlayer.pause(); 
            _lastKnownStatus = MediaPlayer.PlayerState.PAUSED; 
        } 
    } 
} 
 
abandonAudioFocus(); 
```

