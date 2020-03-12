---
description: Cuando la reproducción incluye publicidad, TVSDK distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
seo-description: Cuando la reproducción incluye publicidad, TVSDK distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
seo-title: Orden de los eventos publicitarios
title: Orden de los eventos publicitarios
uuid: 34a6a606-2f2e-42de-88fd-c91202cafddf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Orden de los eventos publicitarios{#order-of-advertising-events}

Cuando la reproducción incluye publicidad, TVSDK distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Al reproducir publicidades, el orden de los eventos es:

* `AdBreakPlaybackEvent.AD_BREAK_STARTED`
* Se envían los siguientes datos para cada publicidad en la pausa publicitaria:

   * `AdPlaybackEvent.AD_STARTED`
   * `AdPlaybackEvent.AD_PROGRESS` (varias veces durante la reproducción de un anuncio)
   * `AdClickEvent.AD_CLICK` (para cada clic)
   * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

El siguiente ejemplo muestra una progresión típica de los eventos de reproducción de publicidad:

```
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_STARTED, onAdBreakStarted); 
private function onAdBreakStarted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED, onAdBreakCompleted); 
private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
private function onAdStarted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_PROGRESS, onAdProgress); 
private function onAdProgress(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad;  
    var progress:uint = event.progress; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
private function onAdCompleted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdClickEvent.AD_CLICK, onAdClick); 
private function onAdClick(event:AdClickThroughEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    var info:AdClick = event.adClick; 
    ... 
} 
```

