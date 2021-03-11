---
description: Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.
title: Guarde la posición del vídeo y reanude más tarde
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Guarde la posición del vídeo y reanude más tarde{#save-the-video-position-and-resume-later}

Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.

Los anuncios insertados de forma dinámica difieren entre las sesiones de usuario, por lo que guardar la posición **con** publicidad duplicada hace referencia a una posición diferente en una sesión futura. TVSDK proporciona métodos para recuperar la posición de reproducción e ignorar los anuncios duplicados.

1. Cuando el usuario sale de un vídeo, la aplicación recupera y guarda la posición en el vídeo.

   >[!TIP]
   >
   >No se incluyen las duraciones de los anuncios.

   Las pausas publicitarias pueden variar en cada sesión debido a patrones de anuncios, restricciones de frecuencia, etc. La hora actual del vídeo en una sesión puede ser diferente en una sesión futura. Al guardar una posición en el vídeo, la aplicación recupera la hora local . Utilice la propiedad `localTime` para leer esta posición , que puede guardar en el dispositivo o en una base de datos del servidor.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Por ejemplo, si el usuario se encuentra en el minuto 20 del vídeo y esta posición incluye cinco minutos de anuncios, `currentTime` tendrá `be` 1200 segundos, mientras que `localTime` en esta posición tendrá `be` 900 segundos.

1. Restaure la sesión del usuario cuando se reanude la actividad del reproductor.

   TVSDK no reanuda la reproducción entre las inicializaciones de TVSDK porque no guarda ninguna información localmente. La aplicación debe implementar esta lógica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Para reanudar el vídeo en la misma posición:

   * Para reanudar la reproducción del vídeo desde la posición guardada en una sesión anterior, utilice `seekToLocal`.

      >[!TIP]
      >
      >Solo se llama a este método con valores de hora locales. Si se llama al método con resultados de tiempo actuales, se produce un comportamiento incorrecto.

   * Para buscar el tiempo actual, utilice `seek`.

1. Cuando la aplicación reciba el evento de cambio de estado `onStatusChanged` , busque la hora local guardada.
1. Proporcione los pausas publicitarias tal como se especifica en la interfaz de directivas de publicidad.
1. Implemente un selector de políticas de publicidad personalizado ampliando el selector de directivas de publicidad predeterminado.
1. Proporcione las pausas publicitarias que se deben presentar al usuario implementando `selectAdBreaksToPlay`.

   Cuando el reproductor introduce el estado PREPARADO, todos los anuncios ya se han resuelto, por lo que la propiedad `AdPolicyInfo.adBreakTimelineItem` contiene todos los saltos de anuncio antes de la posición horaria local. La aplicación puede decidir reproducir una pausa publicitaria previa y reanudar a la hora local especificada, reproducir una pausa publicitaria intermedia y reanudar a la hora local especificada o no reproducir ninguna pausa publicitaria.
