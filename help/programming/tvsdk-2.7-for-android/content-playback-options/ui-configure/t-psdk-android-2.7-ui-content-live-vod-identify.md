---
description: Es posible que deba saber si el contenido multimedia es en directo o vídeo a petición (VOD).
seo-description: Es posible que deba saber si el contenido multimedia es en directo o vídeo a petición (VOD).
seo-title: Identifique si el contenido está activo o VOD
title: Identifique si el contenido está activo o VOD
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Identifique si el contenido está activo o VOD {#identify-whether-the-content-is-live-or-vod}

Es posible que deba saber si el contenido multimedia es en directo o vídeo a petición (VOD).

1. Asegúrese de que el reproductor está al menos en el `PREPARED` estado.
1. Determina si el `MediaPlayerItem` contenido es activo ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
