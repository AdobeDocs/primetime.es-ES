---
description: Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con el tiempo de inicio.
title: Usar metadatos cronometrados
exl-id: 7f87cd14-121a-4543-ab0a-a03d829d040b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Usar metadatos cronometrados {#use-timed-metadata}

Puede utilizar TimedMetadata cuando el tiempo de reproducción actual coincida con el tiempo de inicio.

Para utilizar estos elementos guardados `TimedMetadata` durante la reproducción, utilice el elemento guardado `ArrayList` de [Almacenar objetos de metadatos cronometrados a medida que se envían](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Ejecute un temporizador y consulte repetidamente el tiempo de reproducción actual.
1. Buscar todos los `TimedMetadata` objetos con tiempos de inicio que coinciden con el tiempo de reproducción actual.

   Puede utilizar estos objetos para completar varias acciones.

   >[!IMPORTANT]
   >
   >Al comprobar si el tiempo de reproducción actual coincide con alguno `TimedMetadata` objetos, include `shouldTriggerSubscribedTagEvent` como condición.

   La cronología puede cambiar como resultado de varios comportamientos publicitarios. Por ejemplo, una o más pausas publicitarias podrían moverse desde sus posiciones originales en la cronología, pero `shouldTriggerSubscribedTagEvent` garantiza que la `TimeMetadata` La hora de inicio del objeto coincide con el tiempo de reproducción actual.

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

1. Vaciar periódicamente objetos antiguos `TimedMetadata` instancias de la lista para evitar que la memoria crezca continuamente.
