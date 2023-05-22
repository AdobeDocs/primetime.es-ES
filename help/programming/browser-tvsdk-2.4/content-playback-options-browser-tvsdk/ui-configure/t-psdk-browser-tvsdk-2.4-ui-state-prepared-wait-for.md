---
description: Para poder utilizar la mayoría de los métodos de reproductor de TVSDK del explorador, el reproductor debe estar en un estado válido.
title: Esperar a un estado válido
exl-id: 14f6a5db-4f81-448b-b291-487569a7bc4e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Esperar a un estado válido {#wait-for-a-valid-state}

Para poder utilizar la mayoría de los métodos de reproductor de TVSDK del explorador, el reproductor debe estar en un estado válido.

El reproductor se desplaza por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso multimedia se haya cargado correctamente. Si el reproductor no se encuentra en el estado requerido, se activan muchos métodos de reproductor `IllegalStateException`.

El estado requerido suele ser PREPARADO.

1. Para confirmar que el estado es PREPARADO:

   Cuando se inicie el reproductor, espere a que el TVSDK del explorador envíe el `AdobePSDK.MediaPlayerStatusChangeEvent` evento con un `event.status` de `MediaPlayerStatus.PREPARED`.

   Para comprobar si el estado actual del objeto MediaPlayer es al menos PREPARED.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
