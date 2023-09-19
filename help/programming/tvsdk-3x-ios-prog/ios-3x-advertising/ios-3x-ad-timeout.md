---
description: Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning.
title: Requisitos publicitarios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Tiempo de espera de publicidad {#ad-timeout}

## Requisitos básicos de AV {#av-foundation-requirements}

En el caso del contenido de VOD, la vinculación de lista de reproducción, que implica la carga del manifiesto de contenido principal, la resolución del anuncio y la carga del manifiesto del anuncio, debe completarse en un plazo de 35 segundos.

En el caso del contenido en directo, cada vez que se actualice la lista de reproducción, la vinculación de la lista de reproducción debe completarse en un plazo de 20 segundos

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

A continuación, siga esta sección: [Metadatos de Primetime y del servidor](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

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

A continuación, siga esta sección: [Metadatos de Primetime y del servidor](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
