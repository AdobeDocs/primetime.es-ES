---
description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
title: Mostrar la duración, la hora actual y el tiempo restante del vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Mostrar la duración, la hora actual y el tiempo restante del vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.

1. Espere a que el reproductor esté en el estado INICIALIZADO.
1. Recupere el tiempo actual del cabezal de reproducción mediante la propiedad `MediaPlayer.currentTime` .

   Esto devuelve la posición actual del cabezal de reproducción en la cronología virtual en milisegundos. El tiempo se calcula en función del flujo resuelto que puede contener varias instancias de contenido alternativo, como varios anuncios o pausas publicitarias duplicados en el flujo principal. Para los flujos en directo/lineales, el tiempo devuelto siempre está en el intervalo de la ventana de reproducción.

   ```
   function get currentTime():Number;
   ```

1. Recupere el intervalo de reproducción de la emisión y determine la duración.
   1. Utilice la propiedad `mediaPlayer.playbackRange` para obtener el intervalo de tiempo de la cronología virtual.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analice el intervalo de tiempo con `mediacore.utils.TimeRange`.
   1. Para determinar la duración, reste el inicio desde el final del intervalo.

      Esto incluye la duración del contenido adicional que se inserta en la emisión (anuncios).

      Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y las duraciones del contenido adicional que se inserta en la emisión (anuncios).

      Para un recurso lineal/activo, el rango representa el intervalo de la ventana de reproducción y este intervalo cambia durante la reproducción.

      TVSDK envía un evento `MediaPlayerItemEvent.ITEM_UPDATED` para indicar que el elemento de medios se ha actualizado y que sus atributos (incluido el intervalo de reproducción) se han actualizado.

1. Utilice los métodos disponibles en las clases `MediaPlayer` y `HSlider` que están disponibles públicamente en el SDK para Flex para configurar los parámetros de la barra de búsqueda.

1. Utilice un temporizador para recuperar periódicamente la hora actual y actualizar el `SeekBar`.
