---
description: En algunos casos, es necesario saber si el contenido multimedia está activo o es VOD.
title: Identificar si el contenido está activo o es VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identificar si el contenido está activo o es VOD{#identify-whether-the-content-is-live-or-vod}

En algunos casos, es necesario saber si el contenido multimedia está activo o es VOD.

1. Asegúrese de que el reproductor esté en al menos el estado PREPARADO.
1. Determine si la variable `MediaPlayerItem` el contenido está activo (true) o VOD (false).

   ```java
   boolean isLive();
   ```
