---
description: En Adobe Primetime ad decisioning, puede segmentar los anuncios en pares clave-valor.
title: Información de direccionamiento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# Información de direccionamiento{#targeting-information}

En Adobe Primetime ad decisioning, puede segmentar los anuncios en pares clave-valor.

Para pasar estos pares de valor clave al TVSDK del explorador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
