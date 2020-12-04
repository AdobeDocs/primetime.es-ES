---
description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
seo-title: Acceso a pistas de audio alternativas
title: Acceso a pistas de audio alternativas
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Acceso a pistas de audio alternativas{#access-alternate-audio-tracks}

El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.

1. Espere a que `MediaPlayer` esté en al menos el estado PREPARADO.
1. Escuchen estos eventos:

   * `MediaPlayerItemEvent.ITEM_CREATED`:: La lista inicial de las pistas de audio está disponible.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`:: Pistas de audio cambiadas durante la reproducción

1. Obtenga las pistas de audio disponibles de la instancia `MediaPlayerItem`.
1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la instancia `MediaPlayerItem`.
