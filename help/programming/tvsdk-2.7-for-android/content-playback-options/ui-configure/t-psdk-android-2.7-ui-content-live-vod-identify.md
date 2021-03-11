---
description: Es posible que deba saber si el contenido multimedia está activo o si se trata de vídeo bajo demanda (VOD).
title: Identificar si el contenido está activo o VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Identifique si el contenido está activo o VOD {#identify-whether-the-content-is-live-or-vod}

Es posible que deba saber si el contenido multimedia está activo o si se trata de vídeo bajo demanda (VOD).

1. Asegúrese de que el reproductor está en al menos el estado `PREPARED`.
1. Determine si el contenido `MediaPlayerItem` está activo ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
