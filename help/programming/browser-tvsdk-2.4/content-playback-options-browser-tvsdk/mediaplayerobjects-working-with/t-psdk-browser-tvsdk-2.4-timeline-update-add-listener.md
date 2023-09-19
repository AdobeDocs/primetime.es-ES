---
description: Para recibir notificaciones sobre actualizaciones de la cronología, registre los oyentes de eventos correspondientes.
title: Agregar detectores para TimelineUpdatedEvent
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Agregar detectores para TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Para recibir notificaciones sobre actualizaciones de la cronología, registre los oyentes de eventos correspondientes.

Cada vez que se actualiza la cronología, la variable `MediaPlayer` envíos `AdobePSDK.TimelineEvent` con tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. Implemente los oyentes adecuados.

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. Registre los oyentes de eventos.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```
