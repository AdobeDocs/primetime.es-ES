---
description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.
seo-description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.
seo-title: Escuchar eventos de Primetime Player
title: Escuchar eventos de Primetime Player
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Información general {#implement-event-listeners-and-callbacks-overview}

Los controladores de eventos permiten que TVSDK responda a los eventos. Cuando se produce un evento, el mecanismo de eventos de TVSDK llama al controlador de eventos registrado y pasa la información del evento al controlador.

Flash Runtime proporciona un mecanismo de eventos genérico, que el TVSDK también utiliza y define una serie de eventos personalizados. La aplicación debe implementar detectores de eventos para los eventos TVSDK que afecten a la aplicación.

Para obtener una lista completa de los eventos de análisis de vídeo, consulte [Seguimiento de la reproducción](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html)de vídeo principal.

1. Determinar los eventos que debe escuchar la aplicación.

   * **Eventos** requeridos: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `MediaPlayerStatusChangeEvent.STATUS_CHANGE` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar el siguiente paso del reproductor.

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, escuche todos los `AdBreakPlaybackEvent` eventos y `AdPlaybackEvent` los eventos.

1. Implementar detectores de eventos para cada evento.

   TVSDK devuelve valores de parámetro a las llamadas de retorno de event-listener. Estos valores proporcionan información relevante sobre el evento que puede utilizar en los oyentes para realizar las acciones adecuadas.

   La `Event` clase enumera todas las interfaces de llamada de retorno. Cada interfaz muestra los parámetros que se devuelven para esa interfaz.

   Por ejemplo:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registre los oyentes de llamada de retorno con el `MediaPlayer` objeto mediante `MediaPlayer.addEventListener`.

   `MediaPlayer` prolonga `flash.events.IEventDispatcher`, que forma parte de los archivos principales de Flash Player e incluye las funciones `addEventListener` y `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


