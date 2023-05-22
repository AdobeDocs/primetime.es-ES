---
description: Este ejemplo muestra la forma recomendada de incluir marcadores de publicidad personalizados en la cronología de reproducción.
title: Colocar marcadores de publicidad personalizados en la cronología
exl-id: 32a4b342-1f26-42c5-9682-789c541f0fa6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Colocar marcadores de publicidad personalizados en la cronología {#place-custom-ad-markers-on-the-timeline}

Este ejemplo muestra la forma recomendada de incluir marcadores de publicidad personalizados en la cronología de reproducción.

1. Traducir la información de colocación de anuncios fuera de banda a una lista o matriz de `RepaceTimeRange` clase.
1. Cree una instancia de `CustomRangeMetadata` y utilice su `setTimeRangeList` con la lista/matriz como argumento para establecer su lista de intervalo de tiempo.
1. Utilice su `setType` método para establecer el tipo en `MARK_RANGE`.
1. Utilice el `MediaPlayerItemConfig.setCustomRangeMetadata` con el método `CustomRangeMetadata` como argumento para establecer los metadatos del intervalo personalizado.
1. Utilice el `MediaPlayer.replaceCurrentResource` con el método `MediaPlayerItemConfig` como su argumento para establecer, convierta el nuevo recurso en el actual.
1. Espere un momento `STATE_CHANGED` evento, que informa de que el reproductor está en la `PREPARED` estado.
1. Iniciar reproducción de vídeo llamando a `MediaPlayer.play`.

Este es el resultado de completar las tareas de este ejemplo:

* Si un `ReplaceTimeRange` se solapa con otra en la cronología de reproducción como, por ejemplo, la posición inicial de un objeto `ReplaceTimeRange` es anterior a una posición final ya colocada, TVSDK ajusta silenciosamente el inicio de la infracción `ReplaceTimeRange` para evitar el conflicto.

   Esto hace que el ajuste `ReplaceTimeRange` más corta de lo especificado originalmente. Si el ajuste conduce a una duración de cero, TVSDK descarta silenciosamente el elemento infractor `ReplaceTimeRange`.

* TVSDK busca intervalos de tiempo adyacentes para las pausas publicitarias personalizadas y las agrupa en pausas publicitarias independientes.

Los intervalos de tiempo que no sean adyacentes a ningún otro intervalo de tiempo se traducen en pausas publicitarias que contienen un solo anuncio.

* Si la aplicación intenta cargar un recurso multimedia cuya configuración contiene `CustomRangeMetadata` que solo se puede utilizar en los marcadores de publicidad personalizados de contexto, TVSDK genera una excepción si el recurso subyacente no es de tipo VOD.

* Al tratar con marcadores de anuncios personalizados, TVSDK desactiva otros mecanismos de resolución de anuncios (por ejemplo, Adobe Primetime ad decisioning).

   Puede utilizar cualquier módulo de resolución de anuncios de TVSDK o el mecanismo de marcadores de publicidad personalizados. Cuando se utilizan marcadores de anuncio personalizados, el contenido del anuncio se considera resuelto y se coloca en la cronología.

El siguiente fragmento de código coloca tres intervalos de tiempo en la cronología como marcadores de anuncio personalizados.

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
