---
title: Creación de un reproductor básico con el marco de IU
description: Creación de un reproductor básico con el marco de IU
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Creación de un reproductor básico con el marco de IU{#create-a-basic-player-using-the-ui-framework}

Para crear un reproductor básico con el marco de trabajo de IU:

1. Crear un `<div>` para la instancia de reproductor.

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

   Cuando se crea el reproductor, el especificado `<div>` recibe una clase CSS de `ptp-main-video-div-style`. El DOM resultante aparece de esta manera:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Agregue un control UI.

   Por ejemplo, añada una barra de control que aparezca cuando el ratón pase el ratón sobre el reproductor:

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

El objeto devuelto al llamar a `ptp.videoPlayer()` proporciona un comportamiento que envuelve la API del reproductor de contenidos de TVSDK y permite un control programático de la reproducción. Cuando realiza llamadas en la instancia del reproductor de contenido, la interfaz de usuario se actualiza a sí misma en función de los eventos activados por el reproductor de contenido:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
