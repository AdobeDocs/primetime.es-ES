---
description: Este ejemplo muestra la manera recomendada de incluir marcadores de publicidad personalizados en la línea de tiempo de reproducción.
seo-description: Este ejemplo muestra la manera recomendada de incluir marcadores de publicidad personalizados en la línea de tiempo de reproducción.
seo-title: Colocar marcadores de publicidad personalizados en la línea de tiempo
title: Colocar marcadores de publicidad personalizados en la línea de tiempo
uuid: 47e31a97-e5da-46f3-bdcc-327c159c4355
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Colocar marcadores de publicidad personalizados en la línea de tiempo {#place-custom-ad-markers-on-the-timeline}

Este ejemplo muestra la manera recomendada de incluir marcadores de publicidad personalizados en la línea de tiempo de reproducción.

1. Traduzca la información de posicionamiento de anuncios fuera de banda en una lista o matriz de `RepaceTimeRange` clase.
1. Cree una instancia de `CustomRangeMetadata` clase y utilice su `setTimeRangeList` método con la lista o matriz como argumento para establecer su lista de intervalos de tiempo.
1. Utilice su `setType` método para establecer el tipo en `MARK_RANGE`.
1. Utilice el `MediaPlayerItemConfig.setCustomRangeMetadata` método con la `CustomRangeMetadata` instancia como argumento para establecer los metadatos del rango personalizado.
1. Utilice el `MediaPlayer.replaceCurrentResource` método con la `MediaPlayerItemConfig` instancia como argumento para establecer que el nuevo recurso sea el recurso actual.
1. Espere a que se produzca un `STATE_CHANGED` evento que informe de que el reproductor está en el `PREPARED` estado.
1. Inicie la reproducción del vídeo llamando `MediaPlayer.play`.

Este es el resultado de completar las tareas en este ejemplo:

* Si un `ReplaceTimeRange` se superpone a otro en la línea de tiempo de reproducción, por ejemplo, la posición de inicio de un `ReplaceTimeRange` es anterior a una posición de finalización ya colocada, TVSDK ajusta silenciosamente el inicio de la infracción `ReplaceTimeRange` para evitar el conflicto.

   Esto hace que el ajuste sea `ReplaceTimeRange` más corto que el especificado originalmente. Si el ajuste da como resultado una duración de cero, TVSDK suprime de forma silenciosa la infracción `ReplaceTimeRange`.

* TVSDK busca intervalos de tiempo adyacentes para los saltos de publicidad personalizados y los agrupa en pausas de publicidad independientes.

Los intervalos de tiempo no adyacentes a ningún otro intervalo de tiempo se traducen en pausas publicitarias que contienen un solo anuncio.

* Si la aplicación intenta cargar un recurso de medios cuya configuración contiene `CustomRangeMetadata` que solo se puede usar en los marcadores de anuncios personalizados de contexto, TVSDK emite una excepción si el recurso subyacente no es de tipo VOD.

* Cuando se trata de marcadores de publicidad personalizados, TVSDK desactiva otros mecanismos de resolución de publicidad (por ejemplo, Adobe Primetime y decisiones).

   Puede utilizar cualquier módulo TVSDK de resolución de anuncios o el mecanismo de marcadores de anuncios personalizados. Cuando se utilizan marcadores de publicidad personalizados, el contenido de la publicidad se considera resuelto y se coloca en la línea de tiempo.

El siguiente fragmento de código coloca tres intervalos de tiempo en la línea de tiempo como marcadores de publicidad personalizados.
>```java>
>// Assume that the 3 time ranges are obtained through external means 
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
```>

