---
description: TVSDK gestiona los bloqueos en las emisiones de vídeo en directo y proporciona contenido alternativo durante una interrupción.
title: Gestión de interrupciones en flujos en directo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Gestión de bloqueos en flujos en directo{#handle-blackouts-in-live-streams}

TVSDK gestiona los bloqueos en las emisiones de vídeo en directo y proporciona contenido alternativo durante una interrupción.

El caso de uso más común asociado con un bloqueo de programación es cuando la aplicación del reproductor proporciona contenido alternativo a los usuarios que no pueden ver el flujo principal. Esta aplicación puede utilizar TVSDK para determinar el principio y el final del periodo de interrupción. De este modo, al principio del periodo de interrupción, la reproducción puede cambiar del flujo principal a un flujo alternativo y, a continuación, volver al flujo principal cuando termine el periodo de interrupción.

Para implementar la solución para este caso de uso:

1. Configure la aplicación para suscribirse a las etiquetas de interrupción en un manifiesto de flujo en directo.

   TVSDK no conoce directamente las etiquetas de interrupción, pero permite a la aplicación suscribirse a notificaciones cuando se encuentran etiquetas específicas durante el análisis de archivos de manifiesto.
1. Agregue un oyente de notificación para `PTTimedMetadataChangedNotification`.

   Esta notificación se envía cada vez que se analiza una etiqueta suscrita en el manifiesto y se prepara una nueva `PTTimedMetadata` a partir de ella.

1. Implemente un método de escucha, como `onMediaPlayerSubscribedTagIdentified`, para los objetos `PTTimedMetadata` en primer plano.

1. Cada vez que se produce una actualización durante la reproducción, utilice el `PTMediaPlayerTimeChangeNotification` listener para gestionar los objetos `PTTimedMetadata`.

1. Añada el controlador `PTTimedMetadata`.

   Este controlador le permite cambiar al contenido alternativo y regresar al contenido principal como indica el objeto `PTTimedMetadata` y su tiempo de reproducción.

1. Utilice `onSubscribedTagInBackground` para implementar el método de escucha para los objetos `PTTimedMetadata` en segundo plano.

   Este método supervisa la temporización en el flujo de fondo, lo que le ayuda a determinar cuándo puede volver a cambiar el contenido alternativo al contenido principal.

1. Implemente un método de escucha para los errores en segundo plano.
1. Si el rango de bloqueo está en el DVR en el flujo de reproducción, actualice los rangos no buscables.

   Su aplicación debe establecer el rango no buscable en el DVR en los siguientes casos:

   * Cuando se une al flujo principal cuando hay un apagón en el DVR.
   * Al volver al contenido principal desde el contenido alternativo.

