---
description: TVSDK gestiona bloqueos en flujos de vídeo en directo y proporciona contenido alternativo durante una interrupción.
seo-description: TVSDK gestiona bloqueos en flujos de vídeo en directo y proporciona contenido alternativo durante una interrupción.
seo-title: Gestión de interrupciones en flujos activos
title: Gestión de interrupciones en flujos activos
uuid: 1f70a272-bc77-4d41-a999-b076cb42ac5e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Controlar los bloqueos en flujos activos{#handle-blackouts-in-live-streams}

TVSDK gestiona bloqueos en flujos de vídeo en directo y proporciona contenido alternativo durante una interrupción.

El caso de uso más común asociado a un bloqueo de programación es cuando la aplicación de reproductor proporciona contenido alternativo a los usuarios que no pueden ver el flujo principal. Esta aplicación puede utilizar TVSDK para determinar el comienzo y el final del período de interrupción. De este modo, al principio del período de interrupción, la reproducción puede cambiar del flujo principal a un flujo alternativo y, a continuación, volver al flujo principal cuando el período de interrupción haya finalizado.

Para implementar la solución para este caso de uso:

1. Configure la aplicación para suscribirse a etiquetas de bloqueo en un manifiesto de flujo en directo.

   TVSDK no conoce directamente las etiquetas de bloqueo, pero permite que la aplicación se suscriba a notificaciones cuando se encuentran etiquetas específicas durante el análisis de archivos de manifiesto.
1. Añada un detector de notificaciones para `PTTimedMetadataChangedNotification`.

   Esta notificación se envía cada vez que se analiza una etiqueta suscrita en el manifiesto y se prepara un nuevo `PTTimedMetadata` a partir de él.

1. Implemente un método de escucha, como `onMediaPlayerSubscribedTagIdentified`, para objetos `PTTimedMetadata` en primer plano.

1. Cada vez que se produzca una actualización durante la reproducción, utilice el detector `PTMediaPlayerTimeChangeNotification` para controlar los objetos `PTTimedMetadata`.

1. Añada el controlador `PTTimedMetadata`.

   Este controlador le permite cambiar al contenido alternativo y volver al contenido principal como lo indica el objeto `PTTimedMetadata` y su tiempo de reproducción.

1. Utilice `onSubscribedTagInBackground` para implementar el método de escucha para objetos `PTTimedMetadata` en segundo plano.

   Este método supervisa la temporización en el flujo de fondo, lo que le ayuda a determinar cuándo puede cambiar de contenido alternativo al contenido principal.

1. Implemente un método de escucha para los errores en segundo plano.
1. Si el rango de interrupción está en el DVR en el flujo de reproducción, actualice los rangos que no se pueden buscar.

   La aplicación debe establecer el rango no buscable en el DVR en los siguientes casos:

   * Cuando se une al flujo principal cuando hay un apagón en el DVR.
   * Al volver al contenido principal desde el contenido alternativo.

