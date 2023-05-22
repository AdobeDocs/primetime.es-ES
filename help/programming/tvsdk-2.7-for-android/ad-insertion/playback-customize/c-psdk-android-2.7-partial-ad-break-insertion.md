---
title: Inserción de pausa publicitaria parcial
description: Inserción de pausa publicitaria parcial
copied-description: true
exl-id: bcd4b108-9b91-479e-8147-ec4d24862e37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Inserción de pausa publicitaria parcial {#partial-ad-break-insertion}

Puede habilitar una experiencia similar a la de una TV de poder unirse en medio de un anuncio o en emisiones en directo. La función de pausa parcial para anuncios le permite imitar una experiencia similar a una TV en la que, si el cliente inicia una emisión en directo dentro de un midroll, esta se inicia dentro de ese midroll. Es similar a cambiar a un canal de TV y los anuncios se ejecutan sin problemas.

Por ejemplo, si un usuario se une en mitad de una pausa publicitaria de 90 segundos (tres anuncios de 30 segundos), 10 segundos en el segundo anuncio (es decir, a los 40 segundos en la pausa publicitaria), ocurrirá lo siguiente:

* El segundo anuncio se reproduce durante el tiempo restante (20 segundos), seguido del tercer anuncio.
* Los rastreadores de anuncios para el anuncio parcialmente reproducido (el segundo anuncio) no se activan. Solo se activa el rastreador del tercer anuncio.

Este comportamiento no está habilitado de forma predeterminada. Para habilitar esta función en su aplicación, haga lo siguiente:

1. Deshabilite los prerolls activos, utilizando el método setEnableLivePreroll de la clase AdvertisingMetadata.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Active la preferencia Inserción de pausa publicitaria parcial. Utilice el nuevo método setPartialAdBreakPref en la interfaz de MediaPlayer para activar esta función. Utilice el método getPartialAdBreakPref para buscar el estado actual de esta preferencia.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```
