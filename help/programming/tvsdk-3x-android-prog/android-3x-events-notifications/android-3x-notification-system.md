---
description: Los eventos y las notificaciones le ayudan a administrar los aspectos asincrónicos de la aplicación de vídeo.
seo-description: Los eventos y las notificaciones le ayudan a administrar los aspectos asincrónicos de la aplicación de vídeo.
seo-title: Notificaciones y eventos para el estado, la actividad, los errores y el registro del reproductor
title: Notificaciones y eventos para el estado, la actividad, los errores y el registro del reproductor
uuid: c4a108e7-72aa-4c96-9538-b1385343d6af
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Notificaciones y eventos para el estado, la actividad, los errores y el registro del reproductor {#notifications-and-events-for-player-status-activity-errors-and-logging}

Los eventos y las notificaciones le ayudan a administrar los aspectos asincrónicos de la aplicación de vídeo.

`MediaPlayerStatus` los objetos proporcionan información sobre los cambios en el estado del reproductor. `Notification` los objetos proporcionan información sobre advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor. Los oyentes de evento se implementan para capturar y responder a eventos ( `MediaPlayerEvent` objetos).

La aplicación puede recuperar información de notificación y estado. Con esta información, también puede crear un sistema de registro para diagnósticos y validación.

## Contenido de notificación {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de `MediaPlayerNotification` las notificaciones y cada notificación contiene la siguiente información:

* Marca de hora
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`:: INFORMACIÓN, ADVERTENCIA o ERROR.
   * `code`:: Una representación numérica de la notificación.
   * `name`:: Descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`:: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave llamada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`:: Referencia a otro `MediaPlayerNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información localmente para su posterior análisis o enviarla a un servidor remoto para que la registre y la represente en forma gráfica.

## Configurar el sistema de notificaciones {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Puede escuchar notificaciones.

El núcleo del sistema de notificaciones de Primetime Player es la `Notification` clase, que representa una notificación independiente.

Para recibir notificaciones, escuche las notificaciones de la siguiente manera:

1. Implemente la `NotificationEventListener.onNotification()` llamada de retorno.
1. TVSDK pasa un `NotificationEvent` objeto a la llamada de retorno.

   >[!NOTE]
   >
   >Los tipos de notificaciones se enumeran en la enumeración `Notification.Type` :

   * `ERROR`
   * `INFO`
   * `WARNING`

## Añadir el registro y la depuración en tiempo real {#section_9D4004308CB243AD9B50818895D10005}

Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.

El sistema de notificaciones le permite recopilar información de registro y depuración para realizar diagnósticos y validaciones sin que esto afecte al sistema.

>[!IMPORTANT]
>
>El back-end de inicio de sesión no forma parte de una configuración de producción y no se espera que gestione tráfico de alta carga. Si su implementación no necesita ser absolutamente completa, considere la eficacia de la transmisión de datos para evitar sobrecargar su sistema.

A continuación se muestra un ejemplo de cómo recuperar notificaciones:

1. Cree un subproceso de ejecución basado en temporizador para la aplicación de vídeo que consulta periódicamente los datos recopilados por el sistema de notificaciones TVSDK.
1. Si el intervalo del temporizador es demasiado grande y el tamaño de la lista del evento es demasiado pequeño, la lista del evento de notificación se desbordará.

   >[!NOTE]
   >
   >Para evitar este desbordamiento, realice una de las siguientes acciones:
   >
   >1. Disminuya el intervalo de tiempo que impulsa el subproceso que sondea por nuevos eventos.
      >
      >
   1. Aumente el tamaño de la lista de notificación.


1. Serialice las últimas entradas de evento de notificación en formato JSON y envíe las entradas a un servidor remoto para su postprocesamiento.

   >[!NOTE]
   >
   >El servidor remoto puede mostrar gráficamente los datos proporcionados en tiempo real.

1. Para detectar la pérdida de eventos de notificación, busque espacios en la secuencia de valores de índice de evento.