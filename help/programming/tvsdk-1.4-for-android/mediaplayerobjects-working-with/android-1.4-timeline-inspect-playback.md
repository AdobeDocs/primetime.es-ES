---
description: Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.
title: Inspect de la cronología de reproducción
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Inspect de la cronología de reproducción{#inspect-the-playback-timeline}

Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.

A continuación se muestra un ejemplo de implementación, tal como se ve en la siguiente captura de pantalla.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acceda al objeto `Timeline` en `MediaPlayer` utilizando el método `getTimeline`.

   La clase `Timeline` encapsula la información relacionada con el contenido de la cronología asociada con el elemento de medios que está cargado actualmente por la instancia `MediaPlayer`. La clase `Timeline` proporciona acceso a una vista de solo lectura de la cronología subyacente. La clase `Timeline` proporciona un método de captador que proporciona un iterador a través de una lista de objetos `TimelineMarker`.

1. Repita la lista de `TimelineMarkers` y utilice la información devuelta para implementar la cronología.

       Un objeto &quot;TimelineMarker&quot; contiene dos fragmentos de información:
   
   * Posición del marcador en la cronología (en milisegundos)
   * Duración del marcador en la cronología (en milisegundos)

1. Implemente la interfaz de llamada de retorno del oyente `MediaPlayer.PlaybackEventListener.onTimelineUpdated` y regístrela con el objeto `Timeline`.

   El objeto `Timeline` puede informar a la aplicación de los cambios que podrían producirse en la cronología de reproducción llamando al oyente `OnTimelineUpdated`.

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

