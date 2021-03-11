---
description: Puede mostrar la duración del contenido activo actualmente.
title: Mostrar la duración del vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Mostrar la duración del vídeo {#display-the-duration-of-the-video}

Puede mostrar la duración del contenido activo actualmente.

Implemente una visualización de duración de vídeo con el siguiente código de ejemplo:

    La propiedad &quot;PTMediaPlayer&quot;, ` [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)`, contiene el intervalo de ventanas que se puede buscar actualmente: 
    
    * Para VOD, este intervalo es todo el intervalo de contenido de VOD, incluidos los anuncios.
    * Para live/linear, este rango representa la ventana que se puede buscar.
    
    Para obtener más información sobre la API, consulte [TVSDK 3.4 para referencia de API iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
