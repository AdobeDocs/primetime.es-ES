---
description: En Adobe Primetime Ad Decisioning, puede dirigir las publicidades a pares clave-valor.
title: Información de segmentación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# Información de objetivo{#targeting-information}

En Adobe Primetime Ad Decisioning, puede dirigir las publicidades a pares clave-valor.

Para pasar estos pares de clave-valor a Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

