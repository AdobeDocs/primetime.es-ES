---
description: Puede anular el comportamiento predeterminado de la forma en que TVSDK busca por encima de las publicidades al utilizar marcadores de publicidad personalizados.
seo-description: Puede anular el comportamiento predeterminado de la forma en que TVSDK busca por encima de las publicidades al utilizar marcadores de publicidad personalizados.
seo-title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
uuid: cf973caf-be29-46ce-bfa4-651e7653f8d4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede anular el comportamiento predeterminado de la forma en que TVSDK busca por encima de las publicidades al utilizar marcadores de publicidad personalizados.

De forma predeterminada, cuando un usuario busca en secciones de publicidad anteriores o en secciones de publicidad que resultan de la colocación de marcadores de publicidad personalizados, TVSDK omite las publicidades. Esto puede diferir del comportamiento de reproducción actual de los saltos de publicidad estándar.

Puede indicar a TVSDK que cambie la posición del cursor de reproducción al principio de la última publicidad personalizada omitida cuando el usuario busque más anuncios personalizados.

1. Configure una instancia de metadatos con la `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumeración establecida en el valor de cadena &quot;true&quot; (no como booleano `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Cree y configure una `MediaResource` instancia, pasando las opciones de configuración adicionales a `TimeRangeCollection.toMetadata`. Este método recibe opciones de configuración adicionales mediante otra estructura de metadatos genérica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```

