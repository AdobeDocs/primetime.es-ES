---
description: Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y envía un evento. La aplicación puede extraer datos de la etiqueta.
title: Etiquetas ID3
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Etiquetas ID3 {#id-tags}

Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y envía un evento. La aplicación puede extraer datos de la etiqueta.

>[!IMPORTANT]
>
>TVSDK reconoce metadatos ID3 (versión 2.3.0 o 2.4.0) en flujos de audio (AAC) y vídeo (H.264) en cualquiera de sus posibles codificaciones (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora las etiquetas ID3 que no están en una de las versiones o formatos reconocidos. La codificación no especificada se trata como UTF8.

Cuando TVSDK detecta metadatos de ID3, emite una notificación con los siguientes datos:

* TIPO = ID3
* NOMBRE = ID3

1. Implementación de un detector de eventos para `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` y regístrela en el `MediaPlayer` objeto.

   TVSDK llama a este oyente cuando detecta `ID3` metadatos.

   >[!TIP]
   >
   >Las indicaciones de anuncio personalizadas utilizan lo mismo `onTimedMetadata` para indicar la detección de una etiqueta nueva. Esto no debería causar ninguna confusión, ya que las señales de publicidad personalizadas se detectan en el nivel de manifiesto y las etiquetas ID3 están incrustadas en la secuencia. Para obtener más información, consulte [Etiquetas personalizadas](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


1. Recupere los metadatos.

   ```java
   @Override 
    public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```
