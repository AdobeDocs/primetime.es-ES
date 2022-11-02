---
description: Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.
title: Inspect de la cronología de reproducción
exl-id: af373f1e-ed5b-40a9-a91e-9eb0e4a181de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect de la cronología de reproducción{#inspect-the-playback-timeline}

Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.

A continuación se muestra un ejemplo de implementación, tal como se ve en la siguiente captura de pantalla.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. Acceda a la `Timeline` en el `MediaPlayer` usando la variable `getTimeline` método.

   La variable `Timeline` encapsula la información relacionada con el contenido de la cronología asociada con el elemento multimedia que está cargado actualmente por el `MediaPlayer` instancia. La variable `Timeline` proporciona acceso a una vista de solo lectura de la línea de tiempo subyacente. La variable `Timeline` class proporciona un método de captador que proporciona un iterador a través de una lista de `TimelineMarker` objetos.

1. Iterar por la lista de `TimelineMarkers` y utilice la información devuelta para implementar su línea de tiempo.

       Un objeto &quot;TimelineMarker&quot; contiene dos fragmentos de información:
   
   * Posición del marcador en la cronología (en milisegundos)
   * Duración del marcador en la cronología (en milisegundos)

1. Implementar la interfaz de llamada de retorno de oyente `MediaPlayer.PlaybackEventListener.onTimelineUpdated` y regístrela en el `Timeline` objeto.

   La variable `Timeline` puede informar a la aplicación de los cambios que podrían producirse en la línea de tiempo de reproducción llamando a su `OnTimelineUpdated` listener.

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
