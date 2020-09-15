---
description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.
seo-description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.
seo-title: Controlar la posición y el tamaño de la vista de vídeo
title: Controlar la posición y el tamaño de la vista de vídeo
uuid: 2231c574-03cd-45a8-ab00-4a42f8e044f0
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Controlar la posición y el tamaño de la vista de vídeo{#control-the-position-and-size-of-the-video-view}

Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.

De forma predeterminada, TVSDK intenta mantener la proporción de aspecto de la vista de vídeo cada vez que cambia el tamaño o la posición del vídeo (debido a un cambio realizado por la aplicación, un cambio de perfil, un cambio de contenido, etc.).

Puede anular el comportamiento predeterminado de la relación de aspecto especificando una directiva *de* escala diferente. Especifique la directiva de escala mediante la `MediaPlayerView` propiedad del `scalePolicy` objeto. La directiva `MediaPlayerView`de escala predeterminada se establece con una instancia de la `MaintainAspectRatioScalePolicy` clase. Para restablecer la directiva de escala, reemplace la instancia predeterminada de `MaintainAspectRatioScalePolicy` on `MediaPlayerView.scalePolicy` por su propia directiva. (No se puede establecer la `scalePolicy` propiedad en un valor nulo).

1. Implemente la `MediaPlayerViewScalePolicy` interfaz para crear su propia directiva de escala.

   El `MediaPlayerViewScalePolicy` tiene un método:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK utiliza un `StageVideo` objeto para mostrar el vídeo y, como `StageVideo` los objetos no están en la lista de visualización, el `viewPort` parámetro contiene las coordenadas absolutas del vídeo.
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

1. Asigne la implementación a la `MediaPlayerView` propiedad.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Añada la vista a la propiedad `view` de Media Player.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Por ejemplo: Ajuste la escala del vídeo para rellenar toda la vista del vídeo sin mantener la proporción de aspecto:**

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

