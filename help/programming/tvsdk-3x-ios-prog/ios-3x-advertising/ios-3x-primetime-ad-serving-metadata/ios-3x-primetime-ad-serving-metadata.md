---
description: TVSDK admite la resolución e inserción de anuncios para flujos VOD y en directo/lineal.
title: Metadatos del servidor de publicidad de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Información general {#primetime-ad-server-metadata-overview}

TVSDK admite la resolución e inserción de anuncios para flujos VOD y en directo/lineal.

## Requisito previo

Antes de incluir publicidad en el contenido de vídeo, proporcione la siguiente información de metadatos:

* Un `mediaID`, que identifica el contenido específico que se va a reproducir.
* Su `zoneID`, que identifica a su empresa o sitio web.
* El dominio del servidor de publicidad, que especifica el dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

## Configurar metadatos del servidor de publicidad de Primetime {#section_86C4A3B2DF124770B9B7FD2511394313}

La aplicación debe proporcionar a TVSDK la información `PTAuditudeMetadata` necesaria para conectarse al servidor de publicidad.

Para configurar los metadatos del servidor de publicidad:

1. Cree una instancia de [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) y defina sus propiedades.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Establezca la instancia `PTAuditudeMetadata` como metadatos para los metadatos actuales `PTMediaPlayerItem` mediante `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   Este es un ejemplo:

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```
