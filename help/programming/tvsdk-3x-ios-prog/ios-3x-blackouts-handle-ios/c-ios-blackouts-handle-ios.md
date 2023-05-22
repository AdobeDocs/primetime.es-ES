---
description: TVSDK gestiona las interrupciones en las emisiones de vídeo en directo y proporciona contenido alternativo durante una interrupción.
title: Controlar interrupciones
exl-id: 4a2ff371-69a9-4c13-ac61-3c5cd9c83a6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Controlar interrupciones {#handle-blackouts}

TVSDK gestiona las interrupciones en las emisiones de vídeo en directo y proporciona contenido alternativo durante una interrupción.

El caso de uso más común asociado con una interrupción de programación es cuando la aplicación de reproducción proporciona contenido alternativo a los usuarios que no cumplen los requisitos para ver el flujo principal. Esta aplicación puede utilizar TVSDK para determinar el principio y el final del periodo de interrupción. De este modo, al principio del periodo de interrupción, la reproducción puede cambiar del flujo principal a un flujo alternativo y, a continuación, volver al flujo principal cuando haya terminado el periodo de interrupción.

Para implementar la solución para este caso de uso:

1. Configure la aplicación para suscribirse a etiquetas de interrupción en un manifiesto de flujo en directo.

   TVSDK no detecta directamente las etiquetas de interrupción, pero permite a la aplicación suscribirse a las notificaciones cuando se encuentran etiquetas específicas durante el análisis del archivo de manifiesto.
1. Agregar un detector de notificaciones para `PTTimedMetadataChangedNotification`.

   Esta notificación se envía cada vez que se analiza una etiqueta suscrita en el manifiesto y se crea un nuevo `PTTimedMetadata` se prepara a partir de ella.

1. Implemente un método de escucha, como `onMediaPlayerSubscribedTagIdentified`, para `PTTimedMetadata` objetos en primer plano.

1. Cada vez que haya una actualización durante la reproducción, utilice el `PTMediaPlayerTimeChangeNotification` listener a gestionar `PTTimedMetadata` objetos.

1. Añada el `PTTimedMetadata` controlador.

   Este controlador le permite cambiar al contenido alternativo y volver al contenido principal tal como indica el `PTTimedMetadata` y su tiempo de reproducción.

1. Uso `onSubscribedTagInBackground` para implementar el método de escucha para `PTTimedMetadata` objetos en segundo plano.

   Este método monitoriza el tiempo en el flujo en segundo plano, lo que le ayuda a determinar cuándo puede volver de contenido alternativo al contenido principal.

1. Implemente un método de escucha para los errores en segundo plano.
1. Si el rango de interrupción está en el DVR en el flujo de reproducción, actualice los rangos no buscables.

   Su aplicación debe establecer el rango no buscable en el DVR en los siguientes casos:

   * Al unirse al flujo principal cuando hay un apagón en el DVR.
   * Al volver al contenido principal desde el contenido alternativo.
