---
description: Puede configurar un lugar en la aplicación para que realice la gestión de errores en respuesta al estado ERROR.
seo-description: Puede configurar un lugar en la aplicación para que realice la gestión de errores en respuesta al estado ERROR.
seo-title: Configurar la gestión de errores
title: Configurar la gestión de errores
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 2%

---


# Configurar la gestión de errores{#set-up-error-handling}

Puede configurar un lugar en la aplicación para que realice la gestión de errores en respuesta al estado ERROR.

1. Añada un detector de evento para `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Por ejemplo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. En el detector de evento, cuando `event.status` es `AdobePSDK.MediaPlayerStatus.ERROR`, proporcione la lógica para gestionar todos los errores.
1. Después de gestionar el error, restablezca el objeto `MediaPlayer` o cargue un nuevo recurso de medios.

       Cuando el objeto MediaPlayer está en el estado ERROR, no puede salir de este estado hasta que complete una de las siguientes tareas:
   
   * Restablezca el objeto MediaPlayer mediante el método `MediaPlayer.reset`.
   * Cargue un nuevo recurso de medios mediante el método `MediaPlayer.replaceCurrentResource`.

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

