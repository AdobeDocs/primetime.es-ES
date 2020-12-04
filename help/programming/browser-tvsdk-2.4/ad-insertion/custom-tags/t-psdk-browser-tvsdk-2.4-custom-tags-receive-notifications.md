---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, escuche AdobePSDK.TimedMetadataEvent.
seo-description: Para recibir notificaciones sobre etiquetas en el manifiesto, escuche AdobePSDK.TimedMetadataEvent.
seo-title: Añadir oyentes para notificaciones de metadatos temporizados
title: Añadir oyentes para notificaciones de metadatos temporizados
uuid: c82c5549-0ab6-4343-a766-5176e784d4cb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Añadir oyentes para notificaciones de metadatos temporizados{#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, escuche AdobePSDK.TimedMetadataEvent.

Cuando se crea un nuevo objeto `TimedMetadata`, MediaPlayer distribuye `AdobePSDK.TimedMetadataEvent`.

1. Implemente los oyentes adecuados.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registre los oyentes de evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

Los metadatos ID3 se envían a través de la misma `Events.TimedMetadataEvent`. Puede utilizar la propiedad `timedMetadata.type` para distinguir entre TAG e ID3.

