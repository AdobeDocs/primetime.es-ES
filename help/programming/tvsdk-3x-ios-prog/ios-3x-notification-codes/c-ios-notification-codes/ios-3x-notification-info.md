---
description: Esta tabla proporciona información detallada sobre las notificaciones de tipo INFO.
title: Códigos de notificación INFO
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# Códigos de notificación INFO {#info-notification-codes}

Esta tabla proporciona información detallada sobre las notificaciones de tipo INFO.

La mayoría de las notificaciones informativas contienen metadatos relevantes como, por ejemplo, la dirección URL del recurso que no se ha podido descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Código</b></th> 
   <th colname="2" class="entry"><b>Nombre</b></th> 
   <th colname="3" class="entry"><b>Notificación interna</b></th> 
   <th colname="4" class="entry"><b>Claves de metadatos</b></th> 
   <th colname="5" class="entry"><b>Comentarios</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reproducción</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> Ha comenzado la reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> Se ha completado la reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <p> Ninguno </p> </td> 
   <td colname="5"> Se inició una operación de búsqueda. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> Se completó una operación de búsqueda. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> El estado del reproductor ha cambiado. Cuando el estado es ERROR, la notificación interna es el objeto de notificación de error que activó el cambio al estado ERROR. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Velocidad de bits adaptable (ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> BITRATE </span> </td> 
   <td colname="5"> La velocidad de bits del vídeo ha cambiado. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Audio de enlace tardío (LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>La pista de audio ha cambiado. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Subtítulos</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 307000 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>La pista de subtítulos ha cambiado. </p> </td> 
  </tr> 
 </tbody> 
</table>
