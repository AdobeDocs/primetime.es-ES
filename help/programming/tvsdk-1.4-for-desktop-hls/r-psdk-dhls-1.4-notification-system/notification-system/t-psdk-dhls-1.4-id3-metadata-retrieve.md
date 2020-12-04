---
description: Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y distribuye un evento. La aplicación puede extraer datos de la etiqueta .
seo-description: Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y distribuye un evento. La aplicación puede extraer datos de la etiqueta .
seo-title: Etiquetas ID3
title: Etiquetas ID3
uuid: 5c016260-5ced-480e-897a-11ffe7f34441
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Etiquetas ID3{#id-tags}

Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y distribuye un evento. La aplicación puede extraer datos de la etiqueta .

>[!IMPORTANT]
>
>TVSDK reconoce metadatos ID3 (versión 2.3.0 o 2.4.0) en flujos de audio (AAC) y vídeo (H.264), en cualquiera de sus posibles codificaciones (ASCII, UTF8, UTF16-BE o UTF16-LE). Omite las etiquetas ID3 que no están en una de las versiones o formatos reconocidos. La codificación no especificada se trata como UTF8.

Cuando TVSDK detecta metadatos ID3, emite una notificación con los siguientes datos:

* InfoCode = 303007
* TYPE = ID3
* NAME = no está presente
* ID = 0

1. Implemente un detector de evento para `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` y regístrelo con el objeto `MediaPlayer`.

   TVSDK llama a este detector cuando detecta metadatos ID3.

   >[!NOTE]
   >
   >Las señales de publicidad personalizadas utilizan el mismo evento `onTimedMetadata` para indicar la detección de una nueva etiqueta. Esto no debe causar ninguna confusión, ya que las señales de publicidad personalizadas se detectan en el nivel de manifiesto y las etiquetas ID3 se incrustan en el flujo. Para obtener más información, consulte custom-tags-configure .

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

