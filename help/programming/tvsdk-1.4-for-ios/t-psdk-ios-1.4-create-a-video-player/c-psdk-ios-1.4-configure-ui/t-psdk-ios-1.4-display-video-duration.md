---
description: Puede mostrar la duración del contenido activo actualmente.
title: Mostrar la duración del vídeo
exl-id: 4e31d784-4d16-470b-8317-11be32a55c2f
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Mostrar la duración del vídeo {#display-the-duration-of-the-video}

Puede mostrar la duración del contenido activo actualmente.

Implemente una visualización de duración de vídeo con el siguiente código de ejemplo:

La variable `PTMediaPlayer` propiedad, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contiene el intervalo de ventanas que se puede buscar actualmente:

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
