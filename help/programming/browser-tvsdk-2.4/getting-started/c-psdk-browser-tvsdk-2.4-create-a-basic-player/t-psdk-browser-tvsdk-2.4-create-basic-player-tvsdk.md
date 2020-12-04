---
description: Complete los siguientes pasos para crear un reproductor básico con el SDK TVSDK del explorador.
seo-description: Complete los siguientes pasos para crear un reproductor básico con el SDK TVSDK del explorador.
seo-title: Creación de un reproductor básico con TVSDK
title: Creación de un reproductor básico con TVSDK
uuid: ec15cf53-197f-4190-a6b2-600a57815390
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Crear un reproductor básico con TVSDK{#create-a-basic-player-using-tvsdk}

Complete los siguientes pasos para crear un reproductor básico con el SDK TVSDK del explorador.

1. Cree un nuevo directorio en el que podrá descargar los archivos comprimidos para el SDK del explorador.
1. Descargue TVSDK del explorador de Zendesk, descomprima los archivos y coloque la carpeta de marcos en el nuevo directorio.
1. Cree una plantilla HTML simple para el código con un `div` en ella.
1. Coloque esta plantilla en un archivo HTML en el directorio creado en el paso 1.

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

1. Añada las bibliotecas TVSDK del explorador en la sección head.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. Para la etiqueta body, agregue la sección `onLoad`.

   ```
   <body onload="startVideo()">
   ```

1. Inicio implementando la función `startVideo`.
1. Añada una etiqueta de script y cree la función `startVideo` en la etiqueta .

   Se supone que esto está en la sección del encabezado de la página.

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
   >Aquí es donde se utiliza el `div` que creó anteriormente.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Añada el oyente de evento del reproductor.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente el controlador de evento y colóquelo antes del oyente de agregar evento.

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

1. Cree una configuración vacía y reemplace el recurso.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. Cuando el reproductor esté en el estado INITIALIZADO, llame a `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. Una vez que el reproductor esté en el estado PREPARADO, llame a `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

