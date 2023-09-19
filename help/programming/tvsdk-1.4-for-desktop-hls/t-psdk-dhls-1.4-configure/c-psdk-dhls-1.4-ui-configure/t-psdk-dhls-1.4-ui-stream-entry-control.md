---
description: De forma predeterminada, al iniciar la reproducción, los medios de VOD comienzan en 0 y los medios en directo se inician en el punto en directo del cliente (DefaultMediaPlayer.LIVE_POINT).
title: Introducir un flujo a una hora específica
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
