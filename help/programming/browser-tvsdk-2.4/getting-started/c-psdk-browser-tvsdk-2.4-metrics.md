---
description: El SDK de explorador proporciona métricas que se pueden utilizar para analizar y depurar. Puede obtener estas métricas usando QoSProvider.
title: Métricas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 5%

---


# Métricas{#metrics}

El SDK de explorador proporciona métricas que se pueden utilizar para analizar y depurar. Puede obtener estas métricas usando QoSProvider.

Por ejemplo:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

