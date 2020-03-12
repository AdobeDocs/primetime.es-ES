---
description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-title: Esperar un estado válido
title: Esperar un estado válido
uuid: 918ab021-3685-424a-b84e-683da0357724
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Esperar un estado válido {#wait-for-a-valid-state}

Con TVSDK puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo a petición (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.Antes de utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.

El reproductor pasa por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no tiene al menos el estado requerido, muchos métodos de reproductor se inician `IllegalStateException`.

El estado requerido suele estar PREPARADO.

1. Para confirmar que el estado está PREPARADO:

   Cuando el reproductor se está inicializando, espere a que TVSDK llame a la rellamada del `MediaPlayerStatusChangeEvent.STATUS_CHANGED` evento con estado PREPARADO.

   Para comprobar si el estado actual del `MediaPlayer` objeto está al menos PREPARADO.

   ```
   function getstatus():String;
   ```
