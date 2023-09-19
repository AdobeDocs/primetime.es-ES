---
description: Complete los siguientes pasos para crear un reproductor básico con el TVSDK del explorador.
title: Creación de un reproductor básico con TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Creación de un reproductor básico con TVSDK{#create-a-basic-player-using-tvsdk}

Complete los siguientes pasos para crear un reproductor básico con el TVSDK del explorador.

1. Cree un nuevo directorio en el que pueda descargar los archivos comprimidos para el TVSDK del explorador.
1. Descargue Browser TVSDK de Zendesk, descomprima los archivos y coloque la carpeta de módulos en el nuevo directorio.
1. Cree una plantilla de HTML simple para el código con una `div` en ella.
1. Coloque esta plantilla en un archivo HTML en el directorio que creó en el paso 1.

   ```
   <!DOCTYPE html> 
   
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. Añada las bibliotecas del TVSDK del explorador en la sección del encabezado.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. Para la etiqueta body, añada el `onLoad` sección.

   ```
   <body onload="startVideo()">
   ```

1. Inicie la implementación de `startVideo` función.
1. Añada una etiqueta de script y cree la `startVideo` función en la etiqueta.

   Se supone que está en la sección de encabezado de la página.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. Cree el `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Cree el `MediaPlayerView`.

   >[!TIP]
   >
   >Aquí es donde la variable `div` que ha creado anteriormente se utiliza.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Añada el oyente de eventos del reproductor.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente el controlador de eventos y colóquelo antes de agregar el detector de eventos.

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
   
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   ```

1. Cree el `MediaResource`, que pasa el vínculo M3U8 (o mpd).

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. Cree una configuración vacía y sustituya el recurso.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. Cuando el reproductor esté en el estado INITIALIZED, invoque `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. Una vez que el reproductor esté en el estado PREPARADO, invoque a `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
