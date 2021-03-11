---
description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
title: Acceso a pistas de audio alternativas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Acceso a pistas de audio alternativas{#access-alternate-audio-tracks}

El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.

1. Espere a que MediaPlayer esté en al menos el estado PREPARADO.
1. Escuche este evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: La lista inicial de pistas de audio está disponible.

1. Obtenga las pistas de audio disponibles de la instancia `MediaPlayerItem`.

   `mediaPlayerItem.getAudioTracks()` 1. (Opcional) Presente las pistas disponibles al usuario.
1. Defina la pista de audio seleccionada en la instancia `MediaPlayerItem` .

   `mediaPlayerItem.selectAudioTrack(audioTrack)`