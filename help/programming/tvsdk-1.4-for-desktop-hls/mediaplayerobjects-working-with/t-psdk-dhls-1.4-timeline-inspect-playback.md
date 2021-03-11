---
description: Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.
title: Inspect de la cronología de reproducción
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Inspect de la cronología de reproducción{#inspect-the-playback-timeline}

Puede obtener una descripción de la línea de tiempo asociada con el elemento seleccionado que está reproduciendo TVSDK. Esto resulta muy útil cuando la aplicación muestra un control de barra de desplazamiento personalizado en el que se identifican las secciones de contenido que se corresponden con el contenido de la publicidad.

A continuación se muestra un ejemplo de implementación, tal como se ve en la siguiente captura de pantalla.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acceda al objeto `Timeline` en `MediaPlayer` utilizando el método `get`.

   La clase `Timeline` encapsula la información relacionada con el contenido de la cronología asociada con el elemento de medios que está cargado actualmente por la instancia `MediaPlayer`. La clase `Timeline` proporciona acceso a una vista de solo lectura de la cronología subyacente. La clase `Timeline` proporciona un método de captador para obtener todos los objetos `TimelineMarker` colocados.

1. Repita la lista de `TimelineMarkers` y utilice la información devuelta para implementar la cronología.

       Un objeto &quot;TimelineMarker&quot; contiene dos fragmentos de información:
   
   * Posición del marcador en la cronología (en milisegundos)
   * Duración del marcador en la cronología (en milisegundos)

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

