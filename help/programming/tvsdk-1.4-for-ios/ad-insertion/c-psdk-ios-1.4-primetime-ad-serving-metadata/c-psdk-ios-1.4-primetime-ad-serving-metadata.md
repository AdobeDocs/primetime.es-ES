---
description: TVSDK admite la resolución e inserción de anuncios para VOD y flujos en directo/lineales.
title: Metadatos de Primetime y del servidor
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Información general {#primetime-ad-server-metadata-overview}

TVSDK admite la resolución e inserción de anuncios para VOD y flujos en directo/lineales.

>[!NOTE]
>
>Para poder incluir publicidad en el contenido de vídeo, proporcione la siguiente información de metadatos:
>
>* A `mediaID`, que identifica el contenido específico que se va a reproducir.
>* Su `zoneID`, que identifica a su empresa o sitio web.
>* El dominio del servidor de publicidad, que especifica el dominio del servidor de publicidad asignado.
>* Otros parámetros de segmentación.
>

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

## Habilitar los anuncios en la reproducción de evento completo {#section_6016E1DAF03645C8A8388D03C6AB7571}

La reproducción de evento completo (FER) es un recurso de VOD que actúa como un recurso activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos y las indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo/lineal puede parecerse al contenido de VOD. Por ejemplo, cuando el contenido en directo termina, una `EXT-X-ENDLIST` la etiqueta se anexa al manifiesto en directo. Para HLS, la variable `EXT-X-ENDLIST` significa que el flujo es un flujo de VOD. TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD normal para insertar correctamente los anuncios.

La aplicación debe indicar a TVSDK si el contenido está activo o es VOD especificando la variable `PTAdSignalingMode`.

Para un flujo FER, el servidor de Adobe Primetime ad Decisioning no debe proporcionar la lista de pausas publicitarias que deben insertarse en la cronología antes de iniciar la reproducción. Este es el proceso típico del contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad para cada punto de referencia a fin de solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de anuncio adicional para anuncios previos a la emisión.

1. Desde una fuente externa, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si el comportamiento predeterminado debe sobrescribirse, especifique el `PTAdSignalingMode` mediante `PTAdMetadata.signalingMode`.

   Los valores válidos son `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`, y `PTAdSignalingModeServerMap`.

   Debe establecer el modo de señalización de anuncio antes de llamar a `prepareToPlay`. Una vez que TVSDK empieza a resolver y a colocar los anuncios en la cronología, se omiten los cambios en el modo de señalización de publicidad. Establezca el modo cuando cree los metadatos de publicidad para el recurso.

1. Continuar con la reproducción.

   ```
      PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.zoneId = your-auditude-zone-id; 
   adMetadata.domain = @"your-auditude-domain"; 
   //adMetadata.enableDVRAds = YES; // FOR LIVE DVR case 
   //adMetadata.signalingMode = PTAdSignalingModeManifestCues;  
   // FOR VOD FER case 
   NSMutableDictionary *targetingParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [targetingParameters setValue:@"ipad" forKey:@"device"]; 
   [targetingParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.targetingParameters = targetingParameters; 
   NSMutableDictionary *customParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [customParameters setValue:@"your-media-id" forKey:@"NW_ID"]; 
   [customParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.customParameters = customParameters; 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   ```
