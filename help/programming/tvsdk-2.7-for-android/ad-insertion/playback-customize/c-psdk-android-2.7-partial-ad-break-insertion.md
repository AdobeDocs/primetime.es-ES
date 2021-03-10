---
title: Inserción parcial de pausa publicitaria
description: Inserción parcial de pausa publicitaria
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Inserción parcial de pausa publicitaria {#partial-ad-break-insertion}

Puede activar una experiencia parecida a la TV para poder unirse en medio de un anuncio, en transmisiones en directo. La función Parcial de pausa publicitaria le permite imitar una experiencia parecida a un televisor en la que, si el cliente inicia un flujo en vivo dentro de un midroll, este se iniciará dentro de ese midroll. Es similar a cambiar a un canal de televisión y los anuncios se ejecutan sin problemas.

Por ejemplo, si un usuario se une en medio de una pausa publicitaria de 90 segundos (tres anuncios de 30 segundos), 10 segundos después del segundo anuncio (es decir, a los 40 segundos de la pausa publicitaria), sucederá lo siguiente:

* El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.
* Los rastreadores de anuncios para el anuncio reproducido parcialmente (el segundo anuncio) no se activan. Solo se activa el rastreador del tercer anuncio.

Este comportamiento no está habilitado de forma predeterminada. Para habilitar este funcionamiento en la aplicación, haga lo siguiente:

1. Deshabilite las preconfiguraciones activas mediante el método setEnableLivePreroll de la clase AdvertisingMetadata .

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Active la preferencia para la inserción parcial de pausa publicitaria. Utilice el nuevo método setPartialAdBreakPref en la interfaz de MediaPlayer para activar esta función. Utilice el método getPartialAdBreakPref para encontrar el estado actual de esta preferencia.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```

