---
description: La parte de notificación de la biblioteca TVSDK del explorador permite crear un sistema de registro y depuración que puede ser útil para fines de diagnóstico y validación.
title: Sistema de notificación
exl-id: 6a3a3c56-1580-4f43-ba81-220a5b0fe5c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Sistema de notificación {#notification-system}

La parte de notificación de la biblioteca TVSDK del explorador permite crear un sistema de registro y depuración que puede ser útil para fines de diagnóstico y validación.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

El TVSDK del explorador tiene un *sin lanzamiento* para su API. La mayoría de los métodos devuelven un `PSDKErrorCode` para indicar si el método se ejecutó correctamente. Para obtener una lista completa de todos los posibles `PSDKErrorCode` Consulte Referencias de la API de TVSDK del explorador.

Los errores asincrónicos se notifican a través de los eventos específicos.

Distribuciones de TVSDK del explorador `MediaPlayer` para proporcionar información sobre la actividad del reproductor. Debe implementar detectores de eventos para capturar y responder a estos eventos.

>[!TIP]
>
>Los eventos clave y la información se registran en la consola del explorador web.

## Escuchar notificaciones {#section_06B96633433D497E842FB7ADD5F2C7DA}

Puede escuchar las notificaciones y agregar sus propias notificaciones al historial de notificaciones. El núcleo del sistema de notificación de TVSDK del explorador es el `Notification` , que representa una notificación independiente.

Para configurar la aplicación para recibir notificaciones:

1. Escuche los cambios de estado de MediaPlayer mediante la instancia de MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente la llamada de retorno.

   La llamada de retorno recibe una instancia de `AdobePSDK.MediaPlayerStatusChangeEvent`y el TVSDK del explorador pasa este objeto de evento a la llamada de retorno que contiene el nuevo estado del reproductor.
1. Su aplicación puede escuchar otros eventos distribuidos por el TVSDK del explorador utilizando el `MediaPlayer` ejemplo.
