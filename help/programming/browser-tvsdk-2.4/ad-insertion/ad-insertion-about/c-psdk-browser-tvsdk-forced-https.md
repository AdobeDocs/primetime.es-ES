---
title: Carga segura de publicidad a través de HTTPS
description: Carga segura de publicidad a través de HTTPS
copied-description: true
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Carga segura de publicidad a través de HTTPS{#secure-ad-loading-over-https}

Adobe Primetime puede solicitar servidores de publicidad de terceros a través de https incluso si el reproductor está alojado en http. Solo las llamadas a servidores de publicidad se actualizan a https que el cliente busca durante la fase de resolución de Auditude Ad.

>[!NOTE]
>
>Esta función no es compatible con el Flash.

Utilice lo siguiente para habilitar la carga de publicidad segura. No está activada de forma predeterminada.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
