---
description: Los objetos MediaPlayerNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-description: Los objetos MediaPlayerNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-title: Contenido de notificación
title: Contenido de notificación
uuid: 89fb8f63-b0d5-45cd-bdad-348529fd07d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# Contenido de notificación {#notification-content}

Los objetos MediaPlayerNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la notificación y la información de estado. También puede crear un sistema de registro para diagnósticos y validación mediante la información de notificación.

Los oyentes de evento se implementan para capturar y responder a eventos. Muchos eventos proporcionan `MediaPlayerNotification` notificaciones de estado.

`MediaPlayerNotification` proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de las `MediaPlayerNotification` notificaciones. Cada notificación contiene la siguiente información:

* Marca de hora
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`:: INFORMACIÓN, ADVERTENCIA o ERROR.
   * `code`:: Una representación numérica de la notificación.
   * `name`:: Descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`:: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`:: Referencia a otro  `MediaPlayerNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información localmente para su posterior análisis o enviarla a un servidor remoto para que la registre y la represente en forma gráfica.

## Configure el sistema de notificaciones {#set-up-your-notification-system}

Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.

El núcleo del sistema de notificaciones de Primetime Player es la clase `Notification`, que representa una notificación independiente.

La clase `NotificationHistory` proporciona un mecanismo para la acumulación de notificaciones. Almacena un registro de objetos de notificación (NotificationHistoryItem) que representa una colección de notificaciones.

Para recibir notificaciones:

* Escuchar notificaciones
* Añadir notificaciones al historial de notificaciones

1. Escuche los cambios de estado.
1. Implemente la devolución de llamada `MediaPlayer.PlaybackEventListener.onStateChanged`.
1. TVSDK pasa dos parámetros a la llamada de retorno:

   * El nuevo estado ( `MediaPlayer.PlayerState`)
   * Un objeto `MediaPlayerNotification`

## Añadir el registro y la depuración en tiempo real {#add-real-time-logging-and-debugging}

Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.

El sistema de notificaciones le permite recopilar información de registro y depuración para realizar diagnósticos y validaciones sin tener que hacer demasiado hincapié en el sistema.

>[!IMPORTANT]
>
>El back-end de inicio de sesión no forma parte de una configuración de producción y no se espera que gestione tráfico de alta carga. Si su implementación no necesita ser absolutamente completa, considere la eficacia de la transmisión de datos para evitar sobrecargar su sistema.

Este es un ejemplo de cómo recuperar notificaciones.

1. Cree un subproceso de ejecución basado en temporizador para la aplicación de vídeo que consulta periódicamente los datos recopilados por el sistema de notificaciones TVSDK.

1. Si el intervalo del temporizador es demasiado grande y el tamaño de la lista del evento es demasiado pequeño, la lista del evento de notificación se desbordará. Para evitar este desbordamiento, realice una de las siguientes acciones:

   * Disminuya el intervalo de tiempo que impulsa el subproceso que sondea por nuevos eventos.
   * Aumente el tamaño de la lista de notificación.

1. Serialice las últimas entradas de evento de notificación en formato JSON y envíe las entradas a un servidor remoto para su postprocesamiento.

   El servidor remoto podría entonces mostrar gráficamente los datos proporcionados en tiempo real.
1. Para detectar la pérdida de eventos de notificación, busque espacios en la secuencia de valores de índice de evento.

   Cada evento de notificación tiene un valor de índice que se incrementa automáticamente en la clase `session.NotificationHistory`.

## Etiquetas ID3 {#id-tags}

Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en los flujos HLS y distribuye un evento. La aplicación puede extraer datos de la etiqueta .

>[!IMPORTANT]
>
>TVSDK reconoce metadatos ID3 (versión 2.3.0 o 2.4.0) en flujos de audio (AAC) y vídeo (H.264), en cualquiera de sus posibles codificaciones (ASCII, UTF8, UTF16-BE o UTF16-LE). Omite las etiquetas ID3 que no están en una de las versiones o formatos reconocidos. La codificación no especificada se trata como UTF8.

Cuando TVSDK detecta metadatos ID3, emite una notificación con los siguientes datos:

* InfoCode = 303007
* TYPE = ID3
* NAME = no está presente
* ID = 0

1. Implemente un detector de evento para `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` y regístrelo con el objeto `MediaPlayer`.

   TVSDK llama a este detector cuando detecta metadatos ID3.

   >[!NOTE]
   >
   >Las señales de publicidad personalizadas utilizan el mismo evento `onTimedMetadata` para indicar la detección de una nueva etiqueta. Esto no debe causar ninguna confusión, ya que las señales de publicidad personalizadas se detectan en el nivel de manifiesto y las etiquetas ID3 se incrustan en el flujo. Para obtener más información, consulte custom-tags-configure .

1. Recupere los metadatos.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
