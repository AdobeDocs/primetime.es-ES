---
description: Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView .
title: Controlar la posición y el tamaño de la vista de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Controlar la posición y el tamaño de la vista de vídeo{#control-the-position-and-size-of-the-video-view}

Puede controlar la posición y el tamaño de la vista de vídeo mediante el objeto MediaPlayerView .

De forma predeterminada, el SDK de explorador intenta mantener la proporción de aspecto de la vista de vídeo siempre que el tamaño o la posición del vídeo se altere debido a un cambio realizado por la aplicación, un conmutador de perfil, un conmutador de contenido, etc.

Puede anular el comportamiento predeterminado de relación de aspecto especificando una *directiva de escala* diferente. Especifique la directiva de escala utilizando la propiedad `MediaPlayerView` del objeto `scalePolicy`. La directiva de escala predeterminada de `MediaPlayerView` se configura con una instancia de la clase `MaintainAspectRatioScalePolicy`. Para restablecer la directiva de escala, sustituya la instancia predeterminada de `MaintainAspectRatioScalePolicy` en `MediaPlayerView.scalePolicy` por su propia directiva.

>[!IMPORTANT]
>
>No se puede establecer la propiedad `scalePolicy` en un valor nulo.

## Situaciones de reserva que no son de Flash {#non-flash-fallback-scenarios}

En escenarios de reserva que no sean de Flash, para que la directiva de escala funcione correctamente, el elemento div de vídeo proporcionado en el constructor `View` debe devolver valores distintos de cero para `offsetWidth` y `offsetHeight`. Para dar un ejemplo de función incorrecta, a veces cuando la anchura y la altura de los elementos div de vídeo no se establecen explícitamente en css, el constructor `View` devuelve cero para `offsetWidth` o `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy tiene compatibilidad limitada para algunos exploradores, especialmente IE, Edge y Safari 9. En estos navegadores, no se puede cambiar la proporción de aspecto nativa del vídeo. Sin embargo, la posición y las dimensiones del vídeo se aplican según la política de escala.

1. Implemente la interfaz `MediaPlayerViewScalePolicy` para crear su propia directiva de escala.

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

1. Asigne la implementación a la propiedad `MediaPlayerView` .

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Agregue la vista a la propiedad `view` del reproductor de medios.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Por ejemplo: Escale el vídeo para rellenar toda la vista de vídeo, sin mantener la relación de aspecto:**

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

