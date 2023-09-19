---
description: Cuando la reproducción incluye publicidad, el TVSDK del explorador envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
title: Orden de los eventos publicitarios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Orden de los eventos publicitarios{#order-of-advertising-events}

Cuando la reproducción incluye publicidad, el TVSDK del explorador envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Al reproducir anuncios, el orden de los eventos es:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* Se envían los siguientes elementos por cada anuncio de la pausa publicitaria:

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
