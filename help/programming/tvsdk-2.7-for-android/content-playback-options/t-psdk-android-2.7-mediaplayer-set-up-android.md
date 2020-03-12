---
description: Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.
seo-description: Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.
seo-title: Configuración de MediaPlayer
title: Configuración de MediaPlayer
uuid: 49c3edb9-b6e2-49f8-b4aa-f230af7de6b0
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Configuración de MediaPlayer {#set-up-the-mediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime) que se puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de la reproducción de vídeo.

Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.

1. Crear una instancia `MediaPlayer`, pasando un `android.content.Context` objeto al constructor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Proporcione un diseño de marco ( `android.widget.FrameLayout`) para mantener un `ViewGroup` de `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   A continuación se muestra el fragmento de código que se va a crear `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Coloque una vista del interior del `mediaPlayer` diseño de marco:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>La `MediaPlayer` instancia ( `mediaPlayer`) ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.