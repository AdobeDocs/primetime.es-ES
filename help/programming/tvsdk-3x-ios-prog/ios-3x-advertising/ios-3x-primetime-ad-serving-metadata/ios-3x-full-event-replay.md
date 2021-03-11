---
description: TVSDK admite la resolución e inserción de anuncios para flujos VOD y en directo/lineal.
title: Metadatos del servidor de publicidad de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Habilitar anuncios en reproducción de eventos completos {#section_6016E1DAF03645C8A8388D03C6AB7571}

La reproducción de eventos completos (FER) es un recurso de VOD que actúa como activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos/indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo/lineal puede parecerse al contenido de VOD. Por ejemplo, cuando el contenido en directo se completa, se añade una etiqueta `EXT-X-ENDLIST` al manifiesto en directo. Para HLS, la etiqueta `EXT-X-ENDLIST` significa que el flujo es un flujo de VOD. TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD normal para insertar anuncios correctamente.

La aplicación debe indicar a TVSDK si el contenido está activo o VOD; para ello, especifique `PTAdSignalingMode`.

Para un flujo FER, el servidor de Adobe Primetime ad decisioning no debe proporcionar la lista de pausas publicitarias que deben insertarse en la cronología antes de iniciar la reproducción. Este es el proceso típico del contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad de cada punto de referencia para solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de anuncio adicional para anuncios previos a la emisión.

1. Desde una fuente externa, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si se debe sobrescribir el comportamiento predeterminado, especifique `PTAdSignalingMode` utilizando `PTAdMetadata.signalingMode`.

   Los valores válidos son `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues` y `PTAdSignalingModeServerMap`.

   Debe establecer el modo de señalización de publicidad antes de llamar a `prepareToPlay`. Una vez que TVSDK empiece a resolver y a colocar anuncios en la cronología, se omiten los cambios en el modo de señalización de anuncios. Establezca el modo cuando cree los metadatos de publicidad para el recurso.

1. Continúe con la reproducción.

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
