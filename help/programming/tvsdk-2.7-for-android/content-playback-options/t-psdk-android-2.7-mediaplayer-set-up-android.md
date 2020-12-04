---
description: Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.
seo-description: Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.
seo-title: Configuración de MediaPlayer
title: Configuración de MediaPlayer
uuid: 49c3edb9-b6e2-49f8-b4aa-f230af7de6b0
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Configure MediaPlayer {#set-up-the-mediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime) que se puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de la reproducción de vídeo.

Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.

1. Cree una instancia `MediaPlayer`, pasando un objeto `android.content.Context` al constructor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Proporcione un diseño de marco ( `android.widget.FrameLayout`) para contener un `ViewGroup` de `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   A continuación se muestra el fragmento de código para crear `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Coloque una vista de `mediaPlayer` dentro del diseño de marco:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>La instancia `MediaPlayer` ( `mediaPlayer`) ahora está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.