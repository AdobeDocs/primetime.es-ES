---
description: Los controladores de eventos permiten al Explorador TVSDK responder a eventos.
seo-description: Los controladores de eventos permiten al Explorador TVSDK responder a eventos.
seo-title: Implementar escuchas de eventos y rellamadas
title: Implementar escuchas de eventos y rellamadas
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Implementar escuchas de eventos y rellamadas{#implement-event-listeners-and-callbacks}

Los controladores de eventos permiten al Explorador TVSDK responder a eventos.

Cuando se produce un evento, el mecanismo de eventos del TVSDK del explorador llama al controlador de eventos registrado y pasa la información del evento al controlador.

La aplicación debe implementar detectores de eventos para los eventos TVSDK del explorador que afecten a la aplicación.

1. Determinar los eventos que debe escuchar la aplicación.

   * **Eventos** requeridos: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `STATUS_CHANGED` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar el siguiente paso del reproductor.

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, escuche todos los `AdBreakPlaybackEvent` eventos y `AdPlaybackEvent` los eventos.

1. Implementar detectores de eventos para cada evento.

   El SDK de TVSDK del explorador devuelve valores de parámetro a las llamadas de retorno del detector de eventos. Estos valores proporcionan información relevante sobre el evento que puede utilizar en los oyentes para realizar las acciones adecuadas.

   Por ejemplo:

   * Tipo de evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Propiedad Event: se `MediaPlayerStatus.<event>` usa así:

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

1. Registre los oyentes de llamada de retorno con el `MediaPlayer` objeto mediante `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
