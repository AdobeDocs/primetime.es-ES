---
description: Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de reproducción mediante trucos.
seo-description: Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de reproducción mediante trucos.
seo-title: Limitaciones y comportamiento del juego de trucos
title: Limitaciones y comportamiento del juego de trucos
uuid: 0e84c9ef-fc18-4667-ad17-7f4777b552ba
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Limitaciones y comportamiento del juego de trucos{#limitations-and-behavior-for-trick-play}

Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de reproducción mediante trucos.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Estas son las limitaciones para el modo de reproducción mediante trucos:

* La lista de reproducción maestra debe contener segmentos solo de marco I. En la pantalla solo se muestran los fotogramas clave de la pista I-frame.
* La pista de audio y los subtítulos cerrados están desactivados.
* La lógica de velocidad de bits adaptable (ABR) está deshabilitada. TVSDK selecciona una velocidad de bits entre la velocidad más baja proporcionada y 800 kbps y la utiliza durante toda la sesión de reproducción mediante trucos.
* La reproducción y la pausa están activadas.
* No se permite la búsqueda. Para buscar, llame `pause` a salir del modo de reproducción de trucos y luego llame a `seek`.

* Puede pasar del modo de reproducción ficticia a cualquier velocidad de reproducción permitida (reproducir o pausar).
* Cuando se incorporan publicidades en el flujo:

   * Puede ir a jugar con trucos solo mientras reproduce el contenido principal. Se envía un error si intenta cambiar a la reproducción incorrecta durante una pausa publicitaria.
   * Después de comenzar el modo de reproducción de trucos, se omiten los saltos de publicidad y no se activa ningún evento de publicidad.
   * La línea de tiempo expuesta por TVSDK a la aplicación del reproductor no se modifica aunque se omitan los saltos de publicidad.
   * El valor de tiempo actual salta hacia adelante (hacia delante rápidamente) o hacia atrás (en rebobinado rápido) con la duración de la pausa publicitaria omitida. Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante la reproducción mediante trucos. La aplicación del reproductor puede obtener el valor de hora local para rastrear el tiempo en relación únicamente con el contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir una publicidad.
   * El `MediaPlayerEvent.AD_BREAK_SKIPPED` evento se envía inmediatamente antes de que se omita una pausa publicitaria. El reproductor puede utilizar este evento para implementar la lógica personalizada relacionada con los saltos de publicidad omitidos.
   * Salir de la reproducción de trucos invoca la misma política de reproducción de anuncios que al salir de la búsqueda.

      Por lo tanto, al igual que en la búsqueda, el comportamiento depende de si la política de reproducción de la aplicación es diferente de la predeterminada. El valor predeterminado es que la última pausa publicitaria omitida se reproduce en el punto en el que se sale del modo de reproducción ficticia.

