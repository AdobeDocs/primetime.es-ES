---
description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.
title: Controlar la posición y el tamaño de la vista de vídeo
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Controlar la posición y el tamaño de la vista de vídeo{#control-the-position-and-size-of-the-video-view}

Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView.

TVSDK del explorador intenta mantener de forma predeterminada la relación de aspecto de la vista de vídeo siempre que el tamaño o la posición del vídeo se modifican debido a un cambio realizado por la aplicación, un conmutador de perfil, un conmutador de contenido, etc.

Puede anular el comportamiento de relación de aspecto predeterminado especificando un *política de escalado*. Especifique la política de escalado mediante la variable `MediaPlayerView` del objeto `scalePolicy` propiedad. La política de escala predeterminada de `MediaPlayerView` se configura con una instancia de `MaintainAspectRatioScalePolicy` clase. Para restablecer la política de escalado, sustituya la instancia predeterminada de `MaintainAspectRatioScalePolicy` el `MediaPlayerView.scalePolicy` con su propia política.

>[!IMPORTANT]
>
>No puede establecer el `scalePolicy` propiedad a un valor nulo.

## Situaciones de reserva que no sean de Flash {#non-flash-fallback-scenarios}

En escenarios de reserva que no son de Flash, para que la directiva de escala funcione correctamente, el elemento div de vídeo se proporciona en la variable `View` el constructor debe devolver valores distintos de cero para `offsetWidth` y `offsetHeight`. Para dar un ejemplo de función incorrecta, a veces cuando la anchura y la altura de los elementos div de vídeo no se establecen explícitamente en css, la variable `View` el constructor devuelve cero para `offsetWidth` o `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy tiene compatibilidad limitada con algunos exploradores, especialmente IE, Edge y Safari 9. En estos exploradores, la relación de aspecto nativa del vídeo no se puede cambiar. Sin embargo, la posición y las dimensiones del vídeo se aplicarán según la política de escala.

1. Implementación de `MediaPlayerViewScalePolicy` para crear su propia política de escalado.

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

1. Asigne la implementación a `MediaPlayerView` propiedad.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Añada la vista al reproductor multimedia `view` propiedad.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Por ejemplo: escale el vídeo para rellenar toda la vista de vídeo, sin mantener la proporción de aspecto:**

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
