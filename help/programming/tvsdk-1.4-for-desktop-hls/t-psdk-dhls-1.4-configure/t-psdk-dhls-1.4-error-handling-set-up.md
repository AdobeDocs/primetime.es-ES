---
description: Configure un solo lugar para controlar los errores.
title: Configuración de la gestión de errores
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 2%

---


# Configurar la gestión de errores{#set-up-error-handling}

Configure un solo lugar para controlar los errores.

1. Implemente una función de llamada de retorno de evento para `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK pasa información de eventos, como un objeto `MediaPlayerStatusChangeEvent`.
1. En la rellamada, cuando el estado del parámetro de evento es `MediaPlayerStatus.ERROR`, proporcione lógica para gestionar todos los errores.
1. Una vez que se haya manejado el error, restablezca el objeto `MediaPlayer` o cargue un nuevo recurso de medios.

   Cuando el objeto `MediaPlayer` está en estado ERROR, no puede salir de este estado hasta que se restablezca el objeto `MediaPlayer` (mediante el método `MediaPlayer.reset`) o se cargue un nuevo recurso de medios ( `MediaPlayer.replaceCurrentItem`).

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

