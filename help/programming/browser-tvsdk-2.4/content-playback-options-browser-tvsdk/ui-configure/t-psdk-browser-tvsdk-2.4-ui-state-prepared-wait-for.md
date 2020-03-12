---
description: Para poder utilizar la mayoría de los métodos del reproductor de TVSDK del explorador, el reproductor debe tener un estado válido.
seo-description: Para poder utilizar la mayoría de los métodos del reproductor de TVSDK del explorador, el reproductor debe tener un estado válido.
seo-title: Esperar un estado válido
title: Esperar un estado válido
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Esperar un estado válido {#wait-for-a-valid-state}

Para poder utilizar la mayoría de los métodos del reproductor de TVSDK del explorador, el reproductor debe tener un estado válido.

El jugador se mueve por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está al menos en el estado requerido, muchos métodos del reproductor `IllegalStateException`.

El estado requerido suele estar PREPARADO.

1. Para confirmar que el estado está PREPARADO:

   Cuando el reproductor se está inicializando, espere a que el TVSDK del explorador distribuya el `AdobePSDK.MediaPlayerStatusChangeEvent` evento con un `event.status` de `MediaPlayerStatus.PREPARED`.

   Para comprobar si el estado actual del objeto MediaPlayer está al menos PREPARADO.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

