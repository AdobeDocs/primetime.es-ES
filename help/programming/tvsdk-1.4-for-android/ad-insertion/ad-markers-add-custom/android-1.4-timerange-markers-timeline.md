---
description: Este ejemplo muestra la forma recomendada de incluir especificaciones de TimeRange en la cronología de reproducción.
title: Colocación de marcadores de anuncios de TimeRange en la cronología
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Coloque marcadores de anuncio de TimeRange en la cronología {#place-timerange-ad-markers-on-the-timeline}

Este ejemplo muestra la forma recomendada de incluir especificaciones de TimeRange en la cronología de reproducción.

1. Traduzca la información de posicionamiento de anuncios fuera de banda a una lista de especificaciones `TimeRange` (es decir, instancias de la clase `TimeRange`).
1. Utilice el conjunto de especificaciones `TimeRange` para rellenar una instancia de la clase `TimeRangeCollection`.
1. Pase la instancia de metadatos, que se puede obtener de la instancia `TimeRangeCollection`, al método `replaceCurrentItem` (parte de la interfaz de MediaPlayer).
1. Espere a que TVSDK pase al estado `PREPARED` esperando a que se active la llamada de retorno `PlaybackEventListener#onPrepared`.
1. Inicie la reproducción de vídeo llamando al método `play()` (parte de la interfaz `MediaPlayer`).

* Gestión de conflictos de cronología: Puede haber casos en los que algunas especificaciones `TimeRange` se superponen en la cronología de reproducción. Por ejemplo, el valor de la posición inicial correspondiente a una especificación `TimeRange` puede ser inferior al valor de la posición final que ya se colocó. En este caso, TVSDK ajusta silenciosamente la posición inicial de la especificación `TimeRange` infractora para evitar conflictos de tiempo. Mediante este ajuste, el nuevo `TimeRange` se hace más corto de lo especificado originalmente. Si el ajuste es tan extremo que llevaría a un `TimeRange` con una duración de cero ms, TVSDK descarta silenciosamente la especificación `TimeRange` ofensiva.
* Cuando se proporcionan `TimeRange` especificaciones para las pausas publicitarias personalizadas, TVSDK intenta traducirlas en publicidades que se agrupan dentro de las pausas publicitarias. TVSDK busca especificaciones `TimeRange` adyacentes y las agrupa en pausas publicitarias independientes. Si hay intervalos de tiempo que no son adyacentes a ningún otro intervalo de tiempo, se traducen en pausas publicitarias que contienen un solo anuncio.
* Se da por hecho que el elemento del reproductor de contenidos que se está cargando apunta a un recurso de VOD. TVSDK lo comprueba siempre que la aplicación intenta cargar un recurso multimedia cuyos metadatos contienen `TimeRange` especificaciones que solo se pueden usar en el contexto de la función de marcadores de anuncios personalizados. Si el recurso subyacente no es del tipo VOD, la biblioteca TVSDK genera una excepción.
* Al tratar con marcadores de anuncios personalizados, TVSDK desactiva otros mecanismos de resolución de anuncios (a través de Adobe Primetime ad decisioning (anteriormente conocido como Auditude) u otro sistema de aprovisionamiento de anuncios). Puede utilizar uno de los distintos módulos de resolución de anuncios proporcionados por TVSDK o el mecanismo de marcadores de anuncios personalizados. Al utilizar la API de marcadores de anuncio personalizados, el contenido de la publicidad se considera ya resuelto y se coloca en la cronología.

El siguiente fragmento de código proporciona un ejemplo sencillo en el que se coloca un conjunto de tres especificaciones de intervalo de tiempo en la cronología como marcadores de anuncio personalizados.

```java>
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
TimeRangeCollection timeRanges = new TimeRangeCollection();  
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
 
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                               timeRanges.toMetadata(null)); 
 
// prepare the content for playback by creating 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentItem(mediaResource); 
// wait for TVSDK to reach the PREPARED state 
... 
MediaPlayer.PlaybackEventListener playbackEventListener = new 
  MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // TVSDK in in the PREPARED state. We are allowed to start the playback  
        mediaPlayer.play(); 
    } 
} 
```
