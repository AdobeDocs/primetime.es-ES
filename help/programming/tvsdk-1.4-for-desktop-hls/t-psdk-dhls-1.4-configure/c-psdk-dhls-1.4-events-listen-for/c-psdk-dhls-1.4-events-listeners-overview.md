---
description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que comienza a reproducirse, o las acciones que se producen implícitamente, como la finalización de un anuncio.
title: Escuche los eventos de Primetime Player
exl-id: 3a740245-a9e1-4e36-8761-f9f4b4e85b93
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Información general {#implement-event-listeners-and-callbacks-overview}

Los controladores de eventos permiten que TVSDK responda a eventos. Cuando se produce un evento, el mecanismo de eventos de TVSDK llama al controlador de eventos registrado y pasa la información del evento al controlador.

El tiempo de ejecución de Flash proporciona un mecanismo de eventos genérico, que el SDK de TVSDK también utiliza y define una serie de eventos personalizados. La aplicación debe implementar detectores de eventos para eventos TVSDK que afecten a la aplicación.

1. Determine qué eventos debe escuchar la aplicación.

   * **Eventos** necesarios: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `MediaPlayerStatusChangeEvent.STATUS_CHANGE` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar al siguiente paso del reproductor.

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, escuche todos los eventos `AdBreakPlaybackEvent` y `AdPlaybackEvent`.

1. Implemente detectores de eventos para cada evento.

   TVSDK devuelve valores de parámetro a las llamadas de retorno de event-listener. Estos valores proporcionan información relevante sobre el evento que se puede usar en los oyentes para realizar las acciones adecuadas.

   La clase `Event` enumera todas las interfaces de devolución de llamada. Cada interfaz muestra los parámetros que se devuelven para esa interfaz.

   Por ejemplo:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registre los oyentes de llamada de retorno con el objeto `MediaPlayer` utilizando `MediaPlayer.addEventListener`.

   `MediaPlayer` extiende  `flash.events.IEventDispatcher`, que forma parte de los archivos principales del reproductor de Flash e incluye las funciones  `addEventListener` y  `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
