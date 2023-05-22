---
description: Un objeto MediaPlayer encapsula el comportamiento y la funcionalidad de un reproductor multimedia.
title: Configuración de MediaPlayer
exl-id: f492b2bb-3280-4306-ac4b-8b8d0fd68409
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Configuración de MediaPlayer{#set-up-the-mediaplayer}

Un objeto MediaPlayer encapsula el comportamiento y la funcionalidad de un reproductor multimedia.

1. Crear una instancia de `MediaPlayer` mediante lo siguiente:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Crear un `MediaPlayerView` instancia:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   donde `container` es el destinatario `div` elemento que contiene su `HTMLMediaElement`.

   Por ejemplo, en una página de HTML:

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   Llamada:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Adjunte su `MediaPlayerView` a su `MediaPlayer` instancia:

   ```js
   player.view = view;
   ```

1. Adjuntar los controles personalizados `div` a su instancia de MediaPlayer.

   Por ejemplo, en HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Llamada:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

El `MediaPlayer` La instancia de ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.
