---
description: Este ejemplo muestra la forma recomendada de incluir especificaciones de TimeRange en la cronología de reproducción.
title: Colocar marcadores de anuncios de TimeRange en la cronología
exl-id: 53b48d5b-7725-48ae-848a-ccd2a54b132a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Colocar marcadores de anuncios de TimeRange en la cronología {#place-timerange-ad-markers-on-the-timeline}

Este ejemplo muestra la forma recomendada de incluir especificaciones de TimeRange en la cronología de reproducción.

1. Traducir la información de colocación de anuncios fuera de banda a una lista de `TimeRange` especificaciones (es decir, instancias del `TimeRange` class).
1. Utilice el conjunto de `TimeRange` especificaciones para rellenar una instancia de `TimeRangeCollection` clase.
1. Pase la instancia Metadatos, que se puede obtener del `TimeRangeCollection` ejemplo, a la `replaceCurrentItem` método (parte de la interfaz MediaPlayer).
1. Espere a que TVSDK realice la transición a `PREPARED` estado esperando a que `PlaybackEventListener#onPrepared` llamada de retorno que se va a activar.
1. Inicie la reproducción de vídeo llamando a `play()` método (parte del `MediaPlayer` interfaz).

* Gestión de conflictos de cronología: puede haber casos en los que algunos `TimeRange` las especificaciones se superponen en la cronología de reproducción. Por ejemplo, el valor de la posición inicial correspondiente a un `TimeRange` la especificación puede ser inferior al valor de la posición final que ya se ha colocado. En este caso, TVSDK ajusta silenciosamente la posición inicial del infractor `TimeRange` especificación para evitar conflictos de cronología. Mediante este ajuste, el nuevo `TimeRange` se hace más corto de lo especificado originalmente. Si el ajuste es tan extremo que llevaría a una `TimeRange` con una duración de cero ms, TVSDK descarta silenciosamente el elemento infractor `TimeRange` especificación.
* Cuándo `TimeRange` Cuando se proporcionan especificaciones para las pausas publicitarias personalizadas, TVSDK intenta traducirlas en anuncios que se agrupan dentro de las pausas publicitarias. TVSDK busca elementos adyacentes `TimeRange` las especificaciones y las agrupa en pausas publicitarias independientes. Si hay intervalos de tiempo que no son adyacentes a ningún otro intervalo de tiempo, se traducen en saltos de publicidad que contienen un solo anuncio.
* Se da por hecho que el elemento del reproductor de contenidos que se está cargando apunta a un recurso de VOD. TVSDK comprueba esto cada vez que la aplicación intenta cargar un recurso multimedia cuyos metadatos contienen `TimeRange` especificaciones que solo se pueden utilizar en el contexto de la función de marcadores de publicidad personalizados. Si el recurso subyacente no es de tipo VOD, la biblioteca TVSDK genera una excepción.
* Cuando se trata de marcadores de publicidad personalizados, TVSDK desactiva otros mecanismos de resolución de anuncios (a través de Adobe Primetime ad decisioning (anteriormente conocido como Auditude) u otro sistema de aprovisionamiento de anuncios). Puede utilizar uno de los distintos módulos de resolución de anuncios que proporciona TVSDK o el mecanismo de marcadores de anuncio personalizado. Al utilizar la API personalizada de marcadores de publicidad, el contenido del anuncio se considera ya resuelto y se coloca en la cronología.

El siguiente fragmento de código proporciona un ejemplo sencillo en el que un conjunto de tres especificaciones TimeRange se colocan en la cronología como marcadores de anuncios personalizados.

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
