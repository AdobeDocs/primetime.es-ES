---
title: Carga segura de publicidad a través de HTTPS
description: Carga segura de publicidad a través de HTTPS
copied-description: true
exl-id: 752d9a35-2faa-4953-8357-e2aff445d3c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Carga segura de publicidad a través de HTTPS {#secure-ad-loading-over-https}

Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad de Primetime y las llamadas relacionadas con CRS a través de HTTPS.

La función no está activada de forma predeterminada. Utilice lo siguiente para habilitar la carga de publicidad segura.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
