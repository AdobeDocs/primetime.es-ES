---
description: Los controladores de eventos permiten que el TVSDK del explorador responda a los eventos.
title: Implementación de oyentes de eventos y llamadas de retorno
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Implemente los oyentes de eventos y las llamadas de retorno{#implement-event-listeners-and-callbacks}

Los controladores de eventos permiten que el TVSDK del explorador responda a los eventos.

Cuando se produce un evento, el mecanismo de eventos del TVSDK del explorador llama al controlador de eventos registrado y pasa la información del evento al controlador.

La aplicación debe implementar detectores de eventos para los eventos TVSDK del explorador que afecten a la aplicación.

1. Determine qué eventos debe escuchar la aplicación.

   * **Eventos** necesarios: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `STATUS_CHANGED` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar al siguiente paso del reproductor.

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, escuche todos los eventos `AdBreakPlaybackEvent` y `AdPlaybackEvent`.

1. Implemente detectores de eventos para cada evento.

   El SDK de explorador devuelve valores de parámetro a las llamadas de retorno de event-listener. Estos valores proporcionan información relevante sobre el evento que se puede usar en los oyentes para realizar las acciones adecuadas.

   Por ejemplo:

   * Tipo de evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Propiedad de evento: `MediaPlayerStatus.<event>` usado de esta manera:

```js
player.addEventListener( 
            AdobePSDK.PSDKEventType.STATUS_CHANGED,  
            onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break;
```

1. Registre los oyentes de llamada de retorno con el objeto `MediaPlayer` utilizando `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
