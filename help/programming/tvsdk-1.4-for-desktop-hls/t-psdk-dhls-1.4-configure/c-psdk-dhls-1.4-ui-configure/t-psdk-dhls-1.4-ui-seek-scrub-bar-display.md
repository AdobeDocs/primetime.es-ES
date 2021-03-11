---
description: TVSDK admite la búsqueda en una posición específica (hora) en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo bajo demanda (VOD) como en emisiones en directo.
title: Mostrar una barra de desplazamiento con la posición de reproducción actual
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Mostrar una barra de depuración con la posición de reproducción actual{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición específica (hora) en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo bajo demanda (VOD) como en emisiones en directo.

>[!IMPORTANT]
>
>La llamada a otro sitio en directo solo está permitida para DVR.

1. Configure las llamadas de retorno para la búsqueda.

       La llamada a otro punto del contenido es asíncrona, por lo que TVSDK envía los siguientes eventos relacionados con la búsqueda:
   
   * `SeekEvent.SEEK_BEGIN` - Iniciando la llamada a otro punto del contenido.
   * `SeekEvent.SEEK_END` - Busque con éxito.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` : se ha reajustado la posición de búsqueda proporcionada por el usuario.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARADO, COMPLETADO, PAUSADO y REPRODUCIENDO.

1. Escuche el evento apropiado para ver cuándo el usuario está borrando.
1. Pase la posición de búsqueda solicitada (milisegundos) al método `MediaPlayer.seek` .

   ```
   function seek(position:Number):void;
   ```

   Solo puede buscar en la duración en la que puede buscar el recurso. Para el vídeo bajo demanda, la duración es de 0 a la duración del recurso.

   >[!TIP]
   >
   >Esto mueve el cabezal de reproducción a una nueva posición en el flujo, pero la posición calculada final puede diferir de la posición de búsqueda especificada.

1. Espere a que TVSDK distribuya el evento `SeekEvent.SEEK_END`.
1. Recupere la posición de reproducción ajustada final utilizando event.actualPosition.

       Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. Pueden aplicarse varias reglas, entre ellas:
   
   * El comportamiento de reproducción se ve afectado si una búsqueda u otro cambio de posición termina en medio de una pausa publicitaria o omite las pausas publicitarias.
   * Si busca cerca de un límite de segmento, la posición de búsqueda se ajusta al principio del segmento.

1. Utilice la información de posición para mostrar una barra de desplazamiento.
