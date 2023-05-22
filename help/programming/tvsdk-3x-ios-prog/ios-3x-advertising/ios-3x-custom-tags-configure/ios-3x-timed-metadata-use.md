---
description: Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con el tiempo de inicio.
title: Usar metadatos cronometrados
exl-id: e41718e0-2b6c-4353-a365-2d84ad4ac815
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Usar metadatos cronometrados {#use-timed-metadata}

Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con el tiempo de inicio.

Para utilizar estos elementos guardados `PTTimedMetadata` durante la reproducción, utilice el diccionario guardado de [Almacenar objetos de metadatos cronometrados a medida que se envían](../../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-timed-metadata-store.md).

1. Extraiga y actualice el tiempo de reproducción actual de esta notificación y busque todos los `PTTimedMetadata` objetos con tiempos de inicio que coinciden con el tiempo de reproducción actual.

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

1. Vaciar periódicamente objetos antiguos `PTTimedMetadata` instancias de la lista para evitar que la memoria crezca continuamente.
