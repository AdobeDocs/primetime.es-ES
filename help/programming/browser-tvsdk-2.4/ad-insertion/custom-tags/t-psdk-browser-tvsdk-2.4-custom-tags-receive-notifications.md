---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, escuche AdobePSDK.TimedMetadataEvent.
title: Agregar agentes de escucha para notificaciones de metadatos cronometrados
exl-id: eea2505f-595c-4bbe-9b68-ae395943c888
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Agregar agentes de escucha para notificaciones de metadatos cronometrados{#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, escuche AdobePSDK.TimedMetadataEvent.

Al crear un nuevo `TimedMetadata` Cuando se crea el objeto, MediaPlayer distribuye `AdobePSDK.TimedMetadataEvent`.

1. Implemente los oyentes adecuados.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registre los oyentes de eventos.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

Los metadatos de ID3 se envían mediante el mismo `Events.TimedMetadataEvent`. Puede usar el complemento `timedMetadata.type` para distinguir entre TAG e ID3.
