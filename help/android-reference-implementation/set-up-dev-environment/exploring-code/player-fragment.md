---
description: En la clase PlayerFragment se edita el código para crear los administradores de funciones totalmente habilitados.
seo-description: En la clase PlayerFragment se edita el código para crear los administradores de funciones totalmente habilitados.
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

En la clase PlayerFragment se edita el código para crear los administradores de funciones totalmente habilitados.

La clase `PlayerFragment` contiene todos los componentes de la interfaz de usuario, como `playerFrame`, `ControlBar`, `playerClickableAdFragment` y `adOverlay`.

Gestiona la inicialización de todos estos componentes, así como la creación del reproductor, la configuración de las vistas, la creación de administradores de funciones para el reproductor de medios, la administración de eventos de medios como reanudar, reproducir y pausar y gestionar los oyentes de evento para `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager` y `EntitlementManager`.

El archivo XML que incluye los parámetros de configuración para `PlayerFragment` es `res/layout/fragment_player.xml`.

Antes de crear los administradores de funciones, debe crear el reproductor multimedia asegurándose de que el siguiente código esté en el archivo `PlayerFragment.java`:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
