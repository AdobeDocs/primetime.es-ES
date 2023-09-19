---
description: TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y los eventos de búsqueda.
title: Eventos de QoS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 0%

---

# Eventos de QoS{#qos-events}

TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y los eventos de búsqueda.

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
