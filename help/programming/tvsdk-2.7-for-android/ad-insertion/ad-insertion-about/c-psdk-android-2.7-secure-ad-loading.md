---
title: Carga segura de publicidad a través de HTTPS
description: Carga segura de publicidad a través de HTTPS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Carga segura de publicidad a través de HTTPS {#secure-ad-loading-over-https}

Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad de Primetime y a las llamadas relacionadas con CRS a través de HTTPS.

La función no está activada de forma predeterminada. Utilice lo siguiente para habilitar la carga segura de anuncios.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

