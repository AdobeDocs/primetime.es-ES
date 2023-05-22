---
description: En algunos casos, es necesario saber si el contenido multimedia está activo o es VOD.
title: Identificar si el contenido está activo o es VOD
exl-id: 180eb515-5bc1-4b32-babf-bcc640ebfa72
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identificar si el contenido está activo o es VOD{#identify-whether-the-content-is-live-or-vod}

En algunos casos, es necesario saber si el contenido multimedia está activo o es VOD.

1. Asegúrese de que el reproductor tenga al menos el estado INICIALIZADO.
1. Determine si la variable `MediaPlayerItem` el contenido está activo (true) o VOD (false).

   ```
   function get isLive():Boolean;
   ```
