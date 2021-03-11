---
description: Configure un solo lugar para controlar los errores.
title: Configuración de la gestión de errores
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 2%

---


# Configurar la gestión de errores{#set-up-error-handling}

Configure un solo lugar para controlar los errores.

1. Implemente una función de llamada de retorno de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK pasa información de eventos, como un objeto `MediaPlayerStatusChangeEvent`.
1. En la rellamada, cuando el estado devuelto es `MediaPlayerState.ERROR`, proporcione lógica para gestionar todos los errores.
1. Una vez que se haya manejado el error, restablezca el objeto `MediaPlayer` o cargue un nuevo recurso de medios.

   Cuando el objeto `MediaPlayer` está en estado de error, permanece en ese estado hasta que lo restablezca con el método `MediaPlayer.reset`.

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

