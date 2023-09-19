---
description: Configure un solo lugar para gestionar errores.
title: Configuración de la gestión de errores
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Configuración de la gestión de errores{#set-up-error-handling}

Configure un solo lugar para gestionar errores.

1. Implementación de una función de llamada de retorno para `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK pasa información de evento, como un `MediaPlayerStatusChangeEvent` objeto.
1. En la llamada de retorno, cuando el estado del parámetro de evento es `MediaPlayerStatus.ERROR`, proporcione lógica para gestionar todos los errores.
1. Una vez gestionado el error, restablezca el `MediaPlayer` o cargar un nuevo recurso de medios.

   Si la variable `MediaPlayer` el objeto está en estado ERROR, no puede salir de este estado hasta que restablezca el `MediaPlayer` objeto (a través de ) `MediaPlayer.reset` método) o cargar un nuevo recurso de medios ( `MediaPlayer.replaceCurrentItem`).

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
