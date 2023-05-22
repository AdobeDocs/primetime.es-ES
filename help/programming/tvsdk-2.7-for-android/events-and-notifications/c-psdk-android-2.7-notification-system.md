---
description: Los objetos MediaPlayerStatus proporcionan información sobre los cambios en el estado del reproductor. Los objetos de notificación proporcionan información sobre advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor. Los detectores de eventos se implementan para capturar y responder a eventos (objetos MediaPlayerEvent).
title: Notificaciones y eventos para el estado del reproductor, la actividad, los errores y el registro
exl-id: c25e834e-ffa0-444c-9285-331e6841ac29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Notificaciones y eventos para el estado del reproductor, la actividad, los errores y el registro {#notifications-and-events-for-player-status-activity-errors-and-logging}

Los eventos y las notificaciones le ayudan a administrar los aspectos asincrónicos de la aplicación de vídeo.

Los objetos MediaPlayerStatus proporcionan información sobre los cambios en el estado del reproductor. Los objetos de notificación proporcionan información sobre advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor. Los detectores de eventos se implementan para capturar y responder a eventos (objetos MediaPlayerEvent).

La aplicación puede recuperar información de notificación y estado. Con esta información, también podría crear un sistema de registro para el diagnóstico y la validación.

## Contenido de notificación {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de `MediaPlayerNotification` notificaciones, y cada notificación contiene la siguiente información:

* Una marca de tiempo
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`: INFO, WARN o ERROR.
   * `code`: una representación numérica de la notificación.
   * `name`: una descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`: Pares de clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`: una referencia a otra `MediaPlayerNotification` que afecta directamente a esta notificación.

Puede almacenar esta información localmente para su posterior análisis o enviarla a un servidor remoto para su registro y representación gráfica.

## Configuración del sistema de notificaciones {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Puede escuchar las notificaciones.

El núcleo del sistema de notificación del reproductor de Primetime es el `Notification` , que representa una notificación independiente.

Para recibir notificaciones, escuche notificaciones como se indica a continuación:

1. Implementación de `NotificationEventListener.onNotification()` devolución de llamada.
1. TVSDK pasa un `NotificationEvent` objeto a la llamada de retorno.

   >[!NOTE]
   >
   >Los tipos de notificaciones se enumeran en `Notification.Type` enum:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Añadir el registro y la depuración en tiempo real {#section_9D4004308CB243AD9B50818895D10005}

Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.

El sistema de notificación le permite recopilar información de registro y depuración para diagnósticos y validación sin sobrecargar el sistema.

>[!IMPORTANT]
>
>El back end de registro no forma parte de una configuración de producción y no se espera que administre tráfico de alta carga. Si su implementación no necesita estar absolutamente completa, considere la eficacia de la transmisión de datos para evitar sobrecargar su sistema.

A continuación se muestra un ejemplo de cómo recuperar notificaciones:

1. Cree un subproceso de ejecución basado en temporizador para la aplicación de vídeo que consulte periódicamente los datos recopilados por el sistema de notificación de TVSDK.
1. Si el intervalo del temporizador es demasiado grande y el tamaño de la lista de eventos es demasiado pequeño, la lista de eventos de notificación se desbordará.

   >[!NOTE]
   >
   >Para evitar este desbordamiento, realice una de las siguientes acciones:
   >
   >1. Reduzca el intervalo de tiempo que controla el subproceso que sondea los nuevos eventos.
   >1. Aumente el tamaño de la lista de notificaciones.


1. Serialice las entradas de evento de notificación más recientes en formato JSON y envíe las entradas a un servidor remoto para su posprocesamiento.

   >[!NOTE]
   >
   >El servidor remoto puede mostrar gráficamente los datos proporcionados en tiempo real.

1. Para detectar la pérdida de eventos de notificación, busque espacios en la secuencia de valores de índice de eventos.
