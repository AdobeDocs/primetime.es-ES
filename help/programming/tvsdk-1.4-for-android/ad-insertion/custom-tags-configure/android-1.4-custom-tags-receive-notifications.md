---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de eventos correspondientes.
title: Añadir oyentes para notificaciones de metadatos cronometradas
exl-id: febf354b-2a25-4108-abd9-6ff1e09cee39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Añadir oyentes para notificaciones de metadatos cronometradas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de eventos correspondientes.

Puede monitorizar los metadatos cronometrados si escucha los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `onTimedMetadata`: Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara una nueva `TimedMetadata` y distribuye este evento.

   El objeto contiene el nombre de la etiqueta a la que se ha suscrito, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

   Escuchar eventos.

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

Los metadatos ID3 utilizan el mismo detector onTimedMetadata para indicar la presencia de una etiqueta ID3. Sin embargo, esto no debería causar ninguna confusión, ya que puede utilizar un `TimedMetadata` del objeto `type` para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte [Etiquetas ID3](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
