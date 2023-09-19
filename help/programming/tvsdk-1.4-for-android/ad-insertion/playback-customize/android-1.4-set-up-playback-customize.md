---
description: Puede personalizar o anular los comportamientos de los anuncios.
title: Configuración de la reproducción personalizada
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Configuración de la reproducción personalizada {#cset-up-customized-playback}

Puede personalizar o anular el comportamiento del anuncio registrando la instancia de directiva de publicidad con TVSDK.

Para personalizar los comportamientos de los anuncios, realice una de las siguientes acciones:

* Implementación de `AdPolicySelector` y todos sus métodos.
Esta opción se recomienda si necesita anular todos los comportamientos de publicidad predeterminados.

* Ampliación de la `DefaultAdPolicySelector` y proporcionan implementaciones solo para los comportamientos que requieren personalización.
Esta opción se recomienda si solo necesita anular algunos de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

Para personalizar los comportamientos de los anuncios:

1. Implemente la interfaz AdPolicySelector y todos sus métodos.

1. Asigne la instancia de directiva que utilizará TVSDK a través de la fábrica de publicidad.

>[!IMPORTANT]
>
>Las políticas de publicidad personalizadas que se registran al principio de >reproducción se borran cuando se >desasigna la instancia de MediaPlayer. La aplicación debe registrar una instancia de directiva >selector cada vez que se cree una nueva sesión de reproducción.

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

1. Implementar las personalizaciones.
