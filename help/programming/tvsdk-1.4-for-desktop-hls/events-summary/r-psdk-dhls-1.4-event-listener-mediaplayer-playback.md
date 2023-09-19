---
description: La aplicación puede monitorizar la actividad del reproductor y su estado cambiando al escuchar los eventos distribuidos por TVSDK.
title: Eventos de reproducción
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Eventos de reproducción {#playback-events}

La aplicación puede monitorizar la actividad del reproductor y su estado cambiando al escuchar los eventos distribuidos por TVSDK.

TVSDK envía eventos de reproducción cuando se producen operaciones de reproducción de contenido, como un vídeo que empieza a reproducirse. Para recibir notificaciones acerca de todos los eventos relacionados con la reproducción, registre los oyentes en `MediaPlayer` para los eventos siguientes.

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
   <td colname="2"> El usuario o TVSDK han seleccionado una nueva velocidad de reproducción, como avance rápido, rebobinado o reanudación de la reproducción a velocidad normal. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> Se puede ver una nueva velocidad de reproducción en la pantalla. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> La posición actual del cabezal de reproducción de los medios ha cambiado. Se envía periódicamente cuando cambia la hora actual, cada 250 ms o más. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reproductor multimedia</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ChangeEvent de MediaPlayerStatus.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> El estado del reproductor de contenidos ha cambiado. La aplicación debe controlar los errores en la llamada de retorno de este evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">El perfil actual del reproductor multimedia ha cambiado. Utilice el <span class="codeph"> ProfileEvent.profile</span> para obtener el nuevo perfil que se está reproduciendo. Utilice el <span class="codeph"> hora</span> para obtener la hora en que se produjo este evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaPlayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">A <span class="codeph"> MediaPlayerItem</span> se ha creado. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">El reproductor de contenidos ha actualizado correctamente los contenidos en cualquiera de estos casos: 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">Cuando se produce una actualización de manifiesto para un recurso activo. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">Cuando un VOD o recurso activo tiene subtítulos y la actividad se descubre por primera vez para un seguimiento de subtítulos. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Subtítulos y audio</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">Se ha detectado un nuevo seguimiento de subtítulos en el flujo de medios y el <span class="codeph"> closedCaptionsTracks</span> se ha actualizado la colección. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifiesto y línea de tiempo</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">El reproductor de contenidos ha añadido o eliminado anuncios, por lo que tiene una cronología actualizada. <p>El manifiesto actualizado para un recurso activo y las pausas publicitarias antiguas se eliminaron de la cronología o se descubrieron nuevas oportunidades publicitarias (puntos de referencia). El reproductor de contenidos intenta resolver y colocar los anuncios nuevos en la cronología. </p> <p> Utilice este evento para comprobar si la cronología tiene actualizaciones (VOD no cambia durante la reproducción). A continuación, puede recuperar la cronología mediante <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
