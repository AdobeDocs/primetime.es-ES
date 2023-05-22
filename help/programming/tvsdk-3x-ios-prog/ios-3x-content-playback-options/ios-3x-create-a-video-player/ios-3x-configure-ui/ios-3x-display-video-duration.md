---
description: Puede mostrar la duración del contenido activo actualmente.
title: Mostrar la duración del vídeo
exl-id: a41cb291-9355-44cf-80bb-9c3cf6628b81
source-git-commit: 85818281390b68522da2663496be025acf8f8675
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Mostrar la duración del vídeo {#display-the-duration-of-the-video}

Puede mostrar la duración del contenido activo actualmente.

Implemente una visualización de duración de vídeo con el siguiente código de ejemplo:

El `PTMediaPlayer` propiedad, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contiene el intervalo de ventana actual en el que se puede buscar:

* Para VOD, este intervalo es todo el intervalo de contenido de VOD, incluidos los anuncios.
* Para live/linear, este rango representa la ventana en la que se puede buscar.

Para obtener más información sobre la API, consulte [Referencia de la API de TVSDK 3.4 para iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
