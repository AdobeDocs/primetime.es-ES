---
description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.
title: Controlar la posición y el tamaño de la vista de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Controlar la posición y el tamaño de la vista de vídeo{#control-the-position-and-size-of-the-video-view}

Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.

De forma predeterminada, TVSDK intenta mantener la relación de aspecto de la vista de vídeo siempre que cambia el tamaño o la posición del vídeo (debido a un cambio realizado por la aplicación, por un conmutador de perfil, por un conmutador de contenido, etc.).

Puede anular el comportamiento de relación de aspecto predeterminado especificando un *política de escalado*. Especifique la política de escalado mediante la variable `MediaPlayerView` del objeto `scalePolicy` propiedad. El `MediaPlayerView`La política de escalado predeterminada de se define con una instancia de `MaintainAspectRatioScalePolicy` clase. Para restablecer la política de escalado, sustituya la instancia predeterminada de `MaintainAspectRatioScalePolicy` el `MediaPlayerView.scalePolicy` con su propia política. (No se puede establecer el `scalePolicy` propiedad a un valor nulo).

1. Implementación de `MediaPlayerViewScalePolicy` para crear su propia política de escalado.

   El `MediaPlayerViewScalePolicy` tiene un método:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK utiliza un `StageVideo` para mostrar el vídeo y porque `StageVideo` Los objetos de no están en la lista de visualización. `viewPort` contiene las coordenadas absolutas del vídeo.
   >
   >
   >Por ejemplo:
   >
   >```
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
   >

1. Asigne la implementación a `MediaPlayerView` propiedad.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Añada la vista al reproductor multimedia `view` propiedad.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Por ejemplo: escale el vídeo para rellenar toda la vista de vídeo, sin mantener la proporción de aspecto:**

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
