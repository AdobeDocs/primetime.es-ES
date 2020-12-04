---
description: Un objeto MediaPlayer encapsula el comportamiento y la funcionalidad de un reproductor de medios.
seo-description: Un objeto MediaPlayer encapsula el comportamiento y la funcionalidad de un reproductor de medios.
seo-title: Configuración de MediaPlayer
title: Configuración de MediaPlayer
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Configure MediaPlayer{#set-up-the-mediaplayer}

Un objeto MediaPlayer encapsula el comportamiento y la funcionalidad de un reproductor de medios.

1. Cree una instancia de `MediaPlayer` mediante lo siguiente:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Cree una instancia `MediaPlayerView`:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   donde `container` es el elemento destinatario `div` que contiene su `HTMLMediaElement`.

   Por ejemplo, en una página HTML:

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   Llamar:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Adjunte su instancia `MediaPlayerView` a su instancia `MediaPlayer`:

   ```js
   player.view = view;
   ```

1. Adjunte el elemento de controles personalizados `div` a la instancia de MediaPlayer.

   Por ejemplo, en HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Llamar:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

La instancia `MediaPlayer` ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.
