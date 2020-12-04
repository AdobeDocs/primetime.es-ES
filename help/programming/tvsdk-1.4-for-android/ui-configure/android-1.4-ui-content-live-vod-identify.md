---
description: En algunos casos, debe saber si el contenido multimedia está activo o VOD.
seo-description: En algunos casos, debe saber si el contenido multimedia está activo o VOD.
seo-title: Identifique si el contenido está activo o VOD
title: Identifique si el contenido está activo o VOD
uuid: cd71b8d3-259a-48f8-a6ad-02b57da146a7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Identifique si el contenido está activo o VOD{#identify-whether-the-content-is-live-or-vod}

En algunos casos, debe saber si el contenido multimedia está activo o VOD.

1. Asegúrese de que el reproductor está en al menos el estado PREPARADO.
1. Determine si el contenido `MediaPlayerItem` está activo (true) o VOD (false).

   ```java
   boolean isLive();
   ```

