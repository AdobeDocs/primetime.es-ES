---
description: Puede decidir si desea resolver solo los anuncios que se producen después del punto en directo actual del usuario o también los anuncios que se producen antes del punto en directo actual.
title: Cargar anuncio para una ventana de DVR
exl-id: 3e8542a8-0912-4023-904d-0fdb28411a9d
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Cargar anuncio para una ventana de DVR {#load-ad-for-a-dvr-window}

Puede decidir si desea resolver solo los anuncios que se producen después del punto en directo actual del usuario o también los anuncios que se producen antes del punto en directo actual.

Cuando un usuario comienza a ver contenido al principio de un flujo DVR, TVSDK resuelve todos los anuncios del flujo en ese momento. Sin embargo, cuando el usuario comienza a ver contenido en un punto después del inicio del flujo, puede decidir si desea resolver solo los anuncios que se producen después del punto de activación actual del usuario o también resolver los anuncios que se produjeron antes del punto de activación actual.

>[!TIP]
>
>La resolución de anuncios después del punto en directo actual es más rápida, pero si el usuario hace una búsqueda hacia atrás, esta opción evita que el reproductor reproduzca anuncios que aparecieron anteriormente.

## Control y carga de una ventana DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Para controlar la carga de anuncios de una ventana DVR:

Para cargar todos los anuncios de todo el flujo, configure el `PTAdMetadata.enableDVRAds` propiedad a `YES`.

>[!NOTE]
>
>El valor predeterminado es `NO`y esta opción carga anuncios solo desde el punto en directo actual.

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
