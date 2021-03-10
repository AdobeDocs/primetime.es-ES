---
description: La parte de notificación de la biblioteca TVSDK del explorador le permite crear un sistema de registro y depuración que puede resultar útil para fines de diagnóstico y validación.
title: Sistema de notificaciones
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Sistema de notificaciones {#notification-system}

La parte de notificación de la biblioteca TVSDK del explorador le permite crear un sistema de registro y depuración que puede resultar útil para fines de diagnóstico y validación.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

El SDK de TVSDK del explorador tiene una directiva *no t* para su API. La mayoría de los métodos devuelven un valor `PSDKErrorCode` para indicar si el método se ejecutó correctamente. Para obtener una lista completa de todos los valores `PSDKErrorCode` posibles, consulte Referencias de la API TVSDK del explorador.

Los errores asíncronos se notifican a través de los eventos específicos.

El SDK de TVSDK del explorador distribuye `MediaPlayer` eventos para proporcionar información sobre la actividad del reproductor. Debe implementar detectores de eventos para capturar y responder a estos eventos.

>[!TIP]
>
>Los eventos y la información clave se registran en la consola del explorador web.

## Escuchar notificaciones {#section_06B96633433D497E842FB7ADD5F2C7DA}

Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones. El núcleo del sistema de notificación TVSDK del explorador es la clase `Notification`, que representa una notificación independiente.

Para configurar la aplicación para que escuche notificaciones:

1. Escuche los cambios de estado de MediaPlayer usando la instancia de MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente la rellamada.

   La rellamada recibe una instancia de `AdobePSDK.MediaPlayerStatusChangeEvent` y el SDK de TVSDK del explorador pasa este objeto de evento a la rellamada que contiene el nuevo estado del reproductor.
1. La aplicación puede escuchar otros eventos que envía el SDK de TVSDK del explorador mediante la instancia `MediaPlayer`.

