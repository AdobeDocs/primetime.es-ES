---
description: Puede mostrar la duración del contenido activo en ese momento.
seo-description: Puede mostrar la duración del contenido activo en ese momento.
seo-title: Mostrar la duración del vídeo
title: Mostrar la duración del vídeo
uuid: 945f222d-80ba-4832-a06f-9bb8db6adbcb
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Mostrar la duración del vídeo {#display-the-duration-of-the-video}

Puede mostrar la duración del contenido activo en ese momento.

Implemente una visualización de duración de vídeo con el siguiente código de muestra:

    La propiedad &quot;PTMediaPlayer&quot;, ` [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)&quot;, contiene el intervalo de ventana que se puede buscar:
    
    * Para VOD, este intervalo es todo el intervalo de contenido de VOD, incluidos los anuncios.
    * Para live/linear, este rango representa la ventana que se puede buscar.
    
    Para obtener más información sobre la API, consulte [Referencia de API de TVSDK 3.4 para iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
