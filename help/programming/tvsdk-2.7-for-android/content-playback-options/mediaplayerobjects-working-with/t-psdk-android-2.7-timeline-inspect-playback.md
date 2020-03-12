---
description: Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.
seo-description: Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.
seo-title: Inspeccionar la línea de tiempo de reproducción
title: Inspeccionar la línea de tiempo de reproducción
uuid: d0fe7926-9b9a-4203-a1c7-e57ba25b882e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Inspeccionar la línea de tiempo de reproducción {#inspect-the-playback-timeline}

Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.

A continuación se muestra un ejemplo de implementación, como se muestra en la siguiente captura de pantalla.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acceda al `Timeline` objeto del `MediaPlayer` mediante el `getTimeline()` método .

   La `Timeline` clase encapsula la información relacionada con el contenido de la línea de tiempo asociada al elemento de medios que está cargado actualmente por la `MediaPlayer` instancia. La `Timeline` clase proporciona acceso a una vista de sólo lectura de la línea de tiempo subyacente. La `Timeline` clase proporciona un método getter que proporciona un iterador a través de una lista de `TimelineMarker` objetos.

1. Repita la lista de la información devuelta `TimelineMarkers` y utilícela para implementar la línea de tiempo.

       Un objeto &quot;TimelineMarker&quot; contiene dos partes de información:
   
   * Posición del marcador en la línea de tiempo (en milisegundos)
   * Duración del marcador en la línea de tiempo (en milisegundos)

1. Escuche el `MediaPlayerEvent.TIMELINE_UPDATED` evento en la `MediaPlayer` instancia e implemente la `TimelineUpdatedEventListener.onTimelineUpdated()` llamada de retorno.

   El `Timeline` objeto puede informar a la aplicación de los cambios que podrían producirse en la línea de tiempo de reproducción llamando al `OnTimelineUpdated` detector.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
 
// Iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
 
while (iterator.hasNext()) { 
    TimelineMarker marker = iterator.next(); 
    // the start position of the marker 
    long startPos = marker.getTime(); 
    // the duration of the marker 
    long duration = marker.getDuration(); 
}
```
