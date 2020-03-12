---
description: Configure un solo lugar para gestionar los errores.
seo-description: Configure un solo lugar para gestionar los errores.
seo-title: Configurar la gestión de errores
title: Configurar la gestión de errores
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Configurar la gestión de errores{#set-up-error-handling}

Configure un solo lugar para gestionar los errores.

1. Implementar una función de llamada de retorno de evento para `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK pasa información de eventos, como un `MediaPlayerStatusChangeEvent` objeto.
1. En la llamada de retorno, cuando el estado del parámetro event sea `MediaPlayerStatus.ERROR`, proporcione lógica para controlar todos los errores.
1. Después de gestionar el error, restablezca el `MediaPlayer` objeto o cargue un nuevo recurso de medios.

   Cuando el `MediaPlayer` objeto está en estado ERROR, no puede salir de este estado hasta que se restablezca el `MediaPlayer` objeto (mediante el `MediaPlayer.reset` método ) o se cargue un nuevo recurso de medios ( `MediaPlayer.replaceCurrentItem`).

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Por ejemplo:

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 
```

