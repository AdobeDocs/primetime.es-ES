---
description: 'null'
seo-description: 'null'
seo-title: Limitaciones y comportamiento del juego de trucos
title: Limitaciones y comportamiento del juego de trucos
uuid: 5b947075-eba0-45de-82d0-50b193f1ac83
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Limitaciones y comportamiento para el juego de trucos {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitaciones del modo de reproducción mediante trucos:

* La lista de reproducción maestra debe contener segmentos solo de iframe.

   En la pantalla solo se muestran los fotogramas clave de la pista Iframe.
* La pista de audio y los subtítulos cerrados están desactivados.
* La reproducción y la pausa están activadas.
* Puede salir del modo de reproducción mediante trucos a cualquier velocidad de reproducción permitida (reproducir o pausar).
* Cuando se incorporan publicidades en el flujo:

   * Puede ir a jugar con trucos solo mientras reproduce el contenido principal. Se envía un error si intenta cambiar a la reproducción incorrecta durante una pausa publicitaria.
   * Después de iniciar el modo de reproducción de trucos, se omiten los saltos de publicidad y no se activan eventos de publicidad.
   * La línea de tiempo expuesta por TVSDK al reproductor no se modifica aunque se omitan los saltos de publicidad.
   * El valor de tiempo actual salta hacia adelante (hacia delante rápidamente) o hacia atrás (en rebobinado rápido) con la duración de la pausa publicitaria omitida.

      Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante la reproducción mediante trucos. El reproductor puede rastrear el tiempo en relación únicamente con el contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir una publicidad.
   * El evento `MediaPlayerEvent.AD_BREAK_SKIPPED` se envía inmediatamente antes de que se omita una pausa publicitaria.

      El reproductor puede utilizar este evento para implementar la lógica personalizada relacionada con los saltos de publicidad omitidos.

   * Salir de la reproducción de trucos invoca la misma política de reproducción de anuncios que al salir de la búsqueda.

      Al igual que con la búsqueda, el comportamiento depende de si la política de reproducción de la aplicación es diferente de la predeterminada. El valor predeterminado es que la última pausa publicitaria omitida se reproduce en el punto en el que se sale del juego sucio.

