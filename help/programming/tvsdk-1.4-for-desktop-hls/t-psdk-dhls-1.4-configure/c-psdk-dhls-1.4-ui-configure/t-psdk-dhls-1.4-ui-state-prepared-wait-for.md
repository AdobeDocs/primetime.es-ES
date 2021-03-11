---
description: Para poder usar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
title: Espere un estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Espere un estado válido {#wait-for-a-valid-state}

Con TVSDK, puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor. Antes de poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe estar en un estado válido.

El reproductor pasa por varios estados. Esperar que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, muchos métodos del reproductor arrojan `IllegalStateException`.

El estado requerido suele estar PREPARADO.

1. Para confirmar que el estado está PREPARADO:

   Cuando el reproductor se está inicializando, espere a que TVSDK llame a la rellamada para el evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado PREPARADO.

   Para comprobar si el estado actual del objeto `MediaPlayer` está al menos PREPARADO.

   ```
   function getstatus():String;
   ```
