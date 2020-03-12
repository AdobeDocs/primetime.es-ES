---
description: Si StageVideo no está disponible y la aplicación intenta utilizar StageVideo, TVSDK no emite un error. La aplicación puede determinar si StageVideo está disponible escuchando StageVideoAvailabilityEvent.
seo-description: Si StageVideo no está disponible y la aplicación intenta utilizar StageVideo, TVSDK no emite un error. La aplicación puede determinar si StageVideo está disponible escuchando StageVideoAvailabilityEvent.
seo-title: Compruebe si StageVideo está disponible
title: Compruebe si StageVideo está disponible
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Compruebe si StageVideo está disponible{#check-whether-stagevideo-is-available}

Si StageVideo no está disponible y la aplicación intenta utilizar StageVideo, TVSDK no emite un error. La aplicación puede determinar si StageVideo está disponible escuchando StageVideoAvailabilityEvent.

A partir de Flash 15 y versiones posteriores, cuando el hardware no `StageVideo` esté disponible, volverá al software `StageVideo`. Para Flash 14 y versiones anteriores, puede determinar si `StageVideo` está disponible. Si no `StageVideo` está disponible, puede utilizarlo `StageVideoAvailabilityEvent` para comprender por qué no está disponible.

1. Escuche `StageVideoAvailabilityEvent` para determinar si `StageVideo` está disponible.

   Por ejemplo:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Si no `StageVideo` está disponible, consulte `flash.media.StageVideoAvailabilityReason`.
