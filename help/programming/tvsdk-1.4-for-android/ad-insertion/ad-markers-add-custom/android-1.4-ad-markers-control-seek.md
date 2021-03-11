---
description: Puede anular el comportamiento predeterminado de cómo TVSDK busca por encima de los anuncios al usar marcadores de anuncios personalizados.
title: Controlar el comportamiento de reproducción para buscar en marcadores de anuncios personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Controlar el comportamiento de reproducción para buscar en marcadores de anuncios personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede anular el comportamiento predeterminado de cómo TVSDK busca por encima de los anuncios al usar marcadores de anuncios personalizados.

De forma predeterminada, cuando un usuario busca en secciones de anuncios anteriores o en secciones de anuncios anteriores resultantes de la colocación de marcadores de anuncios personalizados, TVSDK omite los anuncios. Esto puede diferir del comportamiento de reproducción actual de las pausas publicitarias estándar.

Puede indicar a TVSDK que vuelva a colocar el cursor de reproducción hasta el principio del anuncio personalizado que se haya omitido más recientemente cuando el usuario busque más anuncios personalizados.

1. Configure una instancia de metadatos con la enumeración `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` establecida en el valor de cadena &quot;true&quot; (no como booleano `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Cree y configure una instancia `MediaResource`, pasando las opciones de configuración adicionales a `TimeRangeCollection.toMetadata`. Este método recibe opciones de configuración adicionales a través de otra estructura de metadatos genérica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```

