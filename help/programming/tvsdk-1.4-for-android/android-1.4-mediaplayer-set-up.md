---
description: La interfaz de MediaPlayer para Android encapsula la funcionalidad y el comportamiento de un reproductor de medios.
seo-description: La interfaz de MediaPlayer para Android encapsula la funcionalidad y el comportamiento de un reproductor de medios.
seo-title: Configuración de MediaPlayer
title: Configuración de MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Configuración de MediaPlayer {#set-up-the-mediaplayer}

La interfaz de MediaPlayer para Android encapsula la funcionalidad y el comportamiento de un reproductor de medios.

TVSDK proporciona una implementación de la `MediaPlayer` interfaz, la `DefaultMediaPlayer` clase. Cuando necesite la funcionalidad de reproducción de vídeo, cree una instancia `DefaultMediaPlayer`.

>[!TIP]
>
>Interactúe con la `DefaultMediaPlayer` instancia únicamente con los métodos expuestos por la `MediaPlayer` interfaz.

1. Cree una instancia de MediaPlayer mediante el método público `DefaultMediaPlayer.create` de fábrica, pasando un objeto de contexto de aplicación Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Llamar `MediaPlayer.getView` para obtener una referencia a la `MediaPlayerView` instancia.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Coloque la `MediaPlayerView` instancia en una `FrameLayout` instancia, que coloca el vídeo en la pantalla del dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

La `MediaPlayer` instancia ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.
