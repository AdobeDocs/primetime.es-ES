---
description: Cuando la reproducción incluye publicidad, el SDK de TVSDK del explorador distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
seo-description: Cuando la reproducción incluye publicidad, el SDK de TVSDK del explorador distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
seo-title: Orden de los eventos publicitarios
title: Orden de los eventos publicitarios
uuid: 9787e6ac-5e52-4d7d-8fc7-f7609633707c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Orden de los eventos de publicidad{#order-of-advertising-events}

Cuando la reproducción incluye publicidad, el SDK de TVSDK del explorador distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Al reproducir anuncios, el orden de los eventos es:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* Se envían los siguientes datos para cada publicidad en la pausa publicitaria:

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (varias veces durante la reproducción de un anuncio)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

El siguiente ejemplo muestra una progresión típica de los eventos de reproducción de publicidad:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```

