---
description: La interfaz de MediaPlayer para Android encapsula la funcionalidad y el comportamiento de un reproductor de contenidos.
title: Configuración de MediaPlayer
exl-id: 2698fe8d-0b73-4aad-9fee-55d034d8ca64
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Configuración de MediaPlayer {#set-up-the-mediaplayer}

La interfaz de MediaPlayer para Android encapsula la funcionalidad y el comportamiento de un reproductor de contenidos.

TVSDK proporciona una implementación de `MediaPlayer` interfaz, la `DefaultMediaPlayer` clase. Cuando necesite la funcionalidad de reproducción de vídeo, cree una instancia de `DefaultMediaPlayer`.

>[!TIP]
>
>Interacción con `DefaultMediaPlayer` solo con los métodos que expone la variable `MediaPlayer` interfaz.

1. Crear una instancia de MediaPlayer mediante el público `DefaultMediaPlayer.create` método de fábrica, pasar un objeto de contexto de aplicación Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Llamada `MediaPlayer.getView` para obtener una referencia a `MediaPlayerView` ejemplo.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Coloque el `MediaPlayerView` instancia en una `FrameLayout` , que coloca el vídeo en la pantalla del dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

El `MediaPlayer` La instancia de ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.
