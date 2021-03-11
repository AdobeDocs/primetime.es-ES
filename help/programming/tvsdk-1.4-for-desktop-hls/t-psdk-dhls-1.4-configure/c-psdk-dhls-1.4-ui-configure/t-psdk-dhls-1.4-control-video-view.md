---
description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView .
title: Controlar la posición y el tamaño de la vista de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Controlar la posición y el tamaño de la vista de vídeo{#control-the-position-and-size-of-the-video-view}

Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView .

De forma predeterminada, TVSDK intenta mantener la proporción de aspecto de la vista de vídeo siempre que cambie el tamaño o la posición del vídeo (debido a un cambio realizado por la aplicación, o por un conmutador de perfil, o un conmutador de contenido, etc.).

Puede anular el comportamiento predeterminado de relación de aspecto especificando una *directiva de escala* diferente. Especifique la directiva de escala utilizando la propiedad `MediaPlayerView` del objeto `scalePolicy`. La directiva de escala predeterminada de `MediaPlayerView` se establece con una instancia de la clase `MaintainAspectRatioScalePolicy`. Para restablecer la directiva de escala, sustituya la instancia predeterminada de `MaintainAspectRatioScalePolicy` en `MediaPlayerView.scalePolicy` por su propia directiva. (No se puede establecer la propiedad `scalePolicy` en un valor nulo).

1. Implemente la interfaz `MediaPlayerViewScalePolicy` para crear su propia directiva de escala.

   El `MediaPlayerViewScalePolicy` tiene un método:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK utiliza un objeto `StageVideo` para mostrar el vídeo y, como los objetos `StageVideo` no están en la lista de visualización, el parámetro `viewPort` contiene las coordenadas absolutas del vídeo.
   >
   >
   >Por ejemplo:
   >
   >
   ```
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >       /** 
   >         * Default constructor. 
   >         */ 
   >       public function CustomScalePolicy() { 
   >       } 
   > 
   >    
      public function adjust(viewPort:Rectangle,  
   >                                                     videoWidth:Number,  
   >                                                     videoHeight:Number):Rectangle { 
   >               return customAdjustment(); 
   >       } 
   > 
   >    
      public function customAdjustment():Rectangle { 
   >               /* Your custom adjustment here */ 
   >               [...] 
   >       } 
   >}
   >```

1. Asigne la implementación a la propiedad `MediaPlayerView` .

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Agregue la vista a la propiedad `view` del reproductor de medios.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Por ejemplo: Escale el vídeo para rellenar toda la vista de vídeo, sin mantener la relación de aspecto:**

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```

