---
description: Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.
seo-description: Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.
seo-title: Inspeccionar la línea de tiempo de reproducción
title: Inspeccionar la línea de tiempo de reproducción
uuid: b5ede131-1037-449b-bc3f-a066fdc92fc5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Inspeccionar la línea de tiempo de reproducción{#inspect-the-playback-timeline}

Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.

A continuación se muestra un ejemplo de implementación, como se muestra en la siguiente captura de pantalla.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acceda al `Timeline` objeto del `MediaPlayer` mediante el `getTimeline` método .

   La `Timeline` clase encapsula la información relacionada con el contenido de la línea de tiempo asociada al elemento de medios que está cargado actualmente por la `MediaPlayer` instancia. La `Timeline` clase proporciona acceso a una vista de sólo lectura de la línea de tiempo subyacente. La `Timeline` clase proporciona un método getter que proporciona un iterador a través de una lista de `TimelineMarker` objetos.

1. Repita la lista de la información devuelta `TimelineMarkers` y utilícela para implementar la línea de tiempo.

       Un objeto &quot;TimelineMarker&quot; contiene dos partes de información:
   
   * Posición del marcador en la línea de tiempo (en milisegundos)
   * Duración del marcador en la línea de tiempo (en milisegundos)

1. Implemente la interfaz de llamada de retorno de oyente `MediaPlayer.PlaybackEventListener.onTimelineUpdated` y regístrela con el `Timeline` objeto.

   El `Timeline` objeto puede informar a la aplicación de los cambios que podrían producirse en la línea de tiempo de reproducción llamando al `OnTimelineUpdated` detector.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```

