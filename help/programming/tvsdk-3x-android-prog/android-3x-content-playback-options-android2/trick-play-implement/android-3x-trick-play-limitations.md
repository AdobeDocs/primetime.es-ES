---
title: Limitaciones y comportamiento para el juego de trucos
description: Limitaciones y comportamiento para el juego de trucos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Limitaciones y comportamiento para la reproducción de trucos {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitaciones para el modo de reproducción de trucos:

* La lista de reproducción maestra debe contener segmentos solo de iframe.

   En la pantalla solo se muestran los fotogramas clave de la pista de Iframe.
* La pista de audio y los subtítulos están desactivados.
* La reproducción y la pausa están activadas.
* Puede salir del modo de reproducción mediante trucos a cualquier velocidad de reproducción permitida (reproducción o pausa).
* Cuando los anuncios se incorporan al flujo:

   * Puede ir a la reproducción trucada solo mientras reproduce el contenido principal. Se envía un error si intenta cambiar para engañar la reproducción durante una pausa publicitaria.
   * Después de iniciar el modo de reproducción del truco, se omiten las pausas publicitarias y no se activan eventos publicitarios.
   * La línea de tiempo expuesta por TVSDK al reproductor no se modifica aunque se omitan las pausas publicitarias.
   * El valor de tiempo actual salta hacia adelante (hacia delante) o hacia atrás (al rebobinar rápidamente) con la duración de la pausa publicitaria omitida.

      Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante la reproducción de trucos. El reproductor puede rastrear el tiempo relativo solo al contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir un anuncio.
   * El evento `MediaPlayerEvent.AD_BREAK_SKIPPED` se envía inmediatamente antes de que se omita una pausa publicitaria.

      El reproductor puede utilizar este evento para implementar lógica personalizada relacionada con las pausas publicitarias omitidas.

   * Salir de la reproducción de trucos invoca la misma política de reproducción de anuncios que al salir de la llamada a otro punto del contenido.

      Al igual que con la búsqueda, el comportamiento depende de si la política de reproducción de la aplicación es diferente de la predeterminada. El valor predeterminado es que la última pausa publicitaria omitida se reproduce en el punto en el que sale de la reproducción engañosa.