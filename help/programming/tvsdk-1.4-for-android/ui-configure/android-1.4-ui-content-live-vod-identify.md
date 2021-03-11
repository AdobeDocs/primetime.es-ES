---
description: En algunos casos, debe saber si el contenido multimedia está activo o VOD.
title: Identificar si el contenido está activo o VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Identifique si el contenido está activo o VOD{#identify-whether-the-content-is-live-or-vod}

En algunos casos, debe saber si el contenido multimedia está activo o VOD.

1. Asegúrese de que el reproductor esté en al menos el estado PREPARADO.
1. Determine si el contenido `MediaPlayerItem` está activo (verdadero) o VOD (falso).

   ```java
   boolean isLive();
   ```

