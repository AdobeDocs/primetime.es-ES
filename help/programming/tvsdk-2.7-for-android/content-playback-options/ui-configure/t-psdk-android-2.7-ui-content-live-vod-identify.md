---
description: Es posible que deba saber si el contenido multimedia está en directo o es vídeo bajo demanda (VOD).
title: Identificar si el contenido está activo o es VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# Identificar si el contenido está activo o es VOD {#identify-whether-the-content-is-live-or-vod}

Es posible que deba saber si el contenido multimedia está en directo o es vídeo bajo demanda (VOD).

1. Asegúrese de que el reproductor esté en, al menos, la `PREPARED` estado.
1. Determine si la variable `MediaPlayerItem` el contenido está activo ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
