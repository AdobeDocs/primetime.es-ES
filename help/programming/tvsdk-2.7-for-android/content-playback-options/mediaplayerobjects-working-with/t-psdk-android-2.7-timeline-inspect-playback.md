---
description: Puede obtener una descripción de la cronología asociada con el elemento seleccionado actualmente y que TVSDK está reproduciendo. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que corresponden al contenido del anuncio.
title: Inspect la cronología de reproducción
exl-id: 2a12fe28-9a8a-45b7-af05-87c17dd25302
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect la cronología de reproducción {#inspect-the-playback-timeline}

Puede obtener una descripción de la cronología asociada con el elemento seleccionado actualmente y que TVSDK está reproduciendo. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que corresponden al contenido del anuncio.

A continuación, se muestra una implementación de ejemplo como se ve en la siguiente captura de pantalla.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. Acceda a la `Timeline` objeto en el `MediaPlayer` uso del `getTimeline()` método.

   El `Timeline` encapsula la información relacionada con el contenido de la cronología asociada al elemento de medios que carga actualmente el objeto `MediaPlayer` ejemplo. El `Timeline` proporciona acceso a una vista de sólo lectura de la escala de tiempo subyacente. El `Timeline` proporciona un método de captador que proporciona un iterador a través de una lista de `TimelineMarker` objetos.

1. Iterar por la lista de `TimelineMarkers` y utilice la información devuelta para implementar la cronología.

       Un objeto &quot;TimelineMarker&quot; contiene dos fragmentos de información:
   
   * Posición del marcador en la cronología (en milisegundos)
   * Duración del marcador en la escala de tiempo (en milisegundos)

1. Escuche el `MediaPlayerEvent.TIMELINE_UPDATED` evento en el `MediaPlayer` e implemente la variable `TimelineUpdatedEventListener.onTimelineUpdated()` devolución de llamada.

   El `Timeline` puede informar a la aplicación de los cambios que pueden producirse en la cronología de reproducción llamando a su `OnTimelineUpdated` oyente.

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
