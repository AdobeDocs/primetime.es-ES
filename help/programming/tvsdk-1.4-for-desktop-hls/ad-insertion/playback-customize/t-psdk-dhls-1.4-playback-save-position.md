---
description: Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.
seo-description: Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.
seo-title: Guardar la posición del vídeo y reanudarlo más tarde
title: Guardar la posición del vídeo y reanudarlo más tarde
uuid: 03ed5c63-008d-4dd1-9a31-baefa73b56e2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Guarde la posición del vídeo y reanude más tarde{#save-the-video-position-and-resume-later}

Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.

Las publicidades insertadas dinámicamente difieren entre las sesiones de usuario, por lo que al guardar la posición **con** publicidades duplicadas se hace referencia a una posición diferente en una sesión futura. TVSDK proporciona métodos para recuperar la posición de reproducción e ignorar las publicidades duplicadas.

1. Cuando el usuario cierra un vídeo, la aplicación recupera y guarda la posición en el vídeo.

   >[!TIP]
   >
   >No se incluyen las duraciones de los anuncios.

   Los saltos de publicidad pueden variar en cada sesión debido a patrones de publicidad, límites de frecuencia, etc. La hora actual del vídeo en una sesión puede ser diferente en una sesión futura. Al guardar una posición en el vídeo, la aplicación recupera la hora local. Utilice la propiedad `localTime` para leer esta posición, que puede guardar en el dispositivo o en una base de datos del servidor.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Por ejemplo: si el usuario se encuentra en el minuto 20 del video y esta posición incluye cinco minutos de anuncios, `currentTime` `be` tendrá &lt;a1/> 1200 segundos, mientras que `localTime` en esta posición tendrá `be` 900 segundos.

1. Restaure la sesión de usuario cuando se reanude la actividad del reproductor.

   TVSDK no reanuda la reproducción entre las inicializaciones de TVSDK porque no guarda ninguna información localmente. La aplicación debe implementar esta lógica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Para reanudar el vídeo en la misma posición:

   * Para reanudar la reproducción del vídeo desde la posición guardada en una sesión anterior, utilice `seekToLocal`.

      >[!TIP]
      >
      >Este método solo se llama con valores de hora locales. Si se llama al método con los resultados de tiempo actuales, se produce un comportamiento incorrecto.

   * Para buscar la hora actual, utilice `seek`.

1. Cuando la aplicación reciba el evento de cambio de estado `onStatusChanged`, busque la hora local guardada.
1. Proporcione los saltos de publicidad como se especifica en la interfaz de directivas de publicidad.
1. Implemente un selector de directivas de publicidad personalizado ampliando el selector de directivas de publicidad predeterminado.
1. Proporcione los pausas publicitarias que deben presentarse al usuario implementando `selectAdBreaksToPlay`.

   Cuando el reproductor introduce el estado PREPARADO, todas las publicidades ya se resuelven, por lo que la propiedad `AdPolicyInfo.adBreakTimelineItem` contiene todos los saltos de publicidad antes de la posición de tiempo local. La aplicación puede decidir reproducir una pausa publicitaria previa y reanudar a la hora local especificada, reproducir una pausa publicitaria media y reanudar a la hora local especificada o no reproducir ninguna pausa publicitaria.
