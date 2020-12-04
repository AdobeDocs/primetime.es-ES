---
description: Puede mostrar la duración del contenido activo en ese momento.
seo-description: Puede mostrar la duración del contenido activo en ese momento.
seo-title: Mostrar la duración del vídeo
title: Mostrar la duración del vídeo
uuid: 02042070-9c55-4cbb-9dc1-49987451eb8f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Mostrar la duración del video {#display-the-duration-of-the-video}

Puede mostrar la duración del contenido activo en ese momento.

Implemente una visualización de duración de vídeo con el siguiente código de muestra:

    La propiedad &quot;PTMediaPlayer&quot;, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contiene el intervalo de ventana actual que se puede buscar:
    
    * Para VOD, este intervalo es todo el intervalo de contenido de VOD, incluidos los anuncios.
    * Para live/linear, este rango representa la ventana que se puede buscar.
    
    Para obtener más información sobre la API, consulte [Referencia de la API de TVSDK 1.4 para iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
