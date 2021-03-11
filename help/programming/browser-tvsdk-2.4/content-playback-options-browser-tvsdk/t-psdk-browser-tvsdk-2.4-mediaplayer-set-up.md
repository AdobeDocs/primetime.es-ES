---
description: Un objeto MediaPlayer encapsula el comportamiento y la funcionalidad de un reproductor multimedia.
title: Configuración de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Configuración de MediaPlayer{#set-up-the-mediaplayer}

Un objeto MediaPlayer encapsula el comportamiento y la funcionalidad de un reproductor multimedia.

1. Cree una instancia de `MediaPlayer` mediante lo siguiente:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Cree una instancia `MediaPlayerView`:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   donde `container` es el elemento `div` de destino que contiene su `HTMLMediaElement`.

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

   Llamada:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Adjunte la instancia `MediaPlayerView` a la instancia `MediaPlayer`:

   ```js
   player.view = view;
   ```

1. Adjunte el elemento `div` de controles personalizados a la instancia de MediaPlayer.

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

La instancia `MediaPlayer` ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.
