---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, debe implementar los detectores de eventos adecuados.
title: Añadir oyentes para notificaciones de metadatos cronometradas
exl-id: e38f2a25-3379-4132-a8de-6703dc564ed4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Añadir oyentes para notificaciones de metadatos cronometradas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, debe implementar los detectores de eventos adecuados.

Puede monitorizar los metadatos cronometrados si escucha `onTimedMetadata`, que notifican a la aplicación de la actividad relacionada. Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara una nueva `TimedMetadata` y distribuye este evento. El objeto contiene el nombre de la etiqueta a la que se ha suscrito, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

1. Escuchar eventos.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
       @Override 
       public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
           TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
   
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.ID3)){ 
               Metadata metadata = timedMetadata.getMetadata(); 
               Set<String> keys = metadata.keySet(); 
               for (String key : keys) { 
                   String value = metadata.getValue(key); 
               } 
           } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

Los metadatos ID3 utilizan el mismo `onTimedMetadata` para indicar la presencia de una etiqueta ID3. Sin embargo, esto no debería causar ninguna confusión, ya que puede usar el complemento `TimedMetadata` `type` para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte  [Etiquetas ID3](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md).
