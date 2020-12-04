---
description: 'null'
seo-description: 'null'
seo-title: Inserción parcial de pausa publicitaria
title: Inserción parcial de pausa publicitaria
uuid: a81295b8-77fe-4475-a472-080ee7804d7a
translation-type: tm+mt
source-git-commit: fe9d7d1b2b23a70eb4e212de3d9bda47fc11d8f1
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# Inserción parcial de Ad-Break {#partial-ad-break-insertion}

Puede activar una experiencia de tipo TV para poder unirse en medio de un anuncio, en transmisiones en directo. La función de pausa de publicidad parcial le permite imitar una experiencia parecida a la de TV en la que, si el cliente inicio un flujo en directo dentro de un midroll, el inicio se producirá dentro de ese midroll. Es similar a cambiar a un canal de TV y los comerciales funcionan perfectamente.

Por ejemplo, si un usuario se une en medio de una pausa publicitaria de 90 segundos (tres anuncios de 30 segundos), 10 segundos después de la segunda publicidad (es decir, a los 40 segundos de la pausa publicitaria), sucederá lo siguiente:

* El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.
* Los rastreadores de anuncios para el anuncio reproducido parcialmente (el segundo anuncio) no se activan. Solo se activa el rastreador del tercer anuncio.

Este comportamiento no está habilitado de forma predeterminada. Para habilitar esta función en la aplicación, haga lo siguiente:

Active la preferencia para la inserción parcial de pausa publicitaria. Utilice el nuevo método `setPartialAdBreakPref` en la interfaz de MediaPlayer para activar esta función. Utilice el método `getPartialAdBreakPref` para buscar el estado actual de esta preferencia.

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

El anuncio previo, si está disponible, se reproduce y, a continuación, el contenido se reproduce desde el punto en directo emulando la experiencia de la televisión en directo.
