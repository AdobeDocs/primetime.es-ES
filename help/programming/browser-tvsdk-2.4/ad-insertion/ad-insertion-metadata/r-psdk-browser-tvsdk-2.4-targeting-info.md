---
description: En Adobe Primetime y la toma de decisiones, puede dirigir las publicidades a pares de clave-valor.
seo-description: En Adobe Primetime y la toma de decisiones, puede dirigir las publicidades a pares de clave-valor.
seo-title: Información de objetivo
title: Información de objetivo
uuid: 72114bef-36a1-4f2d-92e8-59f4885d70d2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Información de objetivo{#targeting-information}

En Adobe Primetime y la toma de decisiones, puede dirigir las publicidades a pares de clave-valor.

Para pasar estos pares de valor clave al SDK de TVSDK del explorador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

