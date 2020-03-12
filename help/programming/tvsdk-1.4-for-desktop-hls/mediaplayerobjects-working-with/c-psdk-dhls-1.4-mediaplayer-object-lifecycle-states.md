---
description: Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que se finaliza (se reutiliza o se elimina), esta instancia completa una serie de transiciones entre estados.
seo-description: Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que se finaliza (se reutiliza o se elimina), esta instancia completa una serie de transiciones entre estados.
seo-title: Ciclo de vida del objeto MediaPlayer
title: Ciclo de vida del objeto MediaPlayer
uuid: 1452ae3a-7ce9-439e-951c-9d3db63b1d20
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ciclo de vida del objeto MediaPlayer{#mediaplayer-object-lifecycle}

Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que se finaliza (se reutiliza o se elimina), esta instancia completa una serie de transiciones entre estados.

Algunas operaciones solo se permiten cuando el reproductor se encuentra en un estado concreto. Por ejemplo, no se permite llamar `play` en IDLE. Puede llamar a este estado solo después de que el reproductor alcance el estado PREPARADO.

Para trabajar con estados:

* Puede recuperar el estado actual del `MediaPlayer` objeto mediante la `MediaPlayer.status` propiedad .

   ```
   function get status():String;
   ```

* La lista de estados se define en `MediaPlayer.PlayerStatus`.

Diagrama de transición de estado para el ciclo vital de una `MediaPlayer` instancia:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

En la tabla siguiente se proporcionan detalles adicionales:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus </span> </th> 
   <th colname="col2" class="entry"> Ocurre cuando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IDLE </span> </td> 
   <td colname="col2"> <p> La aplicación solicitó un nuevo reproductor de medios creando una instancia de <span class="codeph"> MediaPlayer </span>. El reproductor recién creado está esperando a que especifique un elemento de reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZACIÓN </span> </td> 
   <td colname="col2"> <p>La aplicación se denomina <span class="codeph"> MediaPlayer.replaceCurrentResource </span>y se está cargando el reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZADO </span> </td> 
   <td colname="col2"> <p>TVSDK definió correctamente el elemento del reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARACIÓN </span> </td> 
   <td colname="col2"> <p>La aplicación se denomina <span class="codeph"> MediaPlayer.prepareToPlay </span>. El reproductor de medios está cargando el elemento del reproductor de medios y los recursos asociados. </p> <p>Sugerencia:  Podría producirse algún almacenamiento en búfer del medio principal. </p> <p>TVSDK está preparando el flujo de medios e intentando realizar la resolución de anuncios y la inserción de anuncios (si está activada). </p> <p>Sugerencia:  Para establecer la hora de inicio en un valor distinto de cero, llame a <span class="codeph"> prepareToPlay(startTime) </span> con la hora en milésimas segundos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARADO </span> </td> 
   <td colname="col2"> <p>El contenido se prepara y las publicidades se insertan en la línea de tiempo, o bien se produce un error en el procedimiento de publicidad. Puede comenzar la reproducción o el almacenamiento en búfer. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> REPRODUCCIÓN </span> </td> 
   <td colname="col2"> <p>La aplicación ha llamado a <span class="codeph"> play </span>, por lo que TVSDK está intentando reproducir el vídeo. Es posible que se produzca algún almacenamiento en búfer antes de que se reproduzca realmente el vídeo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> EN PAUSA </span> </td> 
   <td colname="col2"> <p>A medida que la aplicación se reproduce y pone en pausa el medio, el reproductor de medios se mueve entre este estado y PLAYING. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> BÚSQUEDA </span> </td> 
   <td colname="col2"> <p>El reproductor de medios busca la posición correcta mientras está en pausa o reproduciéndose. Para determinar cuándo comenzó o finalizó la búsqueda, escuche los eventos <span class="codeph"> SeekEvent.SEEK_BEGIN </span> y <span class="codeph"> SeekEvent.SEEK_END </span> . </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETADO </span> </td> 
   <td colname="col2"> <p>El reproductor llegó al final del flujo y la reproducción se detuvo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PUBLICADO </span> </td> 
   <td colname="col2"> <p>La aplicación ha lanzado el reproductor de medios, que también libera los recursos asociados. Ya no se puede usar esta instancia </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERROR </span> </td> 
   <td colname="col2"> <p>Error durante el proceso. Un error también puede afectar a lo que la aplicación puede hacer a continuación. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Puede utilizar el estado para proporcionar comentarios sobre el proceso (por ejemplo, un control giratorio mientras espera el siguiente cambio de estado) o para dar el siguiente paso en la reproducción de los medios, como esperar al estado adecuado antes de llamar al siguiente método.

