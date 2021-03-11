---
description: TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
title: Elementos de API para reproducción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Elementos de API para reproducción de publicidad {#api-elements-for-ad-playback}

TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.

Los siguientes elementos API son útiles para personalizar la reproducción:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento de API  </b></th> 
   <th colname="col2" class="entry"> <b>Contenido compatible con la publicidad</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata  </span> </td> 
   <td colname="col2">Controle si un visitante debe marcar una pausa publicitaria como observada y, en caso afirmativo, cuándo marcarla. Establezca y obtenga la directiva vista mediante <span class="codeph"> setAdBreakAsWatched</span> y <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción para las pausas publicitarias. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción de los anuncios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> Selector de políticas de publicidad  </span> </td> 
   <td colname="col2"> Interfaz que permite personalizar el comportamiento de los anuncios de TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> Clase que implementa el comportamiento predeterminado de TVSDK. La aplicación puede anular esta clase para personalizar los comportamientos predeterminados sin implementar la interfaz completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>Es la hora local de la reproducción, excluyendo las pausas publicitarias colocadas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>En este caso, la búsqueda se produce en relación con una hora local del flujo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertedToLocalTime</span>. <p>La posición virtual en la línea de tiempo se convierte a la posición local. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> en <span class="codeph"> MediaPlayer</span> devuelve el tiempo actual en relación con el contenido original, sin anuncios asociados dinámicamente. <span class="codeph"> </span> getLocalTimein  <span class="codeph"> </span> AdBreak devuelve la hora de inicio de la pausa en relación con el contenido original. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> </span> isWatchedproperty. Indica si el espectador ha visto el anuncio. </td> 
  </tr> 
 </tbody> 
</table>