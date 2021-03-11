---
description: Para recibir notificaciones sobre actualizaciones de la cronología, registre los oyentes de eventos correspondientes.
title: Agregar oyentes para TimelineUpdatedEvent
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Agregar oyentes para TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Para recibir notificaciones sobre actualizaciones de la cronología, registre los oyentes de eventos correspondientes.

Cada vez que se actualiza la línea de tiempo, `MediaPlayer` envía `AdobePSDK.TimelineEvent` con el tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
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

1. Registre los oyentes del evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

