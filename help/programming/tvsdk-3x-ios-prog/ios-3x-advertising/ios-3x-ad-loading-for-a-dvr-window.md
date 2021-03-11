---
description: Puede decidir si resolver solo los anuncios que se producen después del punto activo actual del usuario o también los que se producen antes del punto activo actual.
title: Cargar anuncio para una ventana DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Cargar publicidad para una ventana DVR {#load-ad-for-a-dvr-window}

Puede decidir si resolver solo los anuncios que se producen después del punto activo actual del usuario o también los que se producen antes del punto activo actual.

Cuando un usuario comienza a ver contenido al principio de un flujo DVR, TVSDK resuelve todos los anuncios del flujo en ese momento. Sin embargo, cuando el usuario empieza a ver el contenido en un punto después del principio de la emisión, puede decidir si resuelve solo los anuncios que se producen después del punto activo actual del usuario o también resuelve los anuncios que se han producido antes del punto activo actual.

>[!TIP]
>
>La resolución de los anuncios después del punto activo actual es más rápida, pero si el usuario busca hacia atrás, esta opción impide que el reproductor reproduzca los anuncios que aparecieron anteriormente.

## Control de la carga de anuncios para una ventana DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Para controlar la carga de anuncios para una ventana DVR:

    Para cargar todos los anuncios de toda la emisión, establezca la propiedad &quot;PTAdMetadata.enableDVRAds&quot; en &quot;YES&quot;.

>[!NOTE]
>
>El valor predeterminado es `NO`, y esta opción carga los anuncios solo desde el punto activo actual.

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
