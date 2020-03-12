---
description: TVSDK distribuye eventos de reproducción cuando se producen operaciones de reproducción de medios, como un vídeo que empieza a reproducirse.
seo-description: TVSDK distribuye eventos de reproducción cuando se producen operaciones de reproducción de medios, como un vídeo que empieza a reproducirse.
seo-title: Eventos de reproducción
title: Eventos de reproducción
uuid: 809a8e0e-f4d8-4013-b04a-49fb93d7ca8a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Eventos de reproducción{#playback-events}

TVSDK distribuye eventos de reproducción cuando se producen operaciones de reproducción de medios, como un vídeo que empieza a reproducirse.

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
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> onRateSelected</a> (velocidad flotante) </td> 
   <td colname="2"> El usuario o el TVSDK ha seleccionado una nueva velocidad de reproducción, como avance rápido, rebobinado o reanudación de la reproducción a una velocidad normal. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlaying</a> (velocidad flotante) </td> 
   <td colname="2"> En la pantalla se muestra una nueva velocidad de reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Medios</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onPrepared</a> </td> 
   <td colname="2"> El reproductor multimedia ha preparado correctamente los medios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> onSizeAvailable</a> (alto largo, ancho largo) </td> 
   <td colname="2"> El tamaño del medio está disponible. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Reproductor de medios</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a> (estado<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.PlayerState</a> , notificación <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> MediaPlayerNotification</a> ) </td> 
   <td colname="2"> El estado del reproductor de medios ha cambiado. La aplicación debe gestionar los errores de esta llamada de retorno. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChanged</a> (perfil largo, largo tiempo) </td> 
   <td colname="2"> El perfil actual del reproductor de medios ha cambiado. Utilice la propiedad <span class="codeph"> Profile</span> para obtener el nuevo perfil que se está reproduciendo. Utilice la propiedad <span class="codeph"> time</span> para obtener la hora en que se produjo este evento. </td> 
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
     <li>Cuando un VOD o recurso activo tiene subtítulos cerrados y se detecta por primera vez una actividad para una pista de subtítulos opcionales. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Manifiesto y línea de tiempo</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> onTimedMetadata</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> TimedMetadata</a> timedMetadata) </td> 
   <td colname="2"> Se descubren nuevos metadatos temporizados en el manifiesto. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> onTimelineUpdated</a> </td> 
   <td colname="2">El reproductor de medios ha agregado o eliminado publicidades, por lo que tiene una línea de tiempo actualizada. <p>El manifiesto actualizado para un recurso activo y las pausas publicitarias antiguas se eliminaron de la línea de tiempo o se descubrieron nuevas oportunidades publicitarias (puntos de referencia). El reproductor de medios intenta resolver y colocar cualquier publicidad nueva en la línea de tiempo. </p><p> Utilice este evento para comprobar si la línea de tiempo tiene actualizaciones (el VOD no cambia durante la reproducción). A continuación, puede recuperar la línea de tiempo mediante <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
