---
description: En algunos casos, es necesario saber si el contenido multimedia está activo o es VOD.
title: Identificar si el contenido está activo o es VOD
exl-id: b93cc61b-aa72-4edd-a070-93c111dec339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
