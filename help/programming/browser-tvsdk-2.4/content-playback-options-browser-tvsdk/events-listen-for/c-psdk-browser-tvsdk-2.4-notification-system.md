---
description: La porción de notificación de la biblioteca TVSDK del explorador le permite crear un sistema de registro y depuración que puede resultar útil para fines de diagnóstico y validación.
seo-description: La porción de notificación de la biblioteca TVSDK del explorador le permite crear un sistema de registro y depuración que puede resultar útil para fines de diagnóstico y validación.
seo-title: Sistema de notificaciones
title: Sistema de notificaciones
uuid: 69c4ff1d-3167-413b-ab49-942a5ddc34d7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Sistema de notificaciones {#notification-system}

La porción de notificación de la biblioteca TVSDK del explorador le permite crear un sistema de registro y depuración que puede resultar útil para fines de diagnóstico y validación.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

El SDK del explorador tiene una directiva *sin emisión* para su API. La mayoría de los métodos devuelven un `PSDKErrorCode` valor para indicar si el método se ejecutó correctamente. Para obtener una lista completa de todos los valores posibles, consulte Referencias de API de TVSDK de explorador. `PSDKErrorCode`

Los errores asincrónicos se notifican a través de los eventos específicos.

El SDK de TVSDK del explorador distribuye `MediaPlayer` eventos para proporcionar información sobre la actividad del reproductor. Debe implementar detectores de eventos para capturar y responder a estos eventos.

>[!TIP]
>
>La información y los eventos clave se registran en la consola del navegador web.

## Escuchar notificaciones {#section_06B96633433D497E842FB7ADD5F2C7DA}

Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones. El núcleo del sistema de notificación TVSDK del explorador es la `Notification` clase, que representa una notificación independiente.

Para configurar la aplicación para que escuche las notificaciones:

1. Escuche los cambios de estado de MediaPlayer mediante la instancia de MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente la llamada de retorno.

   La llamada de retorno recibe una instancia de la llamada `AdobePSDK.MediaPlayerStatusChangeEvent`y el SDK de TVSDK del explorador pasa este objeto de evento a la llamada de retorno que contiene el nuevo estado del reproductor.
1. La aplicación puede escuchar otros eventos que el Explorador TVSDK distribuye mediante la `MediaPlayer` instancia.

