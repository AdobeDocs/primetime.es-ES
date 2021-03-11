---
description: Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning .
title: Requisitos de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Tiempo de espera de anuncio {#ad-timeout}

## Requisitos de base AV {#av-foundation-requirements}

En el caso del contenido de VOD, la vinculación de la lista de reproducción, que implica la carga del manifiesto de contenido principal, la resolución de anuncios y la carga del manifiesto de anuncios, debe completarse en un plazo de 35 segundos.

En el caso del contenido activo, cada vez que se actualiza la lista de reproducción, la vinculación de la lista de reproducción debe completarse en un plazo de 20 segundos

**API relevantes para el tiempo de espera de la resolución de anuncios**

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

A continuación, siga la sección: [Metadatos del servidor de publicidad de Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

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

A continuación, siga la sección: [Metadatos del servidor de publicidad de Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
