---
title: Carga segura de publicidad a través de HTTPS
description: Carga segura de publicidad a través de HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Carga segura de publicidad a través de HTTPS{#secure-ad-loading-over-https}

Adobe Primetime puede solicitar servidores de publicidad de terceros a través de https incluso si el reproductor está alojado en http. Solo las llamadas a servidores de publicidad se actualizan a https que el cliente busca durante la fase de resolución de publicidad de Auditude.

>[!NOTE]
>
>Esta función no es compatible con el Flash.

Utilice lo siguiente para habilitar la carga de publicidad segura. No está activada de forma predeterminada.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
