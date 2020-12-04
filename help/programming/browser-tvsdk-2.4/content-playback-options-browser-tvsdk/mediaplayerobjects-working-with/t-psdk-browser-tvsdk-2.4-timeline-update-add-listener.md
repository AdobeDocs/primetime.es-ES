---
description: Para recibir notificaciones sobre actualizaciones de línea de tiempo, registre los oyentes de evento correspondientes.
seo-description: Para recibir notificaciones sobre actualizaciones de línea de tiempo, registre los oyentes de evento correspondientes.
seo-title: Añadir oyentes para TimelineUpdatedEvent
title: Añadir oyentes para TimelineUpdatedEvent
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Añadir oyentes para TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Para recibir notificaciones sobre actualizaciones de línea de tiempo, registre los oyentes de evento correspondientes.

Cada vez que se actualiza la línea de tiempo, `MediaPlayer` distribuye `AdobePSDK.TimelineEvent` con el tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
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

1. Registre los oyentes de evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

