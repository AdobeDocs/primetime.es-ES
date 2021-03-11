---
description: Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con la hora de inicio.
title: Usar metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%

---


# Usar metadatos temporizados {#use-timed-metadata}

Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con la hora de inicio.

Para utilizar estos `TimedMetadata` objetos guardados durante la reproducción, utilice los `ArrayList` guardados de [Almacenar objetos de metadatos temporizados a medida que se envían](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Ejecute un temporizador y consulte repetidamente el tiempo de reproducción actual.
1. Busque todos los objetos `TimedMetadata` con tiempos de inicio que coincidan con el tiempo de reproducción actual.

   Puede utilizar estos objetos para completar varias acciones.

   >[!IMPORTANT]
   >
   >Cuando compruebe si el tiempo de reproducción actual coincide con cualquier objeto `TimedMetadata`, incluya `shouldTriggerSubscribedTagEvent` como condición.

   La cronología puede cambiar como resultado de varios comportamientos publicitarios. Por ejemplo, es posible que se muevan una o más pausas publicitarias de sus posiciones originales en la cronología, pero `shouldTriggerSubscribedTagEvent` garantiza que la hora de inicio del objeto `TimeMetadata` coincida con la hora de reproducción actual.

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

1. Elimine periódicamente instancias `TimedMetadata` obsoletas de la lista para evitar que la memoria crezca continuamente.