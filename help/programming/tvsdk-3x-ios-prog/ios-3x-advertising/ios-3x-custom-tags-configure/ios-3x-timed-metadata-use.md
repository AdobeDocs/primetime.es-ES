---
description: Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con el tiempo de inicio.
seo-description: Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con el tiempo de inicio.
seo-title: Uso de metadatos temporizados
title: Uso de metadatos temporizados
uuid: 1531780f-2502-4235-818c-6c0a6bf3d348
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---


# Usar metadatos temporizados {#use-timed-metadata}

Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con el tiempo de inicio.

Para utilizar estos objetos guardados `PTTimedMetadata` durante la reproducción, utilice el diccionario guardado de [Almacenar objetos de metadatos temporizados a medida que se distribuyen](../../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-timed-metadata-store.md).

1. Extraiga y actualice el tiempo de reproducción actual desde esta notificación y busque todos los objetos `PTTimedMetadata` con tiempos de inicio que coincidan con el tiempo de reproducción actual.

   Puede utilizar estos objetos para completar varias acciones.

   Por ejemplo:

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       CMTimeRange seekableRange = self.player.seekableRange; 
       if (CMTIMERANGE_IS_VALID(seekableRange)) 
       { 
           int currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
           NSArray *allKeys = timedMetadataCollection ? [timedMetadataCollection allKeys] : [NSArray array]; 
           NSMutableArray *timedMetadatasToDelete = [[[NSMutableArray alloc] init] autorelease]; 
           int count = [allKeys count]; 
   
           for (int i=count - 1; i > -1; i--) 
           { 
              NSNumber *currTimedMetadataTime = allKeys[i]; 
              if ([currTimedMetadataTime integerValue] == currentTime) 
              { 
               /* 
                   Use the timed metadata here and remove it from the collection. 
               */ 
                NSLog (@"IN PLAYBACK TIME %i TO EXECUTE TIMEDMETADATA %@ scheduled at time %f",currentTime,currTimedMetadata.name,CMTimeGetSeconds(currTimedMetadata.time)); 
   
               PTTimedMetadata *currTimedMetadata = [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
               [timedMetadatasToDelete addObject:currTimedMetadataTime]; 
              } 
           } 
   
           for (int i=0; i<[timedMetadatasToDelete count]; i++) 
           { 
               NSNumber *timedMetadataToDelete = timedMetadatasToDelete[i]; 
               [timedMetadataCollection removeObjectForKey:timedMetadataToDelete]; 
           } 
       } 
   }
   ```

1. Extraiga periódicamente instancias antiguas `PTTimedMetadata` de la lista para evitar que la memoria crezca continuamente.