---
description: Configure un solo lugar para gestionar errores.
title: Configuración de la gestión de errores
exl-id: 2d0e0d08-d932-4b6e-8f95-494a2e666827
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Configuración de la gestión de errores{#set-up-error-handling}

Configure un solo lugar para gestionar errores.

1. Implementación de una función de llamada de retorno para `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK pasa información de evento, como un `MediaPlayerStatusChangeEvent` objeto.
1. En la llamada de retorno, cuando el estado devuelto es `MediaPlayerState.ERROR`, proporcione lógica para gestionar todos los errores.
1. Una vez gestionado el error, restablezca el `MediaPlayer` o cargar un nuevo recurso de medios.

   Si la variable `MediaPlayer` el objeto está en estado de error, permanecerá en ese estado hasta que lo restablezca con el `MediaPlayer.reset` método.

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Por ejemplo:

```java
mediaPlayer.addEventListener( 
  MediaPlayerEvent.STATUS_CHANGED, new StatusChangedEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            // handle TVSDK error here 
        } 
    } 
});
```
