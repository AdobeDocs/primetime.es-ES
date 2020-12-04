---
description: Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.
seo-description: Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.
seo-title: Añadir el registro y la depuración en tiempo real
title: Añadir el registro y la depuración en tiempo real
uuid: 037daf57-a1b3-4b42-ac51-81179fb36915
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Añadir el registro y la depuración en tiempo real{#add-real-time-logging-and-debugging}

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
