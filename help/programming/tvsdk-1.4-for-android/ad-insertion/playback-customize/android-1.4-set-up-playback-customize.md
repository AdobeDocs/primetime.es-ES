---
description: Puede personalizar o anular los comportamientos de publicidad.
seo-description: Puede personalizar o anular los comportamientos de publicidad.
seo-title: Configurar la reproducción personalizada
title: Configurar la reproducción personalizada
uuid: 9cbf0bcf-7932-409e-a690-e79f284eaf74
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Configurar la reproducción personalizada {#cset-up-customized-playback}

Puede personalizar o anular el comportamiento de la publicidad registrando la instancia de directiva de publicidad con TVSDK.

Para personalizar los comportamientos de las publicidades, realice una de las siguientes acciones:

* Implementar la `AdPolicySelector` interfaz y todos sus métodos.
Esta opción se recomienda si necesita anular todos los comportamientos de publicidad predeterminados.

* Amplíe la `DefaultAdPolicySelector` clase y proporcione implementaciones solo para los comportamientos que requieren repetición.
Esta opción se recomienda si necesita anular solo algunos de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

Para personalizar los comportamientos de publicidad:

1. Implementar la interfaz AdPolicySelector y todos sus métodos.

1. Asigne la instancia de directiva que usará TVSDK a través de la fábrica de publicidad.

>[!ATTENTION]
>
>Las directivas de publicidad personalizadas que se registran al principio de >reproducción se borran cuando la instancia de MediaPlayer está >desasignada.La aplicación debe registrar una instancia de directiva >selector cada vez que se cree una nueva sesión de reproducción.

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