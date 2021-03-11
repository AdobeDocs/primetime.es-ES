---
description: La interfaz de MediaPlayer encapsula la funcionalidad y el comportamiento de un reproductor multimedia.
title: Configuración de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Configuración de MediaPlayer {#set-up-the-mediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor Primetime), que puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en TVSDK, que tiene métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y establecer los botones para llamar a esos métodos de TVSDK. La interfaz de MediaPlayer encapsula la funcionalidad y el comportamiento de un reproductor de contenidos.

TVSDK proporciona una sola implementación de la interfaz `MediaPlayer`: la clase DefaultMediaPlayer . Cuando necesite la funcionalidad de reproducción de vídeo, cree una instancia de `DefaultMediaPlayer`.

>[!NOTE]
>
>Interactúe con la instancia `DefaultMediaPlayer` solo con los métodos expuestos por la interfaz `MediaPlayer`.

1. Cree una instancia de `MediaPlayerContext` utilizando la instancia `authorizedFeatures` cargada por la aplicación (consulte [Load your signed token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Cree una instancia de `MediaPlayer` utilizando el método público create factory , pasando un objeto de contexto `MediaPlayerContext`:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Esto devuelve una interfaz genérica `MediaPlayer`. 1. Cree una instancia de `MediaPlayerView` y especifique la instancia de StageVideo que desea utilizar:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Asocie la instancia `MediaPlayerView` con la vista recién creada:

   ```
   mediaPlayer.view = view;
   ```

1. Coloque la instancia `MediaPlayerView` en la pantalla del dispositivo:

   ```
   container.addChild(view)
   ```

La instancia `MediaPlayer` ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.