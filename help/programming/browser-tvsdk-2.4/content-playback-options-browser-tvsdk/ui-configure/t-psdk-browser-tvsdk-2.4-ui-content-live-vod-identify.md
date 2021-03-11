---
description: Es posible que deba saber si el contenido multimedia está activo o VOD.
title: Identificar si el contenido está activo o VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# Identifique si el contenido está activo o VOD{#identify-whether-the-content-is-live-or-vod}

Es posible que deba saber si el contenido multimedia está activo o VOD.

1. Espere a que el TVSDK del explorador almacene en déclencheur un evento `AdobePSDK.PSDKEventType.STATUS_CHANGED` con un `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Este paso garantiza que el recurso de medios se haya cargado correctamente.

   >[!IMPORTANT]
   >
   >Si el SDK del explorador no está en al menos el estado `PREPARED`, al intentar llamar a los siguientes métodos se genera un `IllegalStateException`.

1. Lea `live` desde la interfaz `MediaPlayerItem`:

   ```js
   player.currentItem.live
   ```

