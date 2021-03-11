---
description: Para poder usar la mayoría de los métodos del reproductor TVSDK del explorador, el reproductor debe estar en un estado válido.
title: Espere un estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Espere un estado válido {#wait-for-a-valid-state}

Para poder usar la mayoría de los métodos del reproductor TVSDK del explorador, el reproductor debe estar en un estado válido.

El reproductor se mueve por varios estados. Esperar que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, muchos métodos del reproductor arrojan `IllegalStateException`.

El estado requerido suele estar PREPARADO.

1. Para confirmar que el estado está PREPARADO:

   Cuando el reproductor se está inicializando, espere a que el SDK de TVSDK del explorador distribuya el evento `AdobePSDK.MediaPlayerStatusChangeEvent` con un `event.status` de `MediaPlayerStatus.PREPARED`.

   Para comprobar si el estado actual del objeto MediaPlayer está al menos PREPARADO.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

