---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, registre los oyentes de eventos correspondientes.
title: Agregar oyentes para notificaciones de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Agregar oyentes para notificaciones de metadatos temporizadas{#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, registre los oyentes de eventos correspondientes.

Puede monitorizar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación de la actividad relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: La lista inicial de  `TimedMetadata` objetos está disponible después de  `MediaPlayerItem` crearla.

   Este evento notifica a la aplicación cuando esto sucede.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, pueden aparecer etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden agregar  `TimedMetadata` objetos adicionales a la  `MediaPlayerItem.timedMetadata` propiedad.

   Este evento notifica a la aplicación cuando esto sucede.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Cada vez que se crea un nuevo  `TimedMetadata` objeto, MediaPlayer envía este evento.

   Este evento no se envía para el objeto `TimedMetadata` creado durante la fase de inicialización.

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

1. Registre los oyentes del evento.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

Los metadatos de ID3 se envían a través de la misma `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Sin embargo, esto no debe causar ninguna confusión, ya que puede utilizar la propiedad `type` de un objeto TimedMetadata para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [ID3 tags](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).