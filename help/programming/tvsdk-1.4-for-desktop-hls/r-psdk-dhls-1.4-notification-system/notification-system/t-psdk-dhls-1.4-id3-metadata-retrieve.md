---
description: Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. detecta etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y envía un evento. La aplicación puede extraer datos de la etiqueta.
title: Etiquetas ID3
exl-id: 1934516e-729b-476a-a19d-677bf2eb922a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Etiquetas ID3{#id-tags}

Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. detecta etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y envía un evento. La aplicación puede extraer datos de la etiqueta.

>[!IMPORTANT]
>
>TVSDK reconoce metadatos ID3 (versión 2.3.0 o 2.4.0) en flujos de audio (AAC) y vídeo (H.264), en cualquiera de sus posibles codificaciones (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora las etiquetas ID3 que no están en una de las versiones o formatos reconocidos. La codificación no especificada se trata como UTF8.

Cuando TVSDK detecta metadatos de ID3, emite una notificación con los siguientes datos:

* InfoCode = 303007
* TIPO = ID3
* NAME = no presente
* ID = 0

1. Implementación de un detector de eventos para `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` y regístrela en el `MediaPlayer` objeto.

   TVSDK llama a este oyente cuando detecta metadatos de ID3.

   >[!NOTE]
   >
   >Las indicaciones de anuncio personalizadas utilizan lo mismo `onTimedMetadata` para indicar la detección de una etiqueta nueva. Esto no debería causar ninguna confusión, ya que las señales de publicidad personalizadas se detectan en el nivel de manifiesto y las etiquetas ID3 están incrustadas en la secuencia. Para obtener más información, consulte custom-tags-configure .

1. Recupere los metadatos.

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   ```
