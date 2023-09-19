---
title: Inserción de pausa publicitaria parcial
description: Inserción de pausa publicitaria parcial
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Inserción parcial de un salto de publicidad {#partial-ad-break-insertion}

Puede habilitar una experiencia similar a la de una TV de poder unirse en medio de un anuncio o en emisiones en directo. La función de pausa parcial para anuncios le permite imitar una experiencia similar a una TV en la que, si el cliente inicia una emisión en directo dentro de un midroll, esta se inicia dentro de ese midroll. Es similar a cambiar a un canal de TV y los anuncios se ejecutan sin problemas.

Por ejemplo, si un usuario se une en mitad de una pausa publicitaria de 90 segundos (tres anuncios de 30 segundos), 10 segundos en el segundo anuncio (es decir, a los 40 segundos en la pausa publicitaria), ocurrirá lo siguiente:

* El segundo anuncio se reproduce durante el tiempo restante (20 segundos), seguido del tercer anuncio.
* Los rastreadores de anuncios para el anuncio parcialmente reproducido (el segundo anuncio) no se activan. Solo se activa el rastreador del tercer anuncio.

Este comportamiento no está habilitado de forma predeterminada. Para habilitar esta función en su aplicación, haga lo siguiente:

Active la preferencia Inserción de pausa publicitaria parcial. Utilice el nuevo método `setPartialAdBreakPref` en la interfaz de MediaPlayer para activar esta función. Uso `getPartialAdBreakPref` para encontrar el estado actual de esta preferencia.

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

Se reproduce el anuncio previo a la emisión, si está disponible, y el contenido se reproduce desde el punto de vista en directo emulando la experiencia de la televisión en directo.
