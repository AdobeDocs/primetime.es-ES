---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, debe implementar los detectores de eventos adecuados.
seo-description: Para recibir notificaciones sobre etiquetas en el manifiesto, debe implementar los detectores de eventos adecuados.
seo-title: Adición de oyentes para notificaciones de metadatos temporizados
title: Adición de oyentes para notificaciones de metadatos temporizados
uuid: bb996b4a-282e-4321-a9e9-513f0df45b70
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Adición de oyentes para notificaciones de metadatos temporizados {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, debe implementar los detectores de eventos adecuados.

Puede supervisar los metadatos temporizados mediante la escucha de `onTimedMetadata`, que notifican a la aplicación la actividad relacionada. Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo `TimedMetadata` objeto y distribuye este evento. El objeto contiene el nombre de la etiqueta a la que se suscribió, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

Escuche los eventos.

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

Los metadatos ID3 utilizan el mismo `onTimedMetadata` detector para indicar la presencia de una etiqueta ID3. Sin embargo, esto no debería causar ninguna confusión, ya que puede utilizar la `TimedMetadata` `type` propiedad para diferenciar entre TAG e ID3. Para obtener más información sobre las etiquetas ID3, consulte Etiquetas [ID3](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md).