---
description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones que ha solicitado, como un vídeo que empieza a reproducirse, o las acciones que se producen implícitamente, como la finalización de un anuncio.
title: Escuchar eventos de reproductor de Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Información general {#implement-event-listeners-and-callbacks-overview}

Los controladores de eventos permiten que TVSDK responda a eventos. Cuando se produce un evento, el mecanismo de eventos de TVSDK llama al controlador de eventos registrado y pasa la información de evento al controlador.

El tiempo de ejecución de Flash proporciona un mecanismo de eventos genérico, que el TVSDK también utiliza y define una serie de eventos personalizados. La aplicación debe implementar detectores de eventos para los eventos de TVSDK que afecten a la aplicación.

1. Determine para qué eventos debe escuchar la aplicación.

   * **Eventos obligatorios**: escucha todos los eventos de reproducción.

     >[!IMPORTANT]
     >
     >El evento de reproducción `MediaPlayerStatusChangeEvent.STATUS_CHANGE` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar al siguiente paso del reproductor.

   * **Otros eventos**: Opcional, según la aplicación.

     Por ejemplo, si incorpora publicidad en la reproducción, escuche todas las `AdBreakPlaybackEvent` y `AdPlaybackEvent` eventos.

1. Implemente detectores de eventos para cada evento.

   TVSDK devuelve valores de parámetro a las llamadas de retorno del oyente de eventos. Estos valores proporcionan información relevante sobre el evento que puede utilizar en los oyentes para realizar las acciones adecuadas.

   El `Event` enumera todas las interfaces de devolución de llamada. Cada interfaz muestra los parámetros devueltos por esa interfaz.

   Por ejemplo:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registre los oyentes de devolución de llamada con `MediaPlayer` mediante `MediaPlayer.addEventListener`.

   `MediaPlayer` extiende `flash.events.IEventDispatcher`, que forma parte de los archivos principales del reproductor de Flash e incluye las funciones `addEventListener` y `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
