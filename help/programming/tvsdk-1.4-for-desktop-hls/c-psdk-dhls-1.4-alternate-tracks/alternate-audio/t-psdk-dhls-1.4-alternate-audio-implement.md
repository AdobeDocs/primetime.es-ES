---
description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.
title: Acceso a pistas de audio alternativas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Acceso a pistas de audio alternativas{#access-alternate-audio-tracks}

El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo especificado en una lista de reproducción M3U8 HLS y que puede contener varios flujos de audio alternativos.

1. Espere a que `MediaPlayer` esté en al menos el estado PREPARADO.
1. Escuche estos eventos:

   * `MediaPlayerItemEvent.ITEM_CREATED`: La lista inicial de pistas de audio está disponible.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Las pistas de audio cambiaron durante la reproducción

1. Obtenga las pistas de audio disponibles de la instancia `MediaPlayerItem`.
1. (Opcional) Presente las pistas disponibles al usuario.
1. Defina la pista de audio seleccionada en la instancia `MediaPlayerItem` .
