---
description: Cree una instancia de MediaPlayer y coloque una vista de la misma en un diseño de fotograma.
title: Configuración de MediaPlayer
exl-id: e8fb6527-154b-4f7e-a128-525b5a3b3474
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Configuración de MediaPlayer {#set-up-the-mediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor de Primetime) que puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de reproducción de vídeo.

Cree una instancia de MediaPlayer y coloque una vista de la misma en un diseño de fotograma.

1. Instanciar `MediaPlayer`, pasando un `android.content.Context` objeto al constructor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Proporcionar un diseño de marco ( `android.widget.FrameLayout`) para guardar un `ViewGroup` de `mediaPlayer`:

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

1. Colocar una vista de `mediaPlayer` dentro del diseño del marco:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>El `MediaPlayer` instancia ( `mediaPlayer`) ya está disponible y correctamente configurado para mostrar contenido de vídeo en la pantalla del dispositivo.
