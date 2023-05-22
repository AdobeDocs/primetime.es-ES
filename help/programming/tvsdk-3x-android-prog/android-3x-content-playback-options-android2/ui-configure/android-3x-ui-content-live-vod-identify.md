---
description: Es posible que deba saber si el contenido multimedia está en directo o es vídeo bajo demanda (VOD).
title: Identificar si el contenido está activo o es VOD
exl-id: a75332d9-a23a-423c-8d1f-81b40ca73b21
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
