---
title: Carga segura de publicidad a través de HTTPS
description: Carga segura de publicidad a través de HTTPS
copied-description: true
exl-id: f9de1a2b-4eea-4028-83db-1b4021d1fbb7
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
