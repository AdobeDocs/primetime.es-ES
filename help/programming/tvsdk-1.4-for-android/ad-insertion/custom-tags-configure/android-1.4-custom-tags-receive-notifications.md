---
description: Para recibir notificaciones sobre las etiquetas del manifiesto, implemente los oyentes de evento correspondientes.
seo-description: Para recibir notificaciones sobre las etiquetas del manifiesto, implemente los oyentes de evento correspondientes.
seo-title: Añadir oyentes para notificaciones de metadatos temporizadas
title: Añadir oyentes para notificaciones de metadatos temporizadas
uuid: cd7a5936-d63a-4711-ac16-2d79bac099a3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Añadir oyentes para notificaciones de metadatos temporizadas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre las etiquetas del manifiesto, implemente los oyentes de evento correspondientes.

Puede supervisar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `onTimedMetadata`:: Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo  `TimedMetadata` objeto y distribuye este evento.

   El objeto contiene el nombre de la etiqueta a la que se suscribió, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

   Escucha eventos.

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

Los metadatos ID3 utilizan el mismo detector onTimedMetadata para indicar la presencia de una etiqueta ID3. Sin embargo, esto no debe causar ninguna confusión, ya que puede utilizar la propiedad `TimedMetadata` del objeto `type` para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [etiquetas ID3](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
