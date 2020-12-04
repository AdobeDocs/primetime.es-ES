---
description: La interfaz de MediaPlayer encapsula la funcionalidad y el comportamiento de un reproductor de medios.
seo-description: La interfaz de MediaPlayer encapsula la funcionalidad y el comportamiento de un reproductor de medios.
seo-title: Configuración de MediaPlayer
title: Configuración de MediaPlayer
uuid: 4b27643c-9ccd-4abb-9793-475d06ee2a88
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Configure MediaPlayer {#set-up-the-mediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que se puede integrar con otros componentes de Primetime.

Utilice las herramientas de la plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en TVSDK, que dispone de métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y establecer los botones para llamar a esos métodos de TVSDK.La interfaz de MediaPlayer encapsula la funcionalidad y el comportamiento de un reproductor de medios.

TVSDK proporciona una implementación única de la interfaz `MediaPlayer`: la clase DefaultMediaPlayer. Cuando necesite la funcionalidad de reproducción de vídeo, cree una instancia `DefaultMediaPlayer`.

>[!NOTE]
>
>Interactúe con la instancia `DefaultMediaPlayer` sólo con los métodos expuestos por la interfaz `MediaPlayer`.

1. Cree una instancia `MediaPlayerContext` mediante la instancia `authorizedFeatures` cargada por la aplicación (consulte [Cargar el token firmado](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Cree una instancia de `MediaPlayer` mediante el método público create de fábrica, pasando un objeto de contexto `MediaPlayerContext`:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Esto devuelve una interfaz genérica `MediaPlayer`. 1. Cree una instancia de `MediaPlayerView` y especifique la instancia de StageVideo que se va a usar:

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