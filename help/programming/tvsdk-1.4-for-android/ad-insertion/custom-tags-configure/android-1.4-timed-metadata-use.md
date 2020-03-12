---
description: Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con la hora de inicio.
seo-description: Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con la hora de inicio.
seo-title: Uso de metadatos temporizados
title: Uso de metadatos temporizados
uuid: 98bb8c08-2794-42d6-b5c3-b1047ac804fe
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Uso de metadatos temporizados {#use-timed-metadata}

Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con la hora de inicio.

Para utilizar estos objetos guardados `TimedMetadata` durante la reproducción, utilice los objetos de metadatos de tiempo guardados `ArrayList` desde la [tienda a medida que se distribuyen](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Ejecute un temporizador y consulte repetidamente el tiempo de reproducción actual.
1. Busque todos los `TimedMetadata` objetos con tiempos de inicio que coincidan con el tiempo de reproducción actual.

   Puede utilizar estos objetos para completar varias acciones.

[!IMPORTANT]
Cuando compruebe si el tiempo de reproducción actual coincide con algún `TimedMetadata` objeto, incluya `shouldTriggerSubscribedTagEvent` como condición.

La línea de tiempo puede cambiar como resultado de varios comportamientos publicitarios. Por ejemplo, es posible que uno o varios saltos de publicidad se muevan de sus posiciones originales en la línea de tiempo, pero `shouldTriggerSubscribedTagEvent` garantizan que el tiempo de inicio del `TimeMetadata` objeto coincida con el tiempo de reproducción actual.

Por ejemplo:

```java
 _playbackClockEventListener = new Clock.ClockEventListener() {
    @Override
    public void onTick(String name) {
        getActivity().runOnUiThread(new Runnable() {
            @Override
            public void run() {
                /* handle timedmetadata object list  */ 
                if (_mediaPlayer != null && _timedMetadataList != null && _timedMetadataList.size() > 0) {
                    if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) {
                        long localTime = _mediaPlayer.getLocalTime();
                        Iterator<TimedMetadata> iterator = _timedMetadataList.iterator(); 
                        while (iterator.hasNext()) {
                            TimedMetadata timedMetadata = iterator.next();
                            long diff = localTime - timedMetadata.getTime();
                            if (diff >= 0 &&
                                diff <= PLAYBACK_CLOCK_INTERVAL &&
                                _mediaPlayer.shouldTriggerSubscribedTagEvent()) {
                                // use timed metadata object
                            }
                        }
                    }
                }
            }
        });
    }
};
_playbackClock.addClockEventListener(_playbackClockEventListener);
```

1. Borre periódicamente `TimedMetadata` instancias antiguas de la lista para evitar que la memoria crezca continuamente.