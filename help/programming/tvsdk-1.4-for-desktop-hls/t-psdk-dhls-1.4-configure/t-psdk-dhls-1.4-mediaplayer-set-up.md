---
description: La interfaz de MediaPlayer encapsula la funcionalidad y el comportamiento de un reproductor de contenidos.
title: Configuración de MediaPlayer
exl-id: eec51f3e-4779-4fb5-b735-d5be412de64e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Configuración de MediaPlayer {#set-up-the-mediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor Primetime) que puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en TVSDK, que tiene métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y establecer los botones para llamar a esos métodos de TVSDK. La interfaz de MediaPlayer encapsula la funcionalidad y el comportamiento de un reproductor de contenido.

TVSDK proporciona una única implementación de `MediaPlayer` interfaz: la clase DefaultMediaPlayer. Cuando necesite la funcionalidad de reproducción de vídeo, cree una instancia de `DefaultMediaPlayer`.

>[!NOTE]
>
>Interacción con `DefaultMediaPlayer` solo con los métodos expuestos por la variable `MediaPlayer` interfaz.

1. Crear una instancia de `MediaPlayerContext` uso de la aplicación cargada `authorizedFeatures` instancia de (consulte [Cargue el token firmado](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Crear una instancia de `MediaPlayer` usando el método public create factory, pasando un `MediaPlayerContext` objeto de contexto:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Devuelve un genérico `MediaPlayer` interfaz. 1. Cree una instancia de `MediaPlayerView` y especifique la instancia de StageVideo que se va a utilizar:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Asociar el `MediaPlayerView` con la vista recién creada:

   ```
   mediaPlayer.view = view;
   ```

1. Coloque el `MediaPlayerView` en la pantalla del dispositivo:

   ```
   container.addChild(view)
   ```

El `MediaPlayer` La instancia de ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.
