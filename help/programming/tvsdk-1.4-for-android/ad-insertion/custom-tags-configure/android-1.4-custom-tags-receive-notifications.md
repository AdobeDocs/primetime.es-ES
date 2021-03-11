---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de eventos correspondientes.
title: Agregar oyentes para notificaciones de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Agregar oyentes para notificaciones de metadatos temporizadas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de eventos correspondientes.

Puede monitorizar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación de la actividad relacionada:

* `onTimedMetadata`: Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo  `TimedMetadata` objeto y envía este evento.

   El objeto contiene el nombre de la etiqueta a la que se ha suscrito, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

   Escuche los eventos.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener =  
     new TimedMetadataEventListener() { 
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
           } else if (_mediaPlayer.getPlaybackRange() !=  
                      null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

Los metadatos ID3 utilizan el mismo detector onTimedMetadata para indicar la presencia de una etiqueta ID3. Sin embargo, esto no debe causar ninguna confusión, ya que puede utilizar la propiedad `TimedMetadata` del objeto `type` para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [ID3 tags](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
