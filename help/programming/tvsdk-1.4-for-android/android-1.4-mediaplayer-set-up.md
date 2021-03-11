---
description: La interfaz de MediaPlayer para Android encapsula la funcionalidad y el comportamiento de un reproductor multimedia.
title: Configuración de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Configuración de MediaPlayer {#set-up-the-mediaplayer}

La interfaz de MediaPlayer para Android encapsula la funcionalidad y el comportamiento de un reproductor multimedia.

TVSDK proporciona una implementación de la interfaz `MediaPlayer`, la clase `DefaultMediaPlayer`. Cuando necesite la funcionalidad de reproducción de vídeo, cree una instancia de `DefaultMediaPlayer`.

>[!TIP]
>
>Interactúe con la instancia `DefaultMediaPlayer` solo con los métodos expuestos por la interfaz `MediaPlayer`.

1. Cree una instancia de MediaPlayer con el método público de fábrica `DefaultMediaPlayer.create` , pasando un objeto de contexto de aplicación de Android de Java.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Llame a `MediaPlayer.getView` para obtener una referencia a la instancia `MediaPlayerView`.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Coloque la instancia `MediaPlayerView` en una instancia `FrameLayout`, que coloque el vídeo en la pantalla del dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

La instancia `MediaPlayer` ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.
