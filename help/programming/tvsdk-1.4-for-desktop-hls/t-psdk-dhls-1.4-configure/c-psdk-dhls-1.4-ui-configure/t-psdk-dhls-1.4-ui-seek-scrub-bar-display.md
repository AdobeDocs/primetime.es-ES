---
description: TVSDK admite la búsqueda en una posición específica (tiempo) en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo bajo demanda (VOD) como en flujos en directo.
title: Mostrar una barra de desplazamiento de búsqueda con la posición de reproducción actual
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Mostrar una barra de desplazamiento de búsqueda con la posición de reproducción actual{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición específica (tiempo) en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo bajo demanda (VOD) como en flujos en directo.

>[!IMPORTANT]
>
>La búsqueda en un flujo en vivo solo está permitida para DVR.

1. Configure las llamadas de retorno para la búsqueda.

       La búsqueda es asíncrona, por lo que TVSDK envía los siguientes eventos relacionados con la búsqueda:
   
   * `SeekEvent.SEEK_BEGIN` - Busca empezar.
   * `SeekEvent.SEEK_END` - Búsqueda correcta.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - reajustó la posición de búsqueda proporcionada por el usuario.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARED, COMPLETED, PAUSED y PLAYING.

1. Escuche el evento correspondiente para ver cuándo está borrando el usuario.
1. Pase la posición de búsqueda solicitada (milisegundos) a `MediaPlayer.seek` método.

   ```
   function seek(position:Number):void;
   ```

   Solo puede buscar en la duración buscada del recurso. Para el vídeo bajo demanda, la duración es de 0 a la duración del recurso.

   >[!TIP]
   >
   >Esto mueve el cabezal de reproducción a una nueva posición en el flujo, pero la posición calculada final podría diferir de la posición de búsqueda especificada.

1. Espere a que TVSDK envíe el `SeekEvent.SEEK_END` evento.
1. Recupere la posición de reproducción ajustada final mediante event.actualPosition.

       Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. Se pueden aplicar varias reglas, entre ellas:
   
   * El comportamiento de reproducción se ve afectado si una búsqueda u otro cambio de posición termina en medio de una pausa publicitaria o omite las pausas publicitarias.
   * Si busca cerca de un límite de segmento, la posición de búsqueda se ajusta al principio del segmento.

1. Utilice la información de posición cuando se muestre una barra de desplazamiento de búsqueda.
