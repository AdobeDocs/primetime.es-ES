---
description: Es posible que deba saber si el contenido multimedia está activo o es VOD.
title: Identificar si el contenido está activo o es VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# Identificar si el contenido está activo o es VOD{#identify-whether-the-content-is-live-or-vod}

Es posible que deba saber si el contenido multimedia está activo o es VOD.

1. Espere a que el TVSDK del explorador almacene en déclencheur un `AdobePSDK.PSDKEventType.STATUS_CHANGED` evento con un `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Este paso garantiza que el recurso de medios se haya cargado correctamente.

   >[!IMPORTANT]
   >
   >Si el TVSDK del explorador no está en, al menos, la variable `PREPARED` estado, al intentar llamar a los siguientes métodos se genera un `IllegalStateException`.

1. Leer `live` desde el `MediaPlayerItem` interfaz:

   ```js
   player.currentItem.live
   ```
