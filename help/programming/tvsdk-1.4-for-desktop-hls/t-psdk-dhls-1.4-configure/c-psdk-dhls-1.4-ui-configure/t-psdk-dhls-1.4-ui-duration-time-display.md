---
description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
title: Mostrar la duración, el tiempo actual y el tiempo restante del vídeo
exl-id: 490bfa22-6df6-44a3-8e0d-9bb5939ae881
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Mostrar la duración, el tiempo actual y el tiempo restante del vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.

1. Espere a que su reproductor esté en el estado INICIALIZADO.
1. Recupere el tiempo del cabezal de reproducción actual utilizando `MediaPlayer.currentTime` propiedad.

   Devuelve la posición actual del cabezal de reproducción en la cronología virtual en milisegundos. El tiempo se calcula en relación con el flujo resuelto que puede contener varias instancias de contenido alternativo, como varios anuncios o pausas publicitarias empalmadas en el flujo principal. Para los flujos en directo/lineales, el tiempo devuelto siempre está en el intervalo de la ventana de reproducción.

   ```
   function get currentTime():Number;
   ```

1. Recupere el rango de reproducción de la emisión y determine la duración.
   1. Utilice el `mediaPlayer.playbackRange` para obtener el intervalo de tiempo de la escala de tiempo virtual.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analice el intervalo de tiempo mediante `mediacore.utils.TimeRange`.
   1. Para determinar la duración, reste el inicio desde el final del intervalo.

      Esto incluye la duración del contenido adicional que se inserta en el flujo (anuncios).

      Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y las duraciones del contenido adicional que se inserta en el flujo (anuncios).

      Para un recurso lineal/activo, el rango representa el intervalo de la ventana de reproducción y este intervalo cambia durante la reproducción.

      TVSDK envía un `MediaPlayerItemEvent.ITEM_UPDATED` para indicar que el elemento de medios se actualizó y que sus atributos (incluido el intervalo de reproducción) se actualizaron.

1. Utilice los métodos disponibles en la `MediaPlayer` y el `HSlider` que está disponible públicamente en el SDK de Flex para configurar los parámetros de la barra de búsqueda.

1. Utilice un temporizador para recuperar periódicamente la hora actual y actualizar el `SeekBar`.
