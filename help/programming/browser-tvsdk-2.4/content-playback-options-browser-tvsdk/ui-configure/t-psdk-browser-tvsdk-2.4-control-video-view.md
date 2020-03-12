---
description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.
seo-description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.
seo-title: Controlar la posición y el tamaño de la vista de vídeo
title: Controlar la posición y el tamaño de la vista de vídeo
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Controlar la posición y el tamaño de la vista de vídeo{#control-the-position-and-size-of-the-video-view}

Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.

De forma predeterminada, el SDK del explorador intenta mantener la proporción de aspecto de la vista de vídeo siempre que el tamaño o la posición del vídeo cambie debido a un cambio realizado por la aplicación, un conmutador de perfil, un conmutador de contenido, etc.

Puede anular el comportamiento predeterminado de la relación de aspecto especificando una directiva *de* escala diferente. Especifique la directiva de escala mediante la `MediaPlayerView` propiedad del `scalePolicy` objeto. La directiva de escala predeterminada de `MediaPlayerView` se establece con una instancia de la `MaintainAspectRatioScalePolicy` clase. Para restablecer la directiva de escala, reemplace la instancia predeterminada de `MaintainAspectRatioScalePolicy` on `MediaPlayerView.scalePolicy` por su propia directiva.

>[!IMPORTANT]
>
>No se puede establecer la `scalePolicy` propiedad en un valor nulo.

## Escenarios de reserva que no son Flash {#non-flash-fallback-scenarios}

En los escenarios de reserva que no sean Flash, para que la política de escala funcione correctamente, el elemento div de vídeo proporcionado en el `View` constructor debe devolver valores distintos de cero para `offsetWidth` y `offsetHeight`. Para dar un ejemplo de función incorrecta, a veces cuando la anchura y la altura de los elementos div de vídeo no se establecen explícitamente en css, el `View` constructor devuelve cero para `offsetWidth` o `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy tiene compatibilidad limitada con algunos exploradores, como IE, Edge y Safari 9. Para estos exploradores, no se puede cambiar la proporción de aspecto nativo del vídeo. Sin embargo, la posición y las dimensiones del vídeo se aplicarán de acuerdo con la política de escala.

1. Implemente la `MediaPlayerViewScalePolicy` interfaz para crear su propia directiva de escala.

   El `MediaPlayerViewScalePolicy` tiene un método:

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   Por ejemplo:

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. Asigne la implementación a la `MediaPlayerView` propiedad.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Agregue la vista a la `view` propiedad de Media Player.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Por ejemplo: Ajuste la escala del vídeo para que ocupe toda la vista del vídeo sin mantener la proporción de aspecto:**

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```

