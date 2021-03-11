---
description: TVSDK envía eventos de reproducción cuando se producen operaciones de reproducción de contenido, como un vídeo que comienza a reproducirse.
title: Eventos de reproducción
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Eventos de reproducción{#playback-events}

TVSDK envía eventos de reproducción cuando se producen operaciones de reproducción de contenido, como un vídeo que comienza a reproducirse.

Para recibir notificaciones sobre todos los eventos relacionados con la reproducción, registre una implementación de `MediaPlayer.PlaybackEventListener`, incluidas las siguientes llamadas de retorno de eventos.

<table frame="all" colsep="1" rowsep="1"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Evento </th> 
   <th colname="2" class="entry"> Significado </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Reproducción</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayComplete%28%29" format="html" scope="external"> onPlayComplete</a> </td> 
   <td colname="2"> Se ha llegado al final de una fuente de medios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayStart%28%29" format="html" scope="external"> onPlayStart</a> </td> 
   <td colname="2"> Se ha iniciado la reproducción de una fuente de medios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> onRateSelected</a>  (tasa flotante) </td> 
   <td colname="2"> El usuario o TVSDK ha seleccionado una nueva velocidad de reproducción, como avance rápido, rebobinado o reanudación de la reproducción a una velocidad normal. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlaying</a>  (velocidad flotante) </td> 
   <td colname="2"> Se puede ver una nueva velocidad de reproducción en la pantalla. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Medios</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onPrepared</a> </td> 
   <td colname="2"> El reproductor de medios ha preparado correctamente el contenido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> onSizeAvailable</a>  (altura larga, anchura larga) </td> 
   <td colname="2"> El tamaño del medio está disponible. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Reproductor de medios</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a>  (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.</a> PlayerState,  <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> </a> MediaPlayerNotificationnotification) </td> 
   <td colname="2"> El estado del reproductor de contenidos ha cambiado. La aplicación debe gestionar errores en esta llamada de retorno. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChanged</a>  (perfil largo, largo tiempo) </td> 
   <td colname="2"> El perfil actual del reproductor de contenidos ha cambiado. Utilice la propiedad <span class="codeph"> Perfil</span> para obtener el nuevo perfil que se está reproduciendo. Utilice la propiedad <span class="codeph"> time</span> para obtener la hora en que se produjo este evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>MediaplayerItem</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onUpdated%28%29" format="html" scope="external"> onUpdated</a> </td> 
   <td colname="2">El reproductor de medios ha actualizado correctamente los medios en cualquiera de estos casos: 
    <ul> 
     <li>Cuando se produce una actualización de manifiesto para un recurso activo.</li> 
     <li>Cuando un recurso en directo o de VOD tiene subtítulos cerrados y la actividad se descubre por primera vez para una pista de subtítulos. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Manifiesto y línea de tiempo</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> onTimedMetadata</a>  (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> </a> TimedMetadataMetadataMetadata) </td> 
   <td colname="2"> Se descubren nuevos metadatos temporizados en el manifiesto. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> onTimelineUpdated</a> </td> 
   <td colname="2">El reproductor de contenidos ha agregado o eliminado anuncios, por lo que tiene una cronología actualizada. <p>El manifiesto actualizado para un recurso activo y las pausas publicitarias antiguas se eliminaron de la cronología o se descubrieron nuevas oportunidades publicitarias (puntos de referencia). El reproductor multimedia intenta resolver y colocar cualquier publicidad nueva en la cronología. </p><p> Utilice este evento para comprobar si la línea de tiempo tiene actualizaciones (VOD no cambia durante la reproducción). A continuación, puede recuperar la línea de tiempo utilizando <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
