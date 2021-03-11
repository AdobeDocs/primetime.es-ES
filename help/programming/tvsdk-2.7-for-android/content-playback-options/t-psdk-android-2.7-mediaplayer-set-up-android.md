---
description: Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.
title: Configuración de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configuración de MediaPlayer {#set-up-the-mediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime) que se puede integrar con otros componentes de Primetime. También proporciona varias funciones diseñadas para maximizar la calidad de la reproducción de vídeo.

Cree una instancia de MediaPlayer y coloque una vista de ella en un diseño de marco.

1. Cree una instancia de `MediaPlayer`, pasando un objeto `android.content.Context` al constructor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Proporcione un diseño de marco ( `android.widget.FrameLayout`) para contener `ViewGroup` de `mediaPlayer`:

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

>La instancia `MediaPlayer` ( `mediaPlayer`) ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.