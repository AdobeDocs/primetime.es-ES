---
description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
seo-description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
seo-title: Mostrar la duración, el tiempo actual y el tiempo restante del vídeo
title: Mostrar la duración, el tiempo actual y el tiempo restante del vídeo
uuid: 64536ba7-33a1-49f8-a947-5700e1e9c032
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Mostrar la duración, el tiempo actual y el tiempo restante del vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.

1. Espere a que el reproductor esté en el estado INICIALIZADO.
1. Recupere el tiempo actual del cursor de reproducción mediante la `MediaPlayer.currentTime` propiedad .

   Esto devuelve la posición actual del cursor de reproducción en la línea de tiempo virtual en milisegundos. El tiempo se calcula en relación con el flujo resuelto que puede contener varias instancias de contenido alternativo, como anuncios múltiples o pausas publicitarias que se dividen en el flujo principal. Para flujos en directo/lineal, el tiempo devuelto siempre está en el rango de la ventana de reproducción.

   ```
   function get currentTime():Number;
   ```

1. Recupere el rango de reproducción del flujo y determine la duración.
   1. Utilice la `mediaPlayer.playbackRange` propiedad para obtener el intervalo de tiempo de la línea de tiempo virtual.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analice el intervalo de tiempo usando `mediacore.utils.TimeRange`.
   1. Para determinar la duración, reste el inicio desde el final del rango.

      Esto incluye la duración del contenido adicional que se inserta en el flujo (anuncios).

      Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y la duración del contenido adicional que se inserta en el flujo (anuncios).

      Para un recurso lineal/activo, el rango representa el rango de la ventana de reproducción y este rango cambia durante la reproducción.

      TVSDK distribuye un `MediaPlayerItemEvent.ITEM_UPDATED` evento para indicar que el elemento de medios se ha actualizado y que sus atributos (incluido el intervalo de reproducción) se han actualizado.

1. Utilice los métodos disponibles en la clase `MediaPlayer` y la `HSlider` clase que están públicamente disponibles en el SDK de Flex para configurar los parámetros de la barra de búsqueda.

1. Utilice un temporizador para recuperar periódicamente la hora actual y actualizar el `SeekBar`.
