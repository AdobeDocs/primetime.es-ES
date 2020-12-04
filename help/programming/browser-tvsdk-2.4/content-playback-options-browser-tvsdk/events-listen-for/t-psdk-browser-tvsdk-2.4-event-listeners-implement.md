---
description: Los controladores de evento permiten que TVSDK del explorador responda a eventos.
seo-description: Los controladores de evento permiten que TVSDK del explorador responda a eventos.
seo-title: Implementar escuchas de evento y rellamadas
title: Implementar escuchas de evento y rellamadas
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# Implementar escuchas y rellamadas de evento{#implement-event-listeners-and-callbacks}

Los controladores de evento permiten que TVSDK del explorador responda a eventos.

Cuando se produce un evento, el mecanismo de evento del TVSDK del explorador llama al controlador de evento registrado y pasa la información del evento al controlador.

La aplicación debe implementar detectores de evento para eventos TVSDK del explorador que afecten a la aplicación.

1. Determine los eventos que debe escuchar la aplicación.

   * **Eventos** requeridos: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `STATUS_CHANGED` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar el siguiente paso del reproductor.

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, escuche todos los eventos `AdBreakPlaybackEvent` y `AdPlaybackEvent`.

1. Implementar escuchas de evento para cada evento.

   TVSDK del explorador devuelve valores de parámetro a las llamadas de retorno de oyente de evento. Estos valores proporcionan información relevante sobre el evento que puede utilizar en los oyentes para realizar las acciones adecuadas.

   Por ejemplo:

   * Tipo de evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Propiedad evento: `MediaPlayerStatus.<event>` se usa así:

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

1. Registre los oyentes de llamada de retorno con el objeto `MediaPlayer` mediante `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
