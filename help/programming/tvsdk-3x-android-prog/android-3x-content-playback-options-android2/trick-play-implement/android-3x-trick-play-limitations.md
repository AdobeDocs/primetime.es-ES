---
title: Limitaciones y comportamiento para el juego de trucos
description: Limitaciones y comportamiento para el juego de trucos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Limitaciones y comportamiento para el juego de trucos {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitaciones para el modo de juego con trucos:

* La lista de reproducción principal debe contener segmentos solo de Iframe.

  En la pantalla solo se muestran los fotogramas clave de la pista Iframe.
* La pista de audio y los subtítulos están desactivados.
* La reproducción y la pausa están habilitadas.
* Puede salir del modo truco-reproducción a cualquier velocidad de reproducción permitida (reproducción o pausa).
* Cuando los anuncios se incorporan al flujo:

   * Solo puedes ir a la reproducción con trucos mientras reproduces el contenido principal. Se envía un error si intenta cambiar a la reproducción con trucos durante una pausa publicitaria.
   * Después de iniciar el modo de reproducción con trucos, las pausas publicitarias se omiten y no se activa ningún evento publicitario.
   * La cronología expuesta por TVSDK al reproductor no se modifica aunque se omitan las pausas publicitarias.
   * El valor de tiempo actual salta hacia adelante (hacia adelante rápido) o hacia atrás (hacia atrás rápido) con la duración de la pausa publicitaria omitida.

     Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante el juego de trucos. El reproductor solo puede realizar el seguimiento del tiempo en relación con el contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir un anuncio.
   * El `MediaPlayerEvent.AD_BREAK_SKIPPED` el evento se envía inmediatamente antes de que se vaya a omitir una pausa publicitaria.

     El reproductor puede utilizar este evento para implementar una lógica personalizada relacionada con los saltos de publicidad omitidos.

   * La salida del juego de trucos invoca la misma política de reproducción de anuncios que al salir de la búsqueda.

     Al igual que con la búsqueda, el comportamiento depende de si la directiva de reproducción de la aplicación es diferente de la predeterminada. De forma predeterminada, la última pausa publicitaria omitida se reproduce en el punto en el que sale de la reproducción con trucos.
