---
title: Carga de publicidad segura a través de HTTPS
description: Carga de publicidad segura a través de HTTPS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Carga de publicidad segura a través de HTTPS{#secure-ad-loading-over-https}

Adobe Primetime puede solicitar servidores de publicidad de terceros a través de https incluso si el reproductor está alojado en http. Solo esas llamadas de servidores de publicidad se actualizan a https que el cliente busca durante la fase de resolución de anuncios de Auditude.

>[!NOTE]
>
>Esta función no es compatible con el Flash.

Utilice lo siguiente para habilitar la carga segura de anuncios. No está habilitado de forma predeterminada.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
