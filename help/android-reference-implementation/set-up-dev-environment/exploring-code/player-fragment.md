---
description: En la clase PlayerFragment es donde se edita el código para crear los administradores de características totalmente habilitados.
title: PlayerFragment
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# PlayerFragment {#playerfragment}

En la clase PlayerFragment es donde se edita el código para crear los administradores de características totalmente habilitados.

El `PlayerFragment` contiene todos los componentes de la interfaz de usuario, como `playerFrame`, `ControlBar`, `playerClickableAdFragment`, y `adOverlay`.

Gestiona la inicialización de todos estos componentes, así como la creación del reproductor, la configuración de las vistas, la creación de administradores de funciones para el reproductor de contenidos, la gestión de eventos de contenidos como reanudación, reproducción y pausa, y la gestión de los oyentes de eventos para `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager`, y `EntitlementManager`.

El archivo XML que incluye los parámetros de configuración para `PlayerFragment` es `res/layout/fragment_player.xml`.

Antes de crear los administradores de funciones, debe crear el reproductor de contenidos asegurándose de que el siguiente código se encuentra en `PlayerFragment.java` archivo:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
