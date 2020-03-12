---
description: El audio de enlace tardío utiliza PTMediaPlayer para reproducir un vídeo especificado en una lista de reproducción HLS M3U8 y que puede contener varios flujos de audio alternativos.
seo-description: El audio de enlace tardío utiliza PTMediaPlayer para reproducir un vídeo especificado en una lista de reproducción HLS M3U8 y que puede contener varios flujos de audio alternativos.
seo-title: Acceso a pistas de audio alternativas
title: Acceso a pistas de audio alternativas
uuid: 2915a74f-5ec3-457e-890d-5c79be39f37a
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Acceso a pistas de audio alternativas {#access-alternate-audio-tracks}

El audio de enlace tardío utiliza PTMediaPlayer para reproducir un vídeo especificado en una lista de reproducción HLS M3U8 y que puede contener varios flujos de audio alternativos.

1. Espere a que MediaPlayer tenga al menos el `PTMediaPlayerStatusReady` estado.
1. Escuchar este evento:

   notificación `PTMediaPlayerItemMediaSelectionOptionsAvailable`: La lista inicial de pistas de audio está disponible.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Obtenga las pistas de audio disponibles de la `PTMediaPlayerItem` instancia.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la `PTMediaPlayerItem` instancia.
