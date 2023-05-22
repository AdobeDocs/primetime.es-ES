---
description: Los controladores de eventos permiten que el TVSDK del explorador responda a eventos.
title: Implementación de oyentes de eventos y llamadas de retorno
exl-id: 2ab33c03-4df6-48e5-825c-95aeef8855d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Implementación de oyentes de eventos y llamadas de retorno{#implement-event-listeners-and-callbacks}

Los controladores de eventos permiten que el TVSDK del explorador responda a eventos.

Cuando se produce un evento, el mecanismo de eventos de TVSDK del explorador llama al controlador de eventos registrado y pasa la información de eventos al controlador.

La aplicación debe implementar detectores de eventos para los eventos TVSDK del explorador que afecten a la aplicación.

1. Determine para qué eventos debe escuchar la aplicación.

   * **Eventos obligatorios**: escucha todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `STATUS_CHANGED` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar al siguiente paso del reproductor.

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, escuche todas las `AdBreakPlaybackEvent` y `AdPlaybackEvent` eventos.

1. Implemente detectores de eventos para cada evento.

   El TVSDK del explorador devuelve valores de parámetro a las llamadas de retorno del oyente de eventos. Estos valores proporcionan información relevante sobre el evento que puede utilizar en los oyentes para realizar las acciones adecuadas.

   Por ejemplo:

   * Tipo de evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Propiedad de evento: `MediaPlayerStatus.<event>` se usa de esta manera:

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

1. Registre los oyentes de devolución de llamada con `MediaPlayer` mediante `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
