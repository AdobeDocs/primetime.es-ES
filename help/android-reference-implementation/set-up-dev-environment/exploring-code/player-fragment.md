---
description: En la clase PlayerFragment es donde se edita el código para crear los administradores de características totalmente habilitados.
title: PlayerFragment
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
