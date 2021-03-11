---
title: Creación de un reproductor básico mediante el marco de IU
description: Creación de un reproductor básico mediante el marco de IU
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# Crear un reproductor básico con la interfaz de usuario Framework{#create-a-basic-player-using-the-ui-framework}

Para crear un reproductor básico con el marco de IU:

1. Cree un `<div>` para la instancia del reproductor.

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

   Cuando se crea el reproductor, el elemento `<div>` especificado recibe una clase CSS de `ptp-main-video-div-style`. El DOM resultante se muestra de esta manera:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Agregue un control de interfaz de usuario.

   Por ejemplo, agregue una barra de control que aparezca cuando el ratón se sitúa sobre el reproductor:

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

El objeto devuelto al llamar a `ptp.videoPlayer()` proporciona un comportamiento que ajusta la API del reproductor de medios TVSDK y permite el control programático de la reproducción. Cuando realiza llamadas en la instancia del reproductor de contenidos, la interfaz de usuario se actualiza a sí misma en función de los eventos activados por el reproductor de contenidos:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
