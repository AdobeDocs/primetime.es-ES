---
description: 'null'
seo-description: 'null'
seo-title: Carga segura de publicidad a través de HTTPS
title: Carga segura de publicidad a través de HTTPS
uuid: 0d680fef-a372-4157-a89b-d9f10003c768
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Carga de publicidad segura a través de HTTPS{#secure-ad-loading-over-https}

Adobe Primetime ofrece una opción para solicitar la primera llamada al servidor de publicidad Primetime y las llamadas relacionadas con CRS a través de HTTPS.

La función no está habilitada de forma predeterminada. Utilice lo siguiente para habilitar la carga segura de publicidad.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

