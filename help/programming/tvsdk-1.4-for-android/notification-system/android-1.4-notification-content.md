---
description: Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
title: Contenido de notificación
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Contenido de notificación {#notification-content}

Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la notificación y la información de estado. También puede crear un sistema de registro para diagnósticos y validación utilizando la información de notificación.

Los oyentes de eventos se implementan para capturar eventos y responder a ellos. Muchos eventos proporcionan `MediaPlayerNotification` notificaciones de estado.

`MediaPlayerNotification` proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de `MediaPlayerNotification` notificaciones. Cada notificación contiene la siguiente información:

* Marca de tiempo
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`: INFO, WARN o ERROR.
   * `code`: una representación numérica de la notificación.
   * `name`: una descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`: Pares de clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`: una referencia a otra `MediaPlayerNotification` que afecta directamente a esta notificación.

Puede almacenar esta información localmente para su posterior análisis o enviarla a un servidor remoto para su registro y representación gráfica.

## Configuración del sistema de notificaciones {#set-up-your-notification-system}

Puede escuchar las notificaciones y agregar sus propias notificaciones al historial de notificaciones.

El núcleo del sistema de notificación del reproductor de Primetime es el `Notification` , que representa una notificación independiente.

El `NotificationHistory` proporciona un mecanismo para acumular notificaciones. Almacena un registro de objetos notification (NotificationHistoryItem) que representa una colección de Notificaciones.

Para recibir notificaciones:

* Escuchar notificaciones
* Añadir notificaciones al historial de notificaciones

1. Escuche los cambios de estado.
1. Implementación de `MediaPlayer.PlaybackEventListener.onStateChanged` devolución de llamada.
1. TVSDK pasa dos parámetros a la llamada de retorno:

   * El nuevo estado ( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` objeto

## Añadir el registro y la depuración en tiempo real {#add-real-time-logging-and-debugging}

Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.

El sistema de notificación le permite recopilar información de registro y depuración para diagnósticos y validación sin sobrecargar el sistema.

>[!IMPORTANT]
>
>El back end de registro no forma parte de una configuración de producción y no se espera que administre tráfico de alta carga. Si su implementación no necesita estar absolutamente completa, considere la eficacia de la transmisión de datos para evitar sobrecargar su sistema.

A continuación, se muestra un ejemplo de cómo recuperar notificaciones.

1. Cree un subproceso de ejecución basado en temporizador para la aplicación de vídeo que consulte periódicamente los datos recopilados por el sistema de notificación de TVSDK.

1. Si el intervalo del temporizador es demasiado grande y el tamaño de la lista de eventos es demasiado pequeño, la lista de eventos de notificación se desbordará. Para evitar este desbordamiento, realice una de las siguientes acciones:

   * Reduzca el intervalo de tiempo que controla el subproceso que sondea los nuevos eventos.
   * Aumente el tamaño de la lista de notificaciones.

1. Serialice las entradas de evento de notificación más recientes en formato JSON y envíe las entradas a un servidor remoto para su posprocesamiento.

   El servidor remoto podía mostrar gráficamente los datos proporcionados en tiempo real.
1. Para detectar la pérdida de eventos de notificación, busque espacios en la secuencia de valores de índice de eventos.

   Cada evento de notificación tiene un valor de índice que se incrementa automáticamente con la variable `session.NotificationHistory` clase.

## Etiquetas ID3 {#id-tags}

Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y envía un evento. La aplicación puede extraer datos de la etiqueta.

>[!IMPORTANT]
>
>TVSDK reconoce metadatos ID3 (versión 2.3.0 o 2.4.0) en flujos de audio (AAC) y vídeo (H.264), en cualquiera de sus posibles codificaciones (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora las etiquetas ID3 que no están en una de las versiones o formatos reconocidos. La codificación no especificada se trata como UTF8.

Cuando TVSDK detecta metadatos de ID3, emite una notificación con los siguientes datos:

* InfoCode = 303007
* TIPO = ID3
* NAME = no presente
* ID = 0

1. Implementación de un detector de eventos para `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` y regístrela en el `MediaPlayer` objeto.

   TVSDK llama a este oyente cuando detecta metadatos de ID3.

   >[!NOTE]
   >
   >Las indicaciones de anuncio personalizadas utilizan lo mismo `onTimedMetadata` para indicar la detección de una etiqueta nueva. Esto no debería causar ninguna confusión, ya que las señales de publicidad personalizadas se detectan en el nivel de manifiesto y las etiquetas ID3 están incrustadas en la secuencia. Para obtener más información, consulte custom-tags-configure .

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
