---
description: El audio alternativo utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-description: El audio alternativo utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-title: Acceso a pistas de audio alternativas
title: Acceso a pistas de audio alternativas
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Acceso a pistas de audio alternativas {#access-alternate-audio-tracks}

El audio alternativo utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.

1. Espere a que el `MediaPlayer` estado esté al menos en el `MediaPlayerStatus.PREPARED` estado.
1. Escuche el `MediaPlayerEvent.STATUS_CHANGED` evento con estado `MediaPlayerStatus.PREPARED`.

   Este paso significa que la lista inicial de pistas de audio está disponible.

1. Obtenga las pistas de audio disponibles de la `MediaPlayerItem` instancia.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la `MediaPlayerItem` instancia.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

