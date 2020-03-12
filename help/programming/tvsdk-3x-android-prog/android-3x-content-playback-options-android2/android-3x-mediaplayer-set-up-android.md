---
description: TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime) que se puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de la reproducción de vídeo.
seo-description: TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime) que se puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de la reproducción de vídeo.
seo-title: Configuración del reproductor de medios
title: Configuración del reproductor de medios
uuid: 1f672484-b340-4f92-8a47-dad4c9f3b3fc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Configuración del reproductor de medios {#set-up-the-media-player}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime) que se puede integrar con otros componentes de Primetime. También ofrece una serie de funciones diseñadas para maximizar la calidad de la reproducción de vídeo.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

Cree una instancia `MediaPlayer` y coloque una vista en un diseño de marco.

1. Crear una instancia `MediaPlayer`, pasando un `android.content.Context` objeto al constructor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Proporcione un diseño de marco ( `android.widget.FrameLayout`) para mantener un `ViewGroup` de `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >A continuación se muestra el fragmento de código que se va a crear `_viewGroup`.

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

   >[!NOTE]
   >
   >La `MediaPlayer` instancia ( `mediaPlayer`) ya está disponible y configurada correctamente para mostrar contenido de vídeo en la pantalla del dispositivo.