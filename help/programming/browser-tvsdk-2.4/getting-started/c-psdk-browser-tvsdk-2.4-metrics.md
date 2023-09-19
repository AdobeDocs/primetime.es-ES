---
description: El TVSDK del explorador proporciona métricas que se pueden utilizar para analizar y depurar. Puede obtener estas métricas mediante QoSProvider.
title: Métricas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Métricas{#metrics}

El TVSDK del explorador proporciona métricas que se pueden utilizar para analizar y depurar. Puede obtener estas métricas mediante QoSProvider.

Por ejemplo:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
