---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, escuche AdobePSDK.TimedMetadataEvent.
title: Agregar oyentes para notificaciones de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Agregar oyentes para notificaciones de metadatos temporizados{#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, escuche AdobePSDK.TimedMetadataEvent.

Cuando se crea un nuevo objeto `TimedMetadata`, MediaPlayer envía `AdobePSDK.TimedMetadataEvent`.

1. Implemente los oyentes adecuados.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registre los oyentes del evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

Los metadatos ID3 se envían a través de la misma `Events.TimedMetadataEvent`. Puede utilizar la propiedad `timedMetadata.type` para distinguir entre TAG e ID3.

