---
description: Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.
title: Esperar a un estado válido
exl-id: a225688a-e272-441d-90d2-5ee2c259ca9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Esperar a un estado válido {#wait-for-a-valid-state}

Con TVSDK puede controlar la experiencia de reproducción básica de vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia de reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.

El reproductor se mueve a través de varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el jugador no está en al menos el estado requerido, muchos métodos de jugador lanzan lanzamiento `IllegalStateException`.

El estado requerido suele ser PREPARADO.

1. Para confirmar que el estado es PREPARADO:

   Cuando el reproductor se esté inicializando, espere a que TVSDK llame a la llamada de retorno para el `MediaPlayerStatusChangeEvent.STATUS_CHANGED` evento con el estado PREPARADO.

   Para comprobar si el estado actual de `MediaPlayer` el objeto es al menos PREPARED.

   ```
   function getstatus():String;
   ```
