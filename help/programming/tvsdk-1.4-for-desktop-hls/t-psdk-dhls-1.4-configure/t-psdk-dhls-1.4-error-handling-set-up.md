---
description: Configure un solo lugar para gestionar los errores.
seo-description: Configure un solo lugar para gestionar los errores.
seo-title: Configurar la gestión de errores
title: Configurar la gestión de errores
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 1%

---


# Configurar la gestión de errores{#set-up-error-handling}

Configure un solo lugar para gestionar los errores.

1. Implementar una función de llamada de retorno de evento para `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK pasa información de evento, como un objeto `MediaPlayerStatusChangeEvent`.
1. En la llamada de retorno, cuando el estado del parámetro de evento es `MediaPlayerStatus.ERROR`, proporcione lógica para controlar todos los errores.
1. Después de gestionar el error, restablezca el objeto `MediaPlayer` o cargue un nuevo recurso de medios.

   Cuando el objeto `MediaPlayer` está en el estado ERROR, no puede salir de este estado hasta que se restablezca el objeto `MediaPlayer` (mediante el método `MediaPlayer.reset`) o se cargue un nuevo recurso de medios ( `MediaPlayer.replaceCurrentItem`).

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

