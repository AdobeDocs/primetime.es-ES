---
description: Este ejemplo muestra la forma recomendada de incluir especificaciones de TimeRange en la línea de tiempo de reproducción.
seo-description: Este ejemplo muestra la forma recomendada de incluir especificaciones de TimeRange en la línea de tiempo de reproducción.
seo-title: Colocar marcadores de anuncios de intervalo de tiempo en la línea de tiempo
title: Colocar marcadores de anuncios de intervalo de tiempo en la línea de tiempo
uuid: cbcc4c84-0d56-4331-b555-b8e59f7d52d4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Colocar marcadores de anuncios de intervalo de tiempo en la línea de tiempo {#place-timerange-ad-markers-on-the-timeline}

Este ejemplo muestra la forma recomendada de incluir especificaciones de TimeRange en la línea de tiempo de reproducción.

1. Traduzca la información de posicionamiento de anuncios fuera de banda en una lista de `TimeRange` especificaciones (es decir, instancias de la `TimeRange` clase).
1. Utilice el conjunto de `TimeRange` especificaciones para rellenar una instancia de la `TimeRangeCollection` clase.
1. Pase la instancia de metadatos, que se puede obtener de la `TimeRangeCollection` instancia, al `replaceCurrentItem` método (parte de la `MediaPlayer` interfaz).
1. Espere a que TVSDK pase al estado PREPARADO esperando a que se active la `PlaybackEventListener#onPrepared` llamada de retorno.
1. Inicie la reproducción del vídeo llamando al `play()` método (parte de la `MediaPlayer` interfaz).

* Gestión de conflictos de línea de tiempo: Puede haber casos en los que algunas `TimeRange` especificaciones se superponen en la línea de tiempo de reproducción. Por ejemplo, el valor de la posición inicial correspondiente a una `TimeRange` especificación puede ser inferior al valor de la posición final que ya se colocó. En este caso, TVSDK ajusta en silencio la posición inicial de la especificación que ocasiona el problema `TimeRange` para evitar conflictos de línea de tiempo. Mediante este ajuste, el nuevo `TimeRange` se acorta con respecto al especificado originalmente. Si el ajuste es tan extremo que conduciría a un `TimeRange` con una duración de cero ms, TVSDK descarta silenciosamente la especificación `TimeRange` ofensiva.

* Cuando se proporcionan `TimeRange` las especificaciones para las pausas publicitarias personalizadas, TVSDK intenta traducirlas en publicidades que se agrupan dentro de las pausas publicitarias. TVSDK busca especificaciones adyacentes y las agrupa en pausas publicitarias independientes. `TimeRange` Si hay intervalos de tiempo que no son adyacentes a ningún otro intervalo de tiempo, se traducen en pausas publicitarias que contienen un solo anuncio.

* Se da por hecho que el elemento del reproductor de medios que se está cargando apunta a un recurso de VOD. TVSDK lo comprueba cada vez que la aplicación intenta cargar un recurso multimedia cuyos metadatos contienen `TimeRange` especificaciones que solo se pueden usar en el contexto de la función de marcadores de publicidad personalizados. Si el recurso subyacente no es de tipo VOD, la biblioteca TVSDK emite una excepción.

* Cuando se trata de marcadores de publicidad personalizados, TVSDK desactiva otros mecanismos de resolución de publicidad (mediante Adobe Primetime y la toma de decisiones (anteriormente conocido como Auditude) u otro sistema de aprovisionamiento de anuncios). Puede utilizar uno de los distintos módulos de resolución de anuncios proporcionados por TVSDK o el mecanismo de marcadores de anuncios personalizados. Al utilizar la API de marcadores de publicidad personalizada, el contenido de la publicidad se considera ya resuelto y se coloca en la línea de tiempo.
>
><!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->


El siguiente fragmento de código proporciona un ejemplo sencillo donde se coloca un conjunto de tres `TimeRange` especificaciones en la línea de tiempo como marcadores de publicidad personalizados.

```
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
var timeRanges:TimeRangeCollection = new TimeRangeCollection(); 
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
  
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                             timeRanges.toMetadata(null));
```
