---
description: Esta tabla proporciona información detallada sobre las notificaciones de tipo INFO.
seo-description: Esta tabla proporciona información detallada sobre las notificaciones de tipo INFO.
seo-title: Códigos de notificación de información
title: Códigos de notificación de información
uuid: 10145ce6-9eb0-4829-85dd-1acfe97b07e8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

---


# Códigos de notificación INFO{#info-notification-codes}

Esta tabla proporciona información detallada sobre las notificaciones de tipo INFO.

La mayoría de las notificaciones informativas contienen metadatos relevantes, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Código </th> 
   <th colname="2" class="entry"> Nombre </th> 
   <th colname="3" class="entry"> Notificación interna </th> 
   <th colname="4" class="entry"> Claves de metadatos </th> 
   <th colname="5" class="entry"> Comentarios </th> 
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
   <td colname="1"><span class="codeph"> 300000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_INICIO  </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> Se ha iniciado la reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE  </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> Se completó la reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_INICIO  </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <p> Ninguno </p> </td> 
   <td colname="5"> Se inició una operación de búsqueda. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE  </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> Se completó una operación de búsqueda. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE  </span> </td> 
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
   <td colname="1"><span class="codeph"> 302000  </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE  </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> BITRATE  </span> </td> 
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
   <td colname="1"><span class="codeph"> 304000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE  </span> </td> 
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
   <td colname="1"><span class="codeph"> 307000  </span> </td> 
   <td colname="2"><span class="codeph"> SUBTÍLES_TRACK_CHANGE  </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>El seguimiento de subtítulos ha cambiado. </p> </td> 
  </tr> 
 </tbody> 
</table>

