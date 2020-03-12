---
description: Puede decidir si resolver solo las publicidades que se producen después del punto activo actual del usuario o también resolver las publicidades que se producen antes del punto activo actual.
seo-description: Puede decidir si resolver solo las publicidades que se producen después del punto activo actual del usuario o también resolver las publicidades que se producen antes del punto activo actual.
seo-title: Cargar anuncio para una ventana DVR
title: Cargar anuncio para una ventana DVR
uuid: 67bc3924-3d17-4d1a-b9a7-be8d0488a970
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Cargar anuncio para una ventana DVR {#load-ad-for-a-dvr-window}

Puede decidir si resolver solo las publicidades que se producen después del punto activo actual del usuario o también resolver las publicidades que se producen antes del punto activo actual.

Cuando un usuario comienza a ver el contenido al principio de un flujo DVR, TVSDK resuelve todas las publicidades del flujo en ese momento. Sin embargo, cuando el usuario comienza a ver el contenido en un momento posterior al inicio del flujo, puede decidir si resolver solo las publicidades que se producen después del punto activo actual del usuario o también resolver las publicidades que se produjeron antes del punto activo actual.

>[!TIP]
>
>La resolución de anuncios después del punto activo actual es más rápida, pero si el usuario busca hacia atrás, esta opción evita que el reproductor reproduzca anuncios que aparecieron antes.

## Control y carga de anuncios para una ventana DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Para controlar la carga de anuncios para una ventana DVR:

Para cargar todas las publicidades para el flujo completo, establezca la `PTAdMetadata.enableDVRAds` propiedad en `YES`.

>[!NOTE]
>
>El valor predeterminado es `NO`y esta opción carga publicidades solamente desde el punto activo actual.

Por ejemplo:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
 
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
adMetadata.zoneId = <ZoneId>; 
adMetadata.domain = <Domain>; 
 
// Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
// (PTAuditudeMetadata is a subclass of PTAdMetadata)  
adMetadata.enableDVRAds = YES; 
 
[metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
 
//Create PTMediaPlayerItem with the previously prepared metadata    
playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
```
