---
title: Carga segura de publicidad a través de HTTPS
description: Carga segura de publicidad a través de HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
