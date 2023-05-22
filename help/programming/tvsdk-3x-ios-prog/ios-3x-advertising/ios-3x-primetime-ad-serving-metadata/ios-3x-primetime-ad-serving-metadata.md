---
description: TVSDK admite la resolución e inserción de anuncios para VOD y flujos en directo/lineales.
title: Metadatos de Primetime y del servidor
exl-id: f27657ac-4037-45e5-a658-ad9a783dd990
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Información general {#primetime-ad-server-metadata-overview}

TVSDK admite la resolución e inserción de anuncios para VOD y flujos en directo/lineales.

## Requisito previo

Para poder incluir publicidad en el contenido de vídeo, proporcione la siguiente información de metadatos:

* A `mediaID`, que identifica el contenido específico que se va a reproducir.
* Su `zoneID`, que identifica a su empresa o sitio web.
* El dominio del servidor de publicidad, que especifica el dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

## Configuración de Primetime y metadatos del servidor {#section_86C4A3B2DF124770B9B7FD2511394313}

La aplicación debe proporcionar a TVSDK la información necesaria `PTAuditudeMetadata` información para conectarse al servidor de publicidad.

Para configurar los metadatos del servidor de publicidad:

1. Cree una instancia de [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) y establezca sus propiedades.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Configure las variables `PTAuditudeMetadata` instancia como metadatos para el `PTMediaPlayerItem` metadatos mediante `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   A continuación se muestra un ejemplo:

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
