---
description: Para poder utilizar la mayoría de los métodos de reproductor de TVSDK del explorador, el reproductor debe estar en un estado válido.
title: Esperar a un estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
