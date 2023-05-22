---
description: Si StageVideo no está disponible y la aplicación intenta utilizar StageVideo, TVSDK no genera un error. La aplicación puede determinar si StageVideo está disponible escuchando StageVideoAvailabilityEvent.
title: Comprobar si StageVideo está disponible
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Comprobar si StageVideo está disponible{#check-whether-stagevideo-is-available}

Si StageVideo no está disponible y la aplicación intenta utilizar StageVideo, TVSDK no genera un error. La aplicación puede determinar si StageVideo está disponible escuchando StageVideoAvailabilityEvent.

Desde el Flash 15 y posterior, cuando el hardware `StageVideo` no está disponible, volverá a depender del software `StageVideo`. Para el Flash 14 y anteriores, puede determinar si `StageVideo` está disponible. If `StageVideo` no está disponible, puede utilizar `StageVideoAvailabilityEvent` para comprender por qué no está disponible.

1. Escuchar para `StageVideoAvailabilityEvent` para determinar si `StageVideo` está disponible.

   Por ejemplo:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. If `StageVideo` no está disponible, marque `flash.media.StageVideoAvailabilityReason`.
