---
description: Para recibir notificaciones sobre actualizaciones de la cronología, registre los oyentes de eventos correspondientes.
title: Agregar detectores para TimelineUpdatedEvent
exl-id: 7b55beb5-fd84-4144-8d02-bbd998f99e3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
