---
description: Este ejemplo muestra la forma recomendada de incluir marcadores de anuncios personalizados en la cronología de reproducción.
title: Coloque marcadores de anuncios personalizados en la cronología
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Coloque marcadores de anuncios personalizados en la cronología {#place-custom-ad-markers-on-the-timeline}

Este ejemplo muestra la forma recomendada de incluir marcadores de anuncios personalizados en la cronología de reproducción.

1. Traduzca la información de colocación de anuncios fuera de banda a una lista/matriz de la clase `RepaceTimeRange`.
1. Cree una instancia de la clase `CustomRangeMetadata` y utilice su método `setTimeRangeList` con la lista/matriz como argumento para establecer su lista de intervalos de tiempo.
1. Utilice su método `setType` para establecer el tipo en `MARK_RANGE`.
1. Utilice el método `MediaPlayerItemConfig.setCustomRangeMetadata` con la instancia `CustomRangeMetadata` como argumento para establecer los metadatos de intervalo personalizados.
1. Utilice el método `MediaPlayer.replaceCurrentResource` con la instancia `MediaPlayerItemConfig` como argumento para establecer que el nuevo recurso sea el actual.
1. Espere un evento `STATE_CHANGED`, que informa de que el reproductor está en el estado `PREPARED`.
1. Inicie la reproducción de vídeo llamando a `MediaPlayer.play`.

Este es el resultado de completar las tareas en este ejemplo:

* Si un `ReplaceTimeRange` se superpone con otro en la línea de tiempo de reproducción, por ejemplo, la posición inicial de un `ReplaceTimeRange` es anterior a una posición final ya colocada, TVSDK ajusta silenciosamente el inicio del `ReplaceTimeRange` infractor para evitar el conflicto.

   Esto hace que el `ReplaceTimeRange` ajustado sea más corto que el especificado originalmente. Si el ajuste lleva a una duración de cero, TVSDK descarta de forma silenciosa el `ReplaceTimeRange` infractor.

* TVSDK busca intervalos de tiempo adyacentes para pausas publicitarias personalizadas y los agrupa en pausas publicitarias independientes.

Los intervalos de tiempo que no son adyacentes a ningún otro intervalo de tiempo se traducen en pausas publicitarias que contienen un solo anuncio.

* Si la aplicación intenta cargar un recurso de medios cuya configuración contiene `CustomRangeMetadata` que solo puede utilizarse en los marcadores de anuncios personalizados de contexto, TVSDK genera una excepción si el recurso subyacente no es del tipo VOD.

* Cuando se trata de marcadores de anuncios personalizados, TVSDK desactiva otros mecanismos de resolución de anuncios (por ejemplo, Adobe Primetime y toma de decisiones).

   Puede utilizar cualquier módulo TVSDK de resolución de anuncios o el mecanismo de marcadores de anuncios personalizados. Cuando se utilizan marcadores de anuncios personalizados, el contenido de la publicidad se considera resuelto y se coloca en la cronología.

El siguiente fragmento de código coloca tres intervalos de tiempo en la cronología como marcadores de anuncios personalizados.

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
