---
description: Puede obtener una descripción de la cronología asociada con el elemento seleccionado actualmente y que TVSDK está reproduciendo. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que corresponden al contenido del anuncio.
title: Inspect la cronología de reproducción
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Inspect la cronología de reproducción{#inspect-the-playback-timeline}

Puede obtener una descripción de la cronología asociada con el elemento seleccionado actualmente y que TVSDK está reproduciendo. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que corresponden al contenido del anuncio.

A continuación, se muestra una implementación de ejemplo como se ve en la siguiente captura de pantalla.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. Acceda a la `Timeline` objeto en el `MediaPlayer` uso del `get` método.

   El `Timeline` encapsula la información relacionada con el contenido de la cronología asociada al elemento de medios que carga actualmente el objeto `MediaPlayer` ejemplo. El `Timeline` proporciona acceso a una vista de sólo lectura de la escala de tiempo subyacente. El `Timeline` proporciona un método de captador para obtener todas las `TimelineMarker` objetos.

1. Iterar por la lista de `TimelineMarkers` y utilice la información devuelta para implementar la cronología.

       Un objeto &quot;TimelineMarker&quot; contiene dos fragmentos de información:
   
   * Posición del marcador en la cronología (en milisegundos)
   * Duración del marcador en la escala de tiempo (en milisegundos)

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```
