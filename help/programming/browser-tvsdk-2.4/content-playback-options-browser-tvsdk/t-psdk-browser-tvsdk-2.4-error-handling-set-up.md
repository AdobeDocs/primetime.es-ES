---
description: Puede configurar un lugar en la aplicación para realizar la gestión de errores en respuesta al estado ERROR.
title: Configuración de la gestión de errores
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 3%

---


# Configurar la gestión de errores{#set-up-error-handling}

Puede configurar un lugar en la aplicación para realizar la gestión de errores en respuesta al estado ERROR.

1. Agregue un detector de eventos para `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Por ejemplo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. En el detector de eventos, cuando `event.status` es `AdobePSDK.MediaPlayerStatus.ERROR`, proporcione la lógica para gestionar todos los errores.
1. Una vez que se haya manejado el error, restablezca el objeto `MediaPlayer` o cargue un nuevo recurso de medios.

       Cuando el objeto MediaPlayer está en estado ERROR, no puede salir de este estado hasta que complete una de las siguientes tareas:
   
   * Restablezca el objeto MediaPlayer utilizando el método `MediaPlayer.reset`.
   * Cargue un nuevo recurso de medios utilizando el método `MediaPlayer.replaceCurrentResource` .

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

Por ejemplo:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 
```

