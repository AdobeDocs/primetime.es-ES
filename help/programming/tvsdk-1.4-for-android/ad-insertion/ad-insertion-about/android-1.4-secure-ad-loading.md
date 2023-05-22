---
title: Carga segura de publicidad a través de HTTPS
description: Carga segura de publicidad a través de HTTPS
copied-description: true
exl-id: e12cb9d4-05d4-485e-b629-1af680b83e04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Carga segura de publicidad a través de HTTPS{#secure-ad-loading-over-https}

Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad de Primetime y las llamadas relacionadas con CRS a través de HTTPS.

La función no está activada de forma predeterminada. Utilice lo siguiente para habilitar la carga de publicidad segura.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
