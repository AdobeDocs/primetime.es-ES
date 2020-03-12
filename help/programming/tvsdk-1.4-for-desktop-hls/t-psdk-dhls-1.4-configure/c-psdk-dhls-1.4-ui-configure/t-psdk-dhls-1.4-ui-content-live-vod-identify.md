---
description: En algunos casos, debe saber si el contenido multimedia está activo o VOD.
seo-description: En algunos casos, debe saber si el contenido multimedia está activo o VOD.
seo-title: Identifique si el contenido está activo o VOD
title: Identifique si el contenido está activo o VOD
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Identifique si el contenido está activo o VOD{#identify-whether-the-content-is-live-or-vod}

En algunos casos, debe saber si el contenido multimedia está activo o VOD.

1. Asegúrese de que el reproductor está en al menos el estado INICIALIZADO.
1. Determina si el contenido `MediaPlayerItem` es activo (true) o VOD (false).

   ```
   function get isLive():Boolean;
   ```

