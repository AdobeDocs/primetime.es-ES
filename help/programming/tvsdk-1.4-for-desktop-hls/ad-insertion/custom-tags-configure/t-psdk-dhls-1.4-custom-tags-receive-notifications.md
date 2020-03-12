---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, registre los oyentes de eventos correspondientes.
seo-description: Para recibir notificaciones sobre etiquetas en el manifiesto, registre los oyentes de eventos correspondientes.
seo-title: Adición de oyentes para notificaciones de metadatos temporizados
title: Adición de oyentes para notificaciones de metadatos temporizados
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Adición de oyentes para notificaciones de metadatos temporizados{#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, registre los oyentes de eventos correspondientes.

Puede supervisar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`:: La lista inicial de `TimedMetadata` objetos está disponible después de crear la `MediaPlayerItem` .

   Este evento notifica a la aplicación cuando esto sucede.

* `MediaPlayerItemEvent.ITEM_UPDATED`:: En el caso de flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, es posible que aparezcan etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden agregar `TimedMetadata` objetos adicionales a la `MediaPlayerItem.timedMetadata` propiedad.

   Este evento notifica a la aplicación cuando esto sucede.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:: Cada vez que se crea un nuevo `TimedMetadata` objeto, MediaPlayer distribuye este evento.

   Este suceso no se distribuye para el `TimedMetadata` objeto creado durante la fase de inicialización.

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

1. Registre los oyentes de eventos.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

Los metadatos ID3 se envían a través de la misma `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Sin embargo, esto no debe causar ninguna confusión, ya que puede utilizar la propiedad de un objeto TimedMetadata para diferenciar entre TAG e ID3. `type` Para obtener más información sobre las etiquetas ID3, consulte Etiquetas [ID3](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).