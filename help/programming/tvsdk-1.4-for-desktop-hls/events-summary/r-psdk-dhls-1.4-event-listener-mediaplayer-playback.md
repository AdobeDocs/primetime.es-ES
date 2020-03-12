---
description: La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor detectando los eventos distribuidos por TVSDK.
seo-description: La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor detectando los eventos distribuidos por TVSDK.
seo-title: Eventos de reproducción
title: Eventos de reproducción
uuid: 6d6491d7-cf25-4130-8388-68b8c028bb71
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventos de reproducción {#playback-events}

La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor detectando los eventos distribuidos por TVSDK.

TVSDK distribuye eventos de reproducción cuando se producen operaciones de reproducción de medios, como un vídeo que empieza a reproducirse. Para recibir notificaciones sobre todos los eventos relacionados con la reproducción, registre los oyentes con el `MediaPlayer` objeto para los siguientes eventos.

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Evento </th> 
   <th colname="2" class="entry"> Significado </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reproducción</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> El usuario o el TVSDK ha seleccionado una nueva velocidad de reproducción, como avance rápido, rebobinado o reanudación de la reproducción a una velocidad normal. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> En la pantalla se muestra una nueva velocidad de reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> La posición actual del cursor de reproducción del medio ha cambiado. Se distribuye periódicamente cuando la hora actual ha cambiado, cada 250 ms o más. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reproductor de medios</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> El estado del reproductor de medios ha cambiado. La aplicación debe gestionar los errores en la llamada de retorno de este evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">El perfil actual del reproductor de medios ha cambiado. Utilice la propiedad <span class="codeph"> ProfileEvent.profile</span> para obtener el nuevo perfil que se está reproduciendo. Utilice la propiedad <span class="codeph"> time</span> para obtener la hora en que se produjo este evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">Se ha creado <span class="codeph"> MediaPlayerItem</span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">El reproductor de medios ha actualizado correctamente los medios en cualquiera de estos casos: 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">Cuando se produce una actualización de manifiesto para un recurso activo. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">Cuando un VOD o recurso activo tiene subtítulos cerrados y se detecta por primera vez una actividad para una pista de subtítulos opcionales. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Subtítulos y audio</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">Se ha detectado una nueva pista de subtítulos opcionales en el flujo de medios y se ha actualizado la colección <span class="codeph"> ClosedCaptionsTracks</span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifiesto y línea de tiempo</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">El reproductor de medios ha agregado o eliminado publicidades, por lo que tiene una línea de tiempo actualizada. <p>El manifiesto actualizado para un recurso activo y las pausas publicitarias antiguas se eliminaron de la línea de tiempo o se descubrieron nuevas oportunidades publicitarias (puntos de referencia). El reproductor de medios intenta resolver y colocar cualquier publicidad nueva en la línea de tiempo. </p> <p> Utilice este evento para comprobar si la línea de tiempo tiene actualizaciones (el VOD no cambia durante la reproducción). A continuación, puede recuperar la línea de tiempo mediante <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

