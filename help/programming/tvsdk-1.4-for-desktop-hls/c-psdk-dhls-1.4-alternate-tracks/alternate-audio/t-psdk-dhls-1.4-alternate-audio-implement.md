---
description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción de HLS M3U8 y que puede contener varios flujos de audio alternativos.
title: Acceso a pistas de audio alternativas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Acceso a pistas de audio alternativas{#access-alternate-audio-tracks}

El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción de HLS M3U8 y que puede contener varios flujos de audio alternativos.

1. Espere a que `MediaPlayer` para que esté al menos en estado PREPARADO.
1. Escuche estos eventos:

   * `MediaPlayerItemEvent.ITEM_CREATED`: la lista inicial de pistas de audio está disponible.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Las pistas de audio cambiaron durante la reproducción

1. Obtenga las pistas de audio disponibles de la `MediaPlayerItem` ejemplo.
1. (Opcional) Presente las pistas disponibles al usuario.
1. Configure la pista de audio seleccionada en la `MediaPlayerItem` ejemplo.
