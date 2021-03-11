---
description: Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de reproducción de trucos.
title: Limitaciones y comportamiento para el juego de trucos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Limitaciones y comportamiento para la reproducción de trucos{#limitations-and-behavior-for-trick-play}

Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de reproducción de trucos.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Estas son las limitaciones del modo de reproducción de trucos:

* La lista de reproducción maestra debe contener segmentos solo de marco I. En la pantalla solo se muestran los fotogramas clave de la pista de I-frame.
* La pista de audio y los subtítulos están desactivados.
* La lógica de velocidad de bits adaptable (ABR) está desactivada. TVSDK selecciona una velocidad de bits entre la velocidad más baja proporcionada y 800 kbps y la utiliza durante toda la sesión de reproducción asistida.
* La reproducción y la pausa están activadas.
* No se permite la llamada a otro punto del contenido. Para buscar, llame a `pause` para salir del modo de reproducción de trucos y luego llame a `seek`.

* Puede pasar del modo de reproducción de trucos a cualquier velocidad de reproducción permitida (reproducción o pausa).
* Cuando los anuncios se incorporan al flujo:

   * Puede ir a la reproducción trucada solo mientras reproduce el contenido principal. Se envía un error si intenta cambiar para engañar la reproducción durante una pausa publicitaria.
   * Después de iniciar el modo de reproducción de truco, se omiten las pausas publicitarias y no se activan eventos publicitarios.
   * La línea de tiempo expuesta por TVSDK a la aplicación del reproductor no se modifica aunque se omitan las pausas publicitarias.
   * El valor de tiempo actual salta hacia adelante (hacia delante) o hacia atrás (al rebobinar rápidamente) con la duración de la pausa publicitaria omitida. Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante la reproducción de trucos. La aplicación del reproductor puede obtener el valor de hora local para rastrear el tiempo en relación únicamente con el contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir un anuncio.
   * El evento `MediaPlayerEvent.AD_BREAK_SKIPPED` se envía inmediatamente antes de que se omita una pausa publicitaria. El reproductor puede utilizar este evento para implementar lógica personalizada relacionada con las pausas publicitarias omitidas.
   * Salir de la reproducción de trucos invoca la misma política de reproducción de anuncios que al salir de la llamada a otro punto del contenido.

      Por lo tanto, como en la búsqueda, el comportamiento depende de si la política de reproducción de la aplicación es diferente de la predeterminada. El valor predeterminado es que la última pausa publicitaria omitida se reproduce en el punto en el que se sale del modo de reproducción engañosa.

