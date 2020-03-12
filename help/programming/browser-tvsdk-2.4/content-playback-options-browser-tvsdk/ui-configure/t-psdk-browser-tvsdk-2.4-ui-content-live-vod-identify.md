---
description: Es posible que deba saber si el contenido multimedia está activo o VOD.
seo-description: Es posible que deba saber si el contenido multimedia está activo o VOD.
seo-title: Identifique si el contenido está activo o VOD
title: Identifique si el contenido está activo o VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Identifique si el contenido está activo o VOD{#identify-whether-the-content-is-live-or-vod}

Es posible que deba saber si el contenido multimedia está activo o VOD.

1. Espere a que el TVSDK del explorador active un `AdobePSDK.PSDKEventType.STATUS_CHANGED` evento con un `event.status` valor de `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Este paso garantiza que el recurso de medios se haya cargado correctamente.

   >[!IMPORTANT]
   >
   >Si el SDK del explorador no está en al menos el `PREPARED` estado, al intentar llamar a los siguientes métodos se genera un `IllegalStateException`.

1. Lea `live` desde la `MediaPlayerItem` interfaz:

   ```js
   player.currentItem.live
   ```

