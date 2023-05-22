---
description: El audio de enlace tardío utiliza MediaPlayer para reproducir un vídeo que se especifica en una lista de reproducción de HLS M3U8 y que puede contener varios flujos de audio alternativos.
title: Acceso a pistas de audio alternativas
exl-id: 08158b3b-1ed2-4f86-a710-2b128bb28ed0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
