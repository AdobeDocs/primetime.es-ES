---
description: TVSDK envía eventos/notificaciones en secuencias esperadas generalmente. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
title: Orden de los eventos de reproducción
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Orden de los eventos de reproducción{#order-of-playback-events}

TVSDK envía eventos/notificaciones en secuencias esperadas generalmente. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

Los siguientes ejemplos muestran el orden de algunos eventos que incluyen eventos de reproducción.

* Cuando se carga correctamente un recurso de medios a través de `MediaPlayer.replaceCurrentResource`, el orden de los eventos es:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.INITIALIZED`

* Al prepararse para la reproducción mediante `MediaPlayer.prepareToPlay`, el orden de los eventos es:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` si se insertaron anuncios
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.PREPARED`

* Para emisiones en directo/lineales, durante la reproducción a medida que avanza la ventana de reproducción y se resuelven las oportunidades adicionales, el orden de los eventos es:

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` si se insertaron anuncios

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

El siguiente ejemplo muestra una progresión típica de eventos:

```
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
public function onItemCreated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
public function onItemUpdated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
public function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    switch(event.status){ 
        case MediaPlayerStatus.INITIALIZING: 
        case MediaPlayerStatus.INITIALIZED: 
        ... 
    } 
    ... 
} 
mediaPlayer.addEventListener(TimeChangeEvent.TIME_CHANGED, onTimeChanged); 
public function onTimeChanged(event:TimeChangeEvent):void { 
    var timeInMilliseconds:Number = event.time; 
    ... 
}
```

