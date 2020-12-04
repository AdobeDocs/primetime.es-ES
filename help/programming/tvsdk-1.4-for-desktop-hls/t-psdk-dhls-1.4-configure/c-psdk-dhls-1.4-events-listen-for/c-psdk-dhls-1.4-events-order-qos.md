---
description: TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.
seo-description: TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.
seo-title: Eventos de QoS
title: Eventos de QoS
uuid: e6ba1e9b-435b-480d-bea9-bff41b4e0b21
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Eventos de QoS{#qos-events}

TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.

El siguiente ejemplo muestra una progresión típica de estos eventos:

```
// For buffering 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_BEGIN, onBufferingBegin); 
private function onBufferingBegin(event:BufferEvent):void { ... } 
 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_END, onBufferingCompleted); 
private function onBufferingCompleted(event:BufferEvent):void { ... } 
 
// For seeking 
mediaPlayer.addEventListener(SeekEvent.SEEK_BEGIN, onSeekBegin); 
private function onSeekBegin(event:SeekEvent):void { ... } 
 
mediaPlayer.addEventListener(SeekEvent.SEEK_COMPLETED, onSeekCompleted); 
private function onSeekCompleted(event:SeekEvent):void { ... } 
 
...  SeekEvent.SEEK_POSITION_ADJUSTED...  //if the desired 
// seek position is modified by the current advertising policies 
```

