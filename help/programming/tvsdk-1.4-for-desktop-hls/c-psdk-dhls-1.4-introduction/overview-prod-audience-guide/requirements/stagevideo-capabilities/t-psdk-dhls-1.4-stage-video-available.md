---
description: Si StageVideo no está disponible y la aplicación intenta utilizar StageVideo, el TVSDK no genera ningún error. La aplicación puede determinar si StageVideo está disponible escuchando StageVideoAvailabilityEvent.
title: Comprobar si StageVideo está disponible
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# Comprobar si StageVideo está disponible{#check-whether-stagevideo-is-available}

Si StageVideo no está disponible y la aplicación intenta utilizar StageVideo, el TVSDK no genera ningún error. La aplicación puede determinar si StageVideo está disponible escuchando StageVideoAvailabilityEvent.

A partir del Flash 15 y posteriores, cuando el hardware `StageVideo` no esté disponible, volverá al software `StageVideo`. Para el Flash 14 y anteriores, puede determinar si `StageVideo` está disponible. Si `StageVideo` no está disponible, puede utilizar `StageVideoAvailabilityEvent` para comprender por qué no está disponible.

1. Escuche `StageVideoAvailabilityEvent` para determinar si `StageVideo` está disponible.

   Por ejemplo:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Si `StageVideo` no está disponible, marque `flash.media.StageVideoAvailabilityReason`.
