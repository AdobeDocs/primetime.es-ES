---
description: TVSDK es compatible con la resolución e inserción de anuncios para VOD y flujos en directo/lineal.
seo-description: TVSDK es compatible con la resolución e inserción de anuncios para VOD y flujos en directo/lineal.
seo-title: Metadatos del servidor de publicidad Primetime
title: Metadatos del servidor de publicidad Primetime
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Información general {#primetime-ad-server-metadata-overview}

TVSDK es compatible con la resolución e inserción de anuncios para VOD y flujos en directo/lineal.

[!PREREQUISITE] {othertype=&quot;Prequisite&quot;}

Antes de incluir publicidad en el contenido del vídeo, proporcione la siguiente información de metadatos:

* Un `mediaID`, que identifica el contenido específico que se va a reproducir.
* Su `zoneID`, que identifica a su empresa o sitio web.
* El dominio del servidor de publicidad, que especifica el dominio del servidor de publicidad asignado.
* Otros parámetros de objetivo.

## Configurar metadatos de Primetime y de servidor {#section_86C4A3B2DF124770B9B7FD2511394313}

La aplicación debe proporcionar a TVSDK la `PTAuditudeMetadata` información necesaria para conectarse al servidor de publicidad.

Para configurar los metadatos del servidor de publicidad:

1. Cree una instancia de [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) y defina sus propiedades.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Defina la `PTAuditudeMetadata` instancia como metadatos para los `PTMediaPlayerItem` metadatos actuales utilizando `PTAdResolvingMetadataKey`.

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
