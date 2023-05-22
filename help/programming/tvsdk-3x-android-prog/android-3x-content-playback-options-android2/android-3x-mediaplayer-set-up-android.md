---
description: TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor de Primetime) que puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de reproducción de vídeo.
title: Configuración del reproductor de contenidos
exl-id: 99fdc4c1-0c67-4de5-87a5-b42d76f43ae9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Configuración del reproductor de contenidos {#set-up-the-media-player}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor de Primetime) que puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de reproducción de vídeo.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

Crear una instancia de `MediaPlayer` y coloque una vista de él en un diseño de marco.

1. Instanciar `MediaPlayer`, pasando un `android.content.Context` objeto al constructor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Proporcionar un diseño de marco ( `android.widget.FrameLayout`) para guardar un `ViewGroup` de `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >A continuación se muestra el fragmento de código para crear `_viewGroup`.

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

   >[!NOTE]
   >
   >El `MediaPlayer` instancia ( `mediaPlayer`) ya está disponible y correctamente configurado para mostrar contenido de vídeo en la pantalla del dispositivo.
