---
description: Es posible que deba saber si el contenido multimedia es en directo o vídeo a petición (VOD).
seo-description: Es posible que deba saber si el contenido multimedia es en directo o vídeo a petición (VOD).
seo-title: Identifique si el contenido está activo o VOD
title: Identifique si el contenido está activo o VOD
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Identifique si el contenido está activo o VOD {#identify-whether-the-content-is-live-or-vod}

Es posible que deba saber si el contenido multimedia es en directo o vídeo a petición (VOD).

1. Asegúrese de que el reproductor está al menos en el `PREPARED` estado.
1. Determina si el `MediaPlayerItem` contenido es activo ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
