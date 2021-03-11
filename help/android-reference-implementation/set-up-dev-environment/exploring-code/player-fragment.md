---
description: En la clase PlayerFragment se edita el código para crear los administradores de funciones totalmente habilitados.
title: Fragmento del reproductor
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Fragmento del reproductor {#playerfragment}

En la clase PlayerFragment se edita el código para crear los administradores de funciones totalmente habilitados.

La clase `PlayerFragment` contiene todos los componentes de la interfaz de usuario, como `playerFrame`, `ControlBar`, `playerClickableAdFragment` y `adOverlay`.

Gestiona la inicialización de todos estos componentes, así como la creación del reproductor, la configuración de las vistas, la creación de administradores de funciones para el reproductor de contenidos, la gestión de eventos multimedia como reanudación, reproducción y pausa y el manejo de los oyentes de eventos para `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager` y `EntitlementManager`.

El archivo XML que incluye los parámetros de configuración para `PlayerFragment` es `res/layout/fragment_player.xml`.

Antes de crear los administradores de funciones, debe crear el reproductor de contenidos asegurándose de que el siguiente código se encuentra en el archivo `PlayerFragment.java` :

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
