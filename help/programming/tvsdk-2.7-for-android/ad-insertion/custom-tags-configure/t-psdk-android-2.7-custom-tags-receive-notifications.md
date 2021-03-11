---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, debe implementar los oyentes de eventos adecuados.
title: Agregar oyentes para notificaciones de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Agregar oyentes para notificaciones de metadatos temporizadas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, debe implementar los oyentes de eventos adecuados.

Puede monitorizar los metadatos temporizados escuchando `onTimedMetadata`, que notifica a la aplicación de la actividad relacionada. Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo objeto `TimedMetadata` y envía este evento. El objeto contiene el nombre de la etiqueta a la que se ha suscrito, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

1. Escuche los eventos.

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

Los metadatos ID3 utilizan el mismo `onTimedMetadata` oyente para indicar la presencia de una etiqueta ID3. Sin embargo, esto no debe causar ninguna confusión, ya que puede utilizar la propiedad `TimedMetadata` `type` para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [ID3 tags](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md).