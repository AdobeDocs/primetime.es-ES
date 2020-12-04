---
description: TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo a petición (VOD) como en flujos en directo.
seo-description: TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo a petición (VOD) como en flujos en directo.
seo-title: Mostrar una barra de búsqueda con la posición de reproducción actual
title: Mostrar una barra de búsqueda con la posición de reproducción actual
uuid: f940b305-4893-4531-9a79-53670f5fd23f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Mostrar una barra de búsqueda con la posición de reproducción actual{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo a petición (VOD) como en flujos en directo.

>[!IMPORTANT]
>
>La búsqueda en un flujo en directo solo está permitida para DVR.

1. Configure las rellamadas para la búsqueda.

       La búsqueda es asincrónica, por lo que TVSDK distribuye los siguientes eventos relacionados con la búsqueda:
   
   * `SeekEvent.SEEK_BEGIN` - Buscar inicio.
   * `SeekEvent.SEEK_END` - Busque con éxito.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - reajustó la posición de búsqueda proporcionada por el usuario.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos están PREPARADOS, COMPLETADOS, PAUSADOS y REPRODUCIDOS.

1. Escuche el evento adecuado para ver cuándo el usuario está borrando.
1. Pase la posición de búsqueda solicitada (milisegundos) al método `MediaPlayer.seek`.

   ```
   function seek(position:Number):void;
   ```

   Solo puede buscar en la duración de búsqueda del recurso. Para vídeo a petición, la duración es de 0 a la duración del recurso.

   >[!TIP]
   >
   >Esto mueve el cursor de reproducción a una nueva posición en el flujo, pero la posición calculada final puede diferir de la posición de búsqueda especificada.

1. Espere a que TVSDK distribuya el evento `SeekEvent.SEEK_END`.
1. Recupere la posición de reproducción ajustada final mediante evento.actualPosition.

       Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. Pueden aplicarse varias reglas, entre ellas:
   
   * El comportamiento de reproducción se ve afectado si una búsqueda u otro cambio de posición termina en medio de una pausa publicitaria o omite los saltos publicitarios.
   * Si busca cerca de un límite de segmento, la posición de búsqueda se ajusta al principio del segmento.

1. Utilice la información de posición al mostrar una barra de búsqueda.
