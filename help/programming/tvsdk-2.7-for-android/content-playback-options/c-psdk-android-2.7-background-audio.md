---
title: Habilitar audio de fondo
description: Habilitar audio de fondo
copied-description: true
exl-id: db494969-ef63-46ad-9f08-a95f58c8b27b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Habilitar audio de fondo {#enable-background-audio}

Para habilitar la reproducción de audio cuando la aplicación está en segundo plano, la aplicación debe llamar a `enableAudioPlaybackInBackground` API de MediaPlayer con true como argumento cuando el reproductor está en estado PREPARED.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

La aplicación debe pausar la reproducción cuando pierde la retención del enfoque del audio durante eventos como responder al teléfono, etc. El siguiente fragmento de código muestra cómo implementar la variable `OnAudioFocusChangeListener`:

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```
