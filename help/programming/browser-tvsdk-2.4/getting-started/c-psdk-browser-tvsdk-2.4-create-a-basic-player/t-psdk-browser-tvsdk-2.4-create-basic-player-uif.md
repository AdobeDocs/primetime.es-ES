---
description: 'null'
seo-description: 'null'
seo-title: Creación de un reproductor básico mediante la interfaz de usuario Framework
title: Creación de un reproductor básico mediante la interfaz de usuario Framework
uuid: d1a82dbb-1c05-4d0c-b6bc-e07cbede93cb
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 1%

---


# Crear un reproductor básico con la interfaz de usuario Framework{#create-a-basic-player-using-the-ui-framework}

Para crear un reproductor básico con la interfaz de usuario Framework:

1. Cree un `<div>` para su instancia de reproductor.

   Por ejemplo:

   ```
   <div id="video1" > 
    </div>
   ```

1. Cargue el reproductor.

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   Cuando se crea el reproductor, el elemento `<div>` especificado recibe una clase CSS de `ptp-main-video-div-style`. El DOM resultante aparece algo así:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Añada un control de interfaz de usuario.

   Por ejemplo, agregue una barra de control que aparezca cuando el ratón pase sobre el reproductor:

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   El DOM resultante aparece de la siguiente manera:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

El objeto que se devuelve al llamar a `ptp.videoPlayer()` proporciona un comportamiento que ajusta la API del reproductor de medios TVSDK y permite el control programático de la reproducción. Al realizar llamadas en la instancia del reproductor de medios, la interfaz de usuario se actualiza a sí misma según los eventos activados por el reproductor de medios:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
