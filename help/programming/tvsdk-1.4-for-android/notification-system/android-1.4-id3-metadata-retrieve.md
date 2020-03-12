---
description: Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK detecta etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y distribuye un evento. La aplicación puede extraer datos de la etiqueta .
seo-description: Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK detecta etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y distribuye un evento. La aplicación puede extraer datos de la etiqueta .
seo-title: Etiquetas ID3
title: Etiquetas ID3
uuid: 5e5c5f89-7653-47c1-b9c1-6b9b9b1f8d73
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Etiquetas ID3 {#id-tags}

Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK detecta etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y distribuye un evento. La aplicación puede extraer datos de la etiqueta .

>[!IMPORTANT]
>
>TVSDK reconoce metadatos ID3 (versión 2.3.0 o 2.4.0) en flujos de audio (AAC) y vídeo (H.264), en cualquiera de sus posibles codificaciones (ASCII, UTF8, UTF16-BE o UTF16-LE). Omite las etiquetas ID3 que no están en una de las versiones o formatos reconocidos. La codificación no especificada se trata como UTF8.

Cuando TVSDK detecta metadatos ID3, emite una notificación con los siguientes datos:

* InfoCode = 303007
* TYPE = ID3
* NAME = no está presente
* ID = 0

1. Implemente un detector de eventos para `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` y regístrelo con el `MediaPlayer` objeto.

   TVSDK llama a este detector cuando detecta metadatos ID3.

   >[!NOTE]
   >
   >Las señales de publicidad personalizadas utilizan el mismo `onTimedMetadata` evento para indicar la detección de una etiqueta nueva. Esto no debe causar ninguna confusión, ya que las señales de publicidad personalizadas se detectan en el nivel de manifiesto y las etiquetas ID3 se incrustan en el flujo. Para obtener más información, consulte custom-tags-configure .

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
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```

