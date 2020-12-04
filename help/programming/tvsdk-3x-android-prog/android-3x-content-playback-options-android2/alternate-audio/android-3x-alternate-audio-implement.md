---
description: El audio alternativo utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-description: El audio alternativo utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-title: Acceso a pistas de audio alternativas
title: Acceso a pistas de audio alternativas
uuid: 09aa00e9-0cbf-4f5b-9652-ce514f6e2f38
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Acceso a pistas de audio alternativas{#access-alternate-audio-tracks}

El audio alternativo utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.

1. Espere a que `MediaPlayer` esté al menos en el estado `MediaPlayerStatus.PREPARED`.
1. Escuche el evento `MediaPlayerEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.PREPARED`.

   Este paso significa que la lista inicial de las pistas de audio está disponible.

1. Obtenga las pistas de audio disponibles de la instancia `MediaPlayerItem`.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la instancia `MediaPlayerItem`.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
