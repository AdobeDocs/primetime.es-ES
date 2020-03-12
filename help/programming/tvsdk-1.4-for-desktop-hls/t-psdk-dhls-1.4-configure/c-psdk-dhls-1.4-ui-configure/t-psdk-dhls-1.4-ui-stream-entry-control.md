---
description: De forma predeterminada, al iniciar la reproducción, el medio VOD comienza en 0 y el medio activo se inicia en el punto activo del cliente (DefaultMediaPlayer.LIVE_POINT).
seo-description: De forma predeterminada, al iniciar la reproducción, el medio VOD comienza en 0 y el medio activo se inicia en el punto activo del cliente (DefaultMediaPlayer.LIVE_POINT).
seo-title: Escriba una secuencia a una hora específica
title: Escriba una secuencia a una hora específica
uuid: f58d908a-77b9-465f-b3a9-8fe63a249d39
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Escriba una secuencia a una hora específica{#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, el medio VOD comienza en 0 y el medio activo se inicia en el punto activo del cliente (DefaultMediaPlayer.LIVE_POINT).

Pasa una posición a `MediaPlayer.prepareToPlay`.

TVSDK considera que la posición dada es el punto de partida del recurso. No se requiere ninguna operación de búsqueda. Si la posición no está dentro del rango buscable, utiliza la posición predeterminada.

Por ejemplo:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
