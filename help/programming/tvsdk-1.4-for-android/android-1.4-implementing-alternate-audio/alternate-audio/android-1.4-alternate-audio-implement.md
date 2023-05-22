---
description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción de HLS M3U8 y que puede contener varios flujos de audio alternativos.
title: Acceso a pistas de audio alternativas
exl-id: d357bcc9-2996-42f0-a733-482f59e938ac
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Acceso a pistas de audio alternativas{#access-alternate-audio-tracks}

El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción de HLS M3U8 y que puede contener varios flujos de audio alternativos.

1. Espere a que MediaPlayer esté al menos en el estado PREPARED.
1. Escuche este evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: la lista inicial de pistas de audio está disponible.

1. Obtenga las pistas de audio disponibles de la `MediaPlayerItem` ejemplo.

   `mediaPlayerItem.getAudioTracks()` 1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la `MediaPlayerItem` ejemplo.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
