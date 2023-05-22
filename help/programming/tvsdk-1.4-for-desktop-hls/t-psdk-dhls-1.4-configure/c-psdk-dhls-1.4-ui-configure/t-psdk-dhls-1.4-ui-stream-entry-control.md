---
description: De forma predeterminada, al iniciar la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (DefaultMediaPlayer.LIVE_POINT).
title: Introducir un flujo a una hora específica
exl-id: b97dbabf-e2ab-4669-a9f3-9129af938a40
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Introducir un flujo a una hora específica{#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (DefaultMediaPlayer.LIVE_POINT).

Pasar una posición a `MediaPlayer.prepareToPlay`.

TVSDK considera que la posición dada es el punto de partida del recurso. No se requiere ninguna operación de búsqueda. Si la posición no se encuentra dentro del rango en el que se puede buscar, utiliza la posición predeterminada.

Por ejemplo:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
