---
description: 'null'
seo-description: 'null'
seo-title: Carga segura de publicidad a través de HTTPS
title: Carga segura de publicidad a través de HTTPS
uuid: 18be77cc-c59b-4982-b8c1-e4451495edd2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
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
