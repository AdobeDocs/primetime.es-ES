---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, registre los oyentes de eventos correspondientes.
title: Añadir oyentes para notificaciones de metadatos cronometradas
exl-id: 1df8a4fc-8368-4a80-8f8b-00c1207e6602
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Añadir oyentes para notificaciones de metadatos cronometradas{#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, registre los oyentes de eventos correspondientes.

Puede monitorizar los metadatos cronometrados si escucha los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: la lista inicial de `TimedMetadata` está disponible después de que `MediaPlayerItem` se ha creado.

   Este evento notifica a la aplicación cuando esto sucede.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para emisiones lineales/en directo en las que el manifiesto/lista de reproducción se actualiza periódicamente, es posible que aparezcan etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que resulta `TimedMetadata` objetos que se pueden añadir a `MediaPlayerItem.timedMetadata` propiedad.

   Este evento notifica a la aplicación cuando esto sucede.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Cada vez que se crea un nuevo `TimedMetadata` se crea, este evento es distribuido por MediaPlayer.

   Este evento no se envía para `TimedMetadata` objeto creado durante la fase de inicialización.

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

Los metadatos de ID3 se envían mediante el mismo `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Sin embargo, esto no debería causar ninguna confusión, ya que puede utilizar el de un objeto TimedMetadata `type` para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [Etiquetas ID3](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
