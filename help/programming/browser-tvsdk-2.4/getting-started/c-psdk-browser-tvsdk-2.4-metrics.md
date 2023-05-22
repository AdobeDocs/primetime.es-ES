---
description: El TVSDK del explorador proporciona métricas que se pueden utilizar para analizar y depurar. Puede obtener estas métricas mediante QoSProvider.
title: Métricas
exl-id: 1413ddf5-b458-4040-abf8-8d9dbd6b80e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
