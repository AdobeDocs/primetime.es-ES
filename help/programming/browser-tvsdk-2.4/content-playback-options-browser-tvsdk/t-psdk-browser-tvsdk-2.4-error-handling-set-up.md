---
description: Puede configurar un lugar en la aplicación para realizar el control de errores en respuesta al estado ERROR.
title: Configuración de la gestión de errores
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Configuración de la gestión de errores{#set-up-error-handling}

Puede configurar un lugar en la aplicación para realizar el control de errores en respuesta al estado ERROR.

1. Agregar un detector de eventos para `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Por ejemplo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. En el oyente de eventos, cuando la variable `event.status` es `AdobePSDK.MediaPlayerStatus.ERROR`, proporcione la lógica para gestionar todos los errores.
1. Una vez gestionado el error, restablezca el `MediaPlayer` o cargar un nuevo recurso de medios.

       Cuando el objeto MediaPlayer se encuentra en el estado ERROR, no puede salir de este estado hasta que complete una de las siguientes tareas:
   
   * Restablezca el objeto MediaPlayer mediante el `MediaPlayer.reset` método.
   * Cargar un nuevo recurso de medios utilizando `MediaPlayer.replaceCurrentResource` método.

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
