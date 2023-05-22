---
description: TVSDK envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
title: Orden de los eventos de reproducción
exl-id: d03692f6-04b9-4962-92d1-fad671d06665
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Orden de los eventos de reproducción{#order-of-playback-events}

TVSDK envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

Los siguientes ejemplos muestran el orden de algunos eventos que incluyen eventos de reproducción.

* Al cargar correctamente un recurso de medios mediante `MediaPlayer.replaceCurrentResource`, el orden de los eventos es:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.INITIALIZED`

* Al preparar la reproducción mediante `MediaPlayer.prepareToPlay`, el orden de los eventos es:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` si se insertaron anuncios
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.PREPARED`

* En el caso de los flujos lineales/en directo, durante la reproducción a medida que avanza la ventana de reproducción y se resuelven oportunidades adicionales, el orden de los eventos es el siguiente:

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` si se insertaron anuncios

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

El siguiente ejemplo muestra una progresión típica de los eventos:

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
