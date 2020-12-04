---
description: Para recibir notificaciones sobre las etiquetas del manifiesto, debe implementar los oyentes de evento adecuados.
seo-description: Para recibir notificaciones sobre las etiquetas del manifiesto, debe implementar los oyentes de evento adecuados.
seo-title: Añadir oyentes para notificaciones de metadatos temporizadas
title: Añadir oyentes para notificaciones de metadatos temporizadas
uuid: 336882e7-e2d8-49b8-a23d-f236c7e6a594
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Añadir oyentes para notificaciones de metadatos temporizadas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre las etiquetas del manifiesto, debe implementar los oyentes de evento adecuados.

Puede supervisar los metadatos temporizados escuchando `onTimedMetadata`, que notifican a la aplicación la actividad relacionada. Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo objeto `TimedMetadata` y distribuye este evento. El objeto contiene el nombre de la etiqueta a la que se suscribió, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

1. Escucha eventos.

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

Los metadatos ID3 utilizan el mismo detector `onTimedMetadata` para indicar la presencia de una etiqueta ID3. Sin embargo, esto no debe causar ninguna confusión, ya que puede utilizar la propiedad `TimedMetadata` `type` para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [etiquetas ID3](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md).