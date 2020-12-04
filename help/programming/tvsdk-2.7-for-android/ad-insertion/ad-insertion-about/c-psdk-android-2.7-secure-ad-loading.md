---
description: 'null'
seo-description: 'null'
seo-title: Carga segura de publicidad a través de HTTPS
title: Carga segura de publicidad a través de HTTPS
uuid: 72ab94d3-ee0c-4f02-adf2-c186ae6aec26
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Carga de publicidad segura a través de HTTPS {#secure-ad-loading-over-https}

Adobe Primetime ofrece una opción para solicitar la primera llamada al servidor de publicidad Primetime y las llamadas relacionadas con CRS a través de HTTPS.

La función no está habilitada de forma predeterminada. Utilice lo siguiente para habilitar la carga segura de publicidad.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

