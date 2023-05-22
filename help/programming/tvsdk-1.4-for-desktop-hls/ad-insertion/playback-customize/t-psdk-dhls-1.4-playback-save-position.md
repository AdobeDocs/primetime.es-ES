---
description: Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.
title: Guardar la posición del vídeo y reanudarlo más tarde
exl-id: a06897a6-bf57-4902-b1b4-e931419b56ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Guardar la posición del vídeo y reanudarlo más tarde{#save-the-video-position-and-resume-later}

Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.

Los anuncios insertados dinámicamente difieren entre las sesiones de usuario, por lo que se guarda la posición **con** los anuncios empalmados hacen referencia a una posición diferente en una sesión futura. TVSDK proporciona métodos para recuperar la posición de reproducción al ignorar los anuncios empalmados.

1. Cuando el usuario sale de un vídeo, la aplicación recupera y guarda la posición en el vídeo.

   >[!TIP]
   >
   >No se incluyen las duraciones de los anuncios.

   Las pausas publicitarias pueden variar en cada sesión debido a patrones de anuncios, restricción de frecuencia, etc. La hora actual del vídeo en una sesión puede ser diferente en una sesión futura. Al guardar una posición en el vídeo, la aplicación recupera la hora local Utilice el `localTime` para leer esta posición , que puede guardar en el dispositivo o en una base de datos del servidor.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Por ejemplo, si el usuario se encuentra en el minuto 20 del vídeo y esta posición incluye cinco minutos de anuncios, `currentTime` testamento `be` 1200 segundos, mientras `localTime` en esta posición `be` 900 segundos.

1. Restaura la sesión del usuario cuando se reanuda la actividad del reproductor.

   TVSDK no reanuda la reproducción entre las inicializaciones de TVSDK porque no guarda ninguna información localmente. La aplicación debe implementar esta lógica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Para reanudar el vídeo en la misma posición:

   * Para reanudar la reproducción del vídeo desde la posición guardada en una sesión anterior, utilice `seekToLocal`.

      >[!TIP]
      >
      >Solo se llama a este método con valores de hora local. Si se llama al método con los resultados de la hora actual, se produce un comportamiento incorrecto.

   * Para buscar la hora actual, utilice `seek`.

1. Cuando su aplicación reciba la `onStatusChanged` evento de cambio de estado, busque la hora local guardada.
1. Proporcione los saltos de anuncio según se especifican en la interfaz de la política de anuncios.
1. Implemente un selector de políticas de publicidad personalizado ampliando el selector de políticas de publicidad predeterminado.
1. Proporcione las pausas publicitarias que deben presentarse al usuario implementando `selectAdBreaksToPlay`.

   Cuando el reproductor entra en el estado PREPARADO, todos los anuncios ya están resueltos, por lo que la variable `AdPolicyInfo.adBreakTimelineItem` contiene todas las pausas publicitarias anteriores a la posición horaria local. La aplicación puede decidir reproducir una pausa publicitaria pre-roll y reanudarla a la hora local especificada, reproducir una pausa publicitaria mid-roll y reanudarla a la hora local especificada o reproducir ninguna pausa publicitaria.
