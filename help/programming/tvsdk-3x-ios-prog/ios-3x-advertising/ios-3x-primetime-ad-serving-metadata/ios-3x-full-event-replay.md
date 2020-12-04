---
description: TVSDK es compatible con la resolución e inserción de anuncios para VOD y flujos en directo/lineal.
seo-description: TVSDK es compatible con la resolución e inserción de anuncios para VOD y flujos en directo/lineal.
seo-title: Metadatos del servidor de publicidad Primetime
title: Metadatos del servidor de publicidad Primetime
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Habilitar publicidades en reproducción de evento completo {#section_6016E1DAF03645C8A8388D03C6AB7571}

La reproducción en evento completo (FER) es un recurso de VOD que actúa como recurso de vídeo/DVR, por lo que la aplicación debe tomar los pasos necesarios para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos/indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo o lineal puede parecerse al contenido de VOD. Por ejemplo, cuando se completa el contenido activo, se agrega una etiqueta `EXT-X-ENDLIST` al manifiesto activo. Para HLS, la etiqueta `EXT-X-ENDLIST` significa que el flujo es un flujo VOD. TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD normal para insertar correctamente anuncios.

La aplicación debe indicar a TVSDK si el contenido está activo o VOD especificando `PTAdSignalingMode`.

Para un flujo FER, el servidor de decisiones de anuncios de Adobe Primetime no debe proporcionar la lista de pausas publicitarias que deben insertarse en la línea de tiempo antes de iniciar la reproducción. Este es el proceso habitual para el contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad para cada punto de referencia para solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de publicidad adicional para anuncios previos.

1. Desde un origen externo, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si se debe sobrescribir el comportamiento predeterminado, especifique `PTAdSignalingMode` mediante `PTAdMetadata.signalingMode`.

   Los valores válidos son `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues` y `PTAdSignalingModeServerMap`.

   Debe establecer el modo de señalización de publicidad antes de llamar a `prepareToPlay`. Tras los inicios de TVSDK para resolver y colocar anuncios en la línea de tiempo, se omiten los cambios en el modo de señalización de publicidad. Establezca el modo cuando cree los metadatos de publicidad para el recurso.

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
