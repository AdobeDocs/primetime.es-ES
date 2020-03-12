---
description: Para recibir notificaciones sobre las actualizaciones de la línea de tiempo, registre los detectores de eventos correspondientes.
seo-description: Para recibir notificaciones sobre las actualizaciones de la línea de tiempo, registre los detectores de eventos correspondientes.
seo-title: Agregar oyentes para TimelineUpdatedEvent
title: Agregar oyentes para TimelineUpdatedEvent
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Agregar oyentes para TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Para recibir notificaciones sobre las actualizaciones de la línea de tiempo, registre los detectores de eventos correspondientes.

Cada vez que se actualiza la línea de tiempo, el `MediaPlayer` se distribuye `AdobePSDK.TimelineEvent` con el tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
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

