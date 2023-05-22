---
description: El audio de enlace tardío utiliza PTMediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción de HLS M3U8 y que puede contener varios flujos de audio alternativos.
title: Acceso a pistas de audio alternativas
exl-id: c95e2bae-fcf3-4ae2-be11-fb3191b380f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Acceso a pistas de audio alternativas {#access-alternate-audio-tracks}

El audio de enlace tardío utiliza PTMediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción de HLS M3U8 y que puede contener varios flujos de audio alternativos.

1. Espere a que MediaPlayer esté en, al menos, el `PTMediaPlayerStatusReady` estado.
1. Escuche este evento:

   notificación `PTMediaPlayerItemMediaSelectionOptionsAvailable`: la lista inicial de pistas de audio está disponible.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Obtenga las pistas de audio disponibles de la `PTMediaPlayerItem` ejemplo.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la `PTMediaPlayerItem` ejemplo.
