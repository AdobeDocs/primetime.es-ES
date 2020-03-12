---
description: Configure un solo lugar para gestionar los errores.
seo-description: Configure un solo lugar para gestionar los errores.
seo-title: Configurar la gestión de errores
title: Configurar la gestión de errores
uuid: a3182fce-85ac-4dad-bdb3-f9bfbdb2c62d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Configurar la gestión de errores{#set-up-error-handling}

Configure un solo lugar para gestionar los errores.

1. Implementar una función de llamada de retorno de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK pasa información de eventos, como un `MediaPlayerStatusChangeEvent` objeto.
1. En la llamada de retorno, cuando el estado devuelto sea `MediaPlayerState.ERROR`, proporcione lógica para gestionar todos los errores.
1. Después de gestionar el error, restablezca el `MediaPlayer` objeto o cargue un nuevo recurso de medios.

   Cuando el `MediaPlayer` objeto está en estado de error, permanece en ese estado hasta que se restablece con el `MediaPlayer.reset` método .

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

