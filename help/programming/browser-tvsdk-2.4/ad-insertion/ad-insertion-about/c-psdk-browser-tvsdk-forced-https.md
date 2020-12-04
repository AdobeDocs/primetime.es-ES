---
description: 'null'
seo-description: 'null'
seo-title: Carga segura de publicidad a través de HTTPS
title: Carga segura de publicidad a través de HTTPS
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---


# Carga de publicidad segura a través de HTTPS{#secure-ad-loading-over-https}

Adobe Primetime puede solicitar servidores de publicidad de terceros a través de https incluso si el reproductor está alojado en http. Solo esas llamadas de servidores de publicidad se actualizan a https que el cliente busca durante la fase de resolución de publicidad de Auditude.

>[!NOTE]
>
>Esta función no es compatible con Flash.

Utilice lo siguiente para habilitar la carga segura de publicidad. No está habilitado de forma predeterminada.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
