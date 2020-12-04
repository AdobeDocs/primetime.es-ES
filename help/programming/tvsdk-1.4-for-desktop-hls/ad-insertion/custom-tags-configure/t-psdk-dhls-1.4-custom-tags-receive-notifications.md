---
description: Para recibir notificaciones sobre las etiquetas del manifiesto, registre los oyentes de evento correspondientes.
seo-description: Para recibir notificaciones sobre las etiquetas del manifiesto, registre los oyentes de evento correspondientes.
seo-title: Añadir oyentes para notificaciones de metadatos temporizadas
title: Añadir oyentes para notificaciones de metadatos temporizadas
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Añadir oyentes para notificaciones de metadatos temporizadas{#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre las etiquetas del manifiesto, registre los oyentes de evento correspondientes.

Puede supervisar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`:: La lista inicial de  `TimedMetadata` los objetos está disponible después de  `MediaPlayerItem` crearla.

   Este evento notifica a la aplicación cuando esto sucede.

* `MediaPlayerItemEvent.ITEM_UPDATED`:: En el caso de flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, es posible que aparezcan etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden añadir  `TimedMetadata` objetos adicionales a la  `MediaPlayerItem.timedMetadata` propiedad.

   Este evento notifica a la aplicación cuando esto sucede.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:: Cada vez que se crea un nuevo  `TimedMetadata` objeto, MediaPlayer distribuye este evento.

   Este evento no se distribuye para el objeto `TimedMetadata` creado durante la fase de inicialización.

1. Implemente los oyentes adecuados.

   ```
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onItemUpdated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onTimedMetadataAvailable(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       // process timed metadata 
   }
   ```

1. Registre los oyentes de evento.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

Los metadatos ID3 se envían a través de la misma `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Sin embargo, esto no debe causar ninguna confusión, ya que puede utilizar la propiedad `type` de un objeto TimedMetadata para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [etiquetas ID3](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).