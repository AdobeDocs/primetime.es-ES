---
description: En Adobe Primetime ad decisioning, puede segmentar los anuncios en pares clave-valor.
title: Información de direccionamiento
exl-id: 25610f7d-6b14-4ed1-b61c-9e6bf13ba8e6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
