---
description: Los eventos y las notificaciones ayudan a administrar los aspectos asincrónicos de la aplicación de vídeo.
title: Notificaciones y eventos para el estado, la actividad, los errores y el registro del reproductor
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Notificaciones y eventos para el estado, la actividad, los errores y el registro del reproductor {#notifications-and-events-for-player-status-activity-errors-and-logging}

Los eventos y las notificaciones ayudan a administrar los aspectos asincrónicos de la aplicación de vídeo.

`MediaPlayerStatus` Los objetos proporcionan información sobre los cambios en el estado del reproductor. `Notification` Los objetos proporcionan información sobre advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor. Los oyentes de eventos se implementan para capturar y responder a eventos ( objetos `MediaPlayerEvent` ).

La aplicación puede recuperar información de notificación y estado. Con esta información, también puede crear un sistema de registro para diagnósticos y validación.

## Contenido de notificación {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de notificaciones `MediaPlayerNotification` y cada notificación contiene la siguiente información:

* Una marca de tiempo
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`: INFO, WARN o ERROR.
   * `code`: Una representación numérica de la notificación.
   * `name`: Una descripción de la notificación legible en lenguaje natural, como SEEK_ERROR
   * `metadata`: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`: Referencia a otro  `MediaPlayerNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información localmente para análisis posteriores o enviarla a un servidor remoto para el registro y la representación gráfica.

## Configure el sistema de notificaciones {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Puede escuchar notificaciones.

El núcleo del sistema de notificación de Primetime Player es la clase `Notification`, que representa una notificación independiente.

Para recibir notificaciones, escuche las notificaciones de la siguiente manera:

1. Implemente la llamada de retorno `NotificationEventListener.onNotification()`.
1. TVSDK pasa un objeto `NotificationEvent` a la rellamada.

   >[!NOTE]
   >
   >Los tipos de notificaciones se enumeran en la enumeración `Notification.Type`:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Añadir el registro en tiempo real y la depuración {#section_9D4004308CB243AD9B50818895D10005}

Puede utilizar notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.

El sistema de notificaciones le permite recopilar información de registro y depuración para realizar diagnósticos y validaciones sin necesidad de estresar el sistema.

>[!IMPORTANT]
>
>El back-end de registro no forma parte de una configuración de producción y no se espera que gestione tráfico de alta carga. Si su implementación no necesita ser absolutamente completa, considere la eficacia de la transmisión de datos para evitar sobrecargar su sistema.

Este es un ejemplo de cómo recuperar notificaciones:

1. Cree un subproceso de ejecución basado en temporizador para la aplicación de vídeo que consulte periódicamente los datos recopilados por el sistema de notificación TVSDK.
1. Si el intervalo del temporizador es demasiado grande y el tamaño de la lista de eventos es demasiado pequeño, la lista de eventos de notificación se desbordará.

   >[!NOTE]
   >
   >Para evitar este desbordamiento, realice una de las siguientes acciones:
   >
   >1. Disminuya el intervalo de tiempo que impulsa el subproceso que sondea por nuevos eventos.
      >
      >
   1. Aumente el tamaño de la lista de notificaciones.


1. Serialice las entradas de evento de notificación más recientes en formato JSON y envíe las entradas a un servidor remoto para su posprocesamiento.

   >[!NOTE]
   >
   >El servidor remoto puede mostrar gráficamente los datos proporcionados en tiempo real.

1. Para detectar la pérdida de eventos de notificación, busque espacios en la secuencia de valores de índice de eventos.