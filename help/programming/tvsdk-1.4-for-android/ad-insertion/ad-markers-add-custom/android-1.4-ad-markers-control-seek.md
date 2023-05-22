---
description: Puede anular el comportamiento predeterminado para la forma en que TVSDK busca sobre los anuncios al utilizar marcadores de anuncio personalizados.
title: Controle el comportamiento de reproducción para buscar sobre los marcadores de publicidad personalizados
exl-id: 83faa5a4-4416-499e-8cf2-d016cd9a379d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Controle el comportamiento de reproducción para buscar sobre los marcadores de publicidad personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede anular el comportamiento predeterminado para la forma en que TVSDK busca sobre los anuncios al utilizar marcadores de anuncio personalizados.

De forma predeterminada, cuando un usuario busca dentro o fuera de las secciones de publicidad que resultan de la colocación de marcadores de publicidad personalizados, TVSDK omite los anuncios. Esto puede diferir del comportamiento de reproducción actual para las pausas publicitarias estándar.

Puede indicar a TVSDK que cambie la posición del cabezal de reproducción al principio del anuncio personalizado omitido más recientemente cuando el usuario busque más allá de uno o más anuncios personalizados.

1. Configuración de una instancia de metadatos con `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumeración establecida en el valor de cadena &quot;true&quot; (no como Boolean) `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Creación y configuración de un `MediaResource` , pasando las opciones de configuración adicionales a `TimeRangeCollection.toMetadata`. Este método recibe opciones de configuración adicionales a través de otra estructura de metadatos genérica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```
