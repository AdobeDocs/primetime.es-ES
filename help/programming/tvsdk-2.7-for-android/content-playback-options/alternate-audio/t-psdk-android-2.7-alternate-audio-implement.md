---
description: El audio alternativo utiliza MediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción HLS M3U8 y que puede contener varios flujos de audio alternativos.
title: Acceso a pistas de audio alternativas
exl-id: e5f5b943-4886-4884-80d2-225b5c7e3aed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Acceso a pistas de audio alternativas {#access-alternate-audio-tracks}

El audio alternativo utiliza MediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción HLS M3U8 y que puede contener varios flujos de audio alternativos.

1. Espere a que `MediaPlayer` para estar en al menos el `MediaPlayerStatus.PREPARED` estado.
1. Escuche el `MediaPlayerEvent.STATUS_CHANGED` evento con estado `MediaPlayerStatus.PREPARED`.

   Este paso significa que la lista inicial de pistas de audio está disponible.

1. Obtenga las pistas de audio disponibles de la `MediaPlayerItem` ejemplo.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la `MediaPlayerItem` ejemplo.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
