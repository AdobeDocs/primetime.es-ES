---
description: Puede insertar anuncios en el VOD y contenido en directo o lineal mediante la interfaz de Adobe Primetime para la toma de decisiones de publicidad.
seo-description: Puede insertar anuncios en el VOD y contenido en directo o lineal mediante la interfaz de Adobe Primetime para la toma de decisiones de publicidad.
seo-title: Requisitos de publicidad
title: Requisitos de publicidad
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Tiempo de espera de publicidad {#ad-timeout}

## Requisitos de la Fundación AV {#av-foundation-requirements}

En el caso del contenido de VOD, la vinculación de la lista de reproducción, que implica la carga del manifiesto de contenido principal, la resolución de anuncios y la carga del manifiesto de anuncios, se debe completar en un plazo de 35 segundos.

En el caso de contenido en directo, cada vez que se actualice la lista de reproducción, la vinculación de la lista de reproducción se completará en un plazo de 20 segundos

**API relevantes para el tiempo de espera de AdResolution**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

Puede establecer adResolutionTimeout estableciendo PTAdMetadata::adResolutionTimeout al configurar los metadatos de la publicidad.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

A continuación, siga la sección: [Metadatos](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)del servidor de publicidad Primetime.

**API relevantes para el tiempo de espera de AdManifest**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

Puede establecer adManifestTimeout estableciendo PTAdMetadata::adManifestTimeout al configurar los metadatos de la publicidad.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

A continuación, siga la sección: [Metadatos](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)del servidor de publicidad Primetime.
