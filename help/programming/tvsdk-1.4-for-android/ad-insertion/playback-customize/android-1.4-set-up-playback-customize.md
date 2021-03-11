---
description: Puede personalizar o anular los comportamientos publicitarios.
title: Configuración de una reproducción personalizada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 1%

---


# Configuración de reproducción personalizada {#cset-up-customized-playback}

Puede personalizar o anular el comportamiento de la publicidad registrando la instancia de directiva de publicidad con TVSDK.

Para personalizar los comportamientos publicitarios, realice una de las siguientes acciones:

* Implemente la interfaz `AdPolicySelector` y todos sus métodos.
Se recomienda esta opción si necesita anular todos los comportamientos de publicidad predeterminados.

* Amplíe la clase `DefaultAdPolicySelector` y proporcione implementaciones solo para los comportamientos que requieren
personalización.
Esta opción se recomienda si necesita anular solo algunos de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

Para personalizar el comportamiento de los anuncios:

1. Implemente la interfaz AdPolicySelector y todos sus métodos.

1. Asigne la instancia de directiva que utilizará TVSDK a través de la fábrica de publicidad.

>[!IMPORTANT]
>
>Las políticas de publicidad personalizadas que se registran al principio de >reproducción se borran cuando la instancia de MediaPlayer está >desasignada.La aplicación debe registrar una instancia de directiva >selector cada vez que se cree una nueva sesión de reproducción.

Por ejemplo:

```
    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. Implemente sus personalizaciones.