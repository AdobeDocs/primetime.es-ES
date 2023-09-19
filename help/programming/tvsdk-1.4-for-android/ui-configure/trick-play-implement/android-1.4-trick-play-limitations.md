---
description: Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de juego con trucos.
title: Limitaciones y comportamiento para el juego de trucos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Limitaciones y comportamiento para el juego de trucos{#limitations-and-behavior-for-trick-play}

Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de juego con trucos.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Estas son las limitaciones del modo de juego con trucos:

* La lista de reproducción principal debe contener segmentos solo de I-frame. En la pantalla solo se muestran los fotogramas clave de la pista I-frame.
* La pista de audio y los subtítulos están desactivados.
* La lógica de velocidad de bits adaptable (ABR) está deshabilitada. TVSDK selecciona una velocidad de bits entre la velocidad más baja proporcionada y 800 kbps y utiliza esa velocidad durante toda la sesión de truco.
* La reproducción y la pausa están habilitadas.
* La búsqueda no está permitida. Para buscar, llame a `pause` para salir del modo de juego truco y luego llamar a `seek`.

* Puede pasar del modo de reproducción con trucos a cualquier velocidad de reproducción permitida (reproducción o pausa).
* Cuando los anuncios se incorporan al flujo:

   * Solo puedes ir a la reproducción con trucos mientras reproduces el contenido principal. Se envía un error si intenta cambiar a la reproducción con trucos durante una pausa publicitaria.
   * Después de iniciar el modo de reproducción con trucos, las pausas publicitarias se ignoran y no se activa ningún evento publicitario.
   * La cronología expuesta por TVSDK a la aplicación del reproductor no se modifica aunque se omitan las pausas publicitarias.
   * El valor de tiempo actual salta hacia adelante (hacia adelante rápido) o hacia atrás (hacia atrás rápido) con la duración de la pausa publicitaria omitida. Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante el juego de trucos. La aplicación de reproducción puede obtener el valor de hora local para realizar un seguimiento de la hora solo en relación con el contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir un anuncio.
   * El `MediaPlayerEvent.AD_BREAK_SKIPPED` el evento se envía inmediatamente antes de que se vaya a omitir una pausa publicitaria. El reproductor puede utilizar este evento para implementar una lógica personalizada relacionada con los saltos de publicidad omitidos.
   * La salida del juego de trucos invoca la misma política de reproducción de anuncios que al salir de la búsqueda.

     Por lo tanto, como en la búsqueda, el comportamiento depende de si la directiva de reproducción de la aplicación es diferente de la predeterminada. De forma predeterminada, la última pausa publicitaria omitida se reproduce en el punto en el que sale del modo de reproducción con trucos.
