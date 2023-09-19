---
description: Puede utilizar las notificaciones para implementar el registro en tiempo real en la aplicación de vídeo.
title: Añadir el registro y la depuración en tiempo real
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Añadir el registro y la depuración en tiempo real{#add-real-time-logging-and-debugging}

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

   Cada evento de notificación tiene un valor de índice que se incrementa automáticamente con la variable `NotificationHistory` clase.
