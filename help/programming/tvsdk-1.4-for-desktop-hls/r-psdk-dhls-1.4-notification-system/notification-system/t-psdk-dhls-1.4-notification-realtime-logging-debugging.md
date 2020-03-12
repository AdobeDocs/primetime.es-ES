---
description: Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.
seo-description: Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.
seo-title: Agregar registro y depuración en tiempo real
title: Agregar registro y depuración en tiempo real
uuid: 568ea2e7-963b-427e-9cb2-e261e4423902
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Agregar registro y depuración en tiempo real{#add-real-time-logging-and-debugging}

Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.

El sistema de notificaciones le permite recopilar información de registro y depuración para realizar diagnósticos y validaciones sin tener que hacer demasiado hincapié en el sistema.

>[!IMPORTANT]
>
>El back-end de inicio de sesión no forma parte de una configuración de producción y no se espera que gestione tráfico de alta carga. Si su implementación no necesita ser absolutamente completa, considere la eficacia de la transmisión de datos para evitar sobrecargar su sistema.

Este es un ejemplo de cómo recuperar notificaciones.

1. Cree un subproceso de ejecución basado en temporizador para la aplicación de vídeo que consulte periódicamente los datos recopilados por el sistema de notificación TVSDK.

1. Si el intervalo del temporizador es demasiado grande y el tamaño de la lista de eventos es demasiado pequeño, la lista de eventos de notificación se desbordará. Para evitar este desbordamiento, realice una de las siguientes acciones:

   * Reduzca el intervalo de tiempo que genera el subproceso que sondea para nuevos eventos.
   * Aumente el tamaño de la lista de notificaciones.

1. Serialice las últimas entradas de eventos de notificación en formato JSON y envíe las entradas a un servidor remoto para su postprocesamiento.

   El servidor remoto podría entonces mostrar gráficamente los datos proporcionados en tiempo real.
1. Para detectar la pérdida de eventos de notificación, busque espacios en la secuencia de valores de índice de eventos.

   Cada evento de notificación tiene un valor de índice que la `NotificationHistory` clase incrementa automáticamente.
