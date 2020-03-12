---
description: Cree un PlaybackManager que gestione la configuración y la operación de reproducción del flujo HLS. No se requiere ninguna otra configuración.
seo-description: Cree un PlaybackManager que gestione la configuración y la operación de reproducción del flujo HLS. No se requiere ninguna otra configuración.
seo-title: Habilitar la reproducción de vídeo
title: Habilitar la reproducción de vídeo
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# Habilitar la reproducción de vídeo {#enable-video-playback}

Cree un PlaybackManager que gestione la configuración y la operación de reproducción del flujo HLS. No se requiere ninguna otra configuración.

1. Cree el objeto del reproductor multimedia asegurándose de que existe el siguiente código en [!DNL PlayerFragment.java]:

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. Cree el administrador de reproducción mediante el `ManagerFactory`:

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. Implemente el `PlaybackManagerEventListener` en el para `PlayerFragment` controlar los eventos de reproducción:

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. Registre el detector de eventos en el `PlayerFragment`:

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. Configure el recurso de vídeo:

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. Configure las operaciones de la barra de control en la `PlayerFragment`:

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## Documentación de API relacionada {#related-api-documentation}

* [Class PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)