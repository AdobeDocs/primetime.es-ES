---
description: De forma predeterminada, al iniciar la reproducción, el contenido de VOD se inicia en 0 y el contenido en directo se inicia en el punto activo del cliente (DefaultMediaPlayer.LIVE_POINT).
title: Introduzca una emisión a una hora específica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Introduzca un flujo a una hora específica{#enter-a-stream-at-a-specific-time}

De forma predeterminada, al iniciar la reproducción, el contenido de VOD se inicia en 0 y el contenido en directo se inicia en el punto activo del cliente (DefaultMediaPlayer.LIVE_POINT).

Pase una posición a `MediaPlayer.prepareToPlay`.

TVSDK considera que la posición dada es el punto de partida del recurso. No se requiere ninguna operación de búsqueda. Si la posición no está dentro del rango en el que se puede buscar, utiliza la posición predeterminada.

Por ejemplo:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
