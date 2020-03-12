---
description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-title: Acceso a pistas de audio alternativas
title: Acceso a pistas de audio alternativas
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Acceso a pistas de audio alternativas{#access-alternate-audio-tracks}

El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.

1. Espere a que el `MediaPlayer` estado esté al menos en el estado PREPARADO.
1. Escuchar estos eventos:

   * `MediaPlayerItemEvent.ITEM_CREATED`:: La lista inicial de pistas de audio está disponible.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`:: Pistas de audio cambiadas durante la reproducción

1. Obtenga las pistas de audio disponibles de la `MediaPlayerItem` instancia.
1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la `MediaPlayerItem` instancia.
