---
description: TVSDK proporciona clases y métodos que se pueden utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
seo-description: TVSDK proporciona clases y métodos que se pueden utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
seo-title: Elementos de API para reproducción de publicidad
title: Elementos de API para reproducción de publicidad
uuid: 5e21e709-8446-4fed-8711-aa4f629f1147
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Elementos de API para reproducción de publicidad {#api-elements-for-ad-playback}

TVSDK proporciona clases y métodos que se pueden utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.

Los siguientes elementos de API son útiles para personalizar la reproducción:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento API </th> 
   <th colname="col2" class="entry"> Contenido que admite publicidad </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata </span> </td> 
   <td colname="col2">Controle si un salto de publicidad debe marcarse como visto por un visor y, en caso afirmativo, cuándo debe marcarse. Configure y obtenga la directiva observada mediante <span class="codeph"> setAdBreakAsWatched</span> y <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción para pausas publicitarias. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción de las publicidades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> Interfaz que permite personalizar el comportamiento de la publicidad TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Clase que implementa el comportamiento predeterminado de TVSDK. La aplicación puede anular esta clase para personalizar los comportamientos predeterminados sin implementar la interfaz completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>Es la hora local de la reproducción, excluyendo las pausas publicitarias colocadas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> searchToLocal</span>. <p>Aquí, la búsqueda se produce en relación con una hora local del flujo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posición virtual en la línea de tiempo se convierte a la posición local. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> en <span class="codeph"> MediaPlayer</span> devuelve el tiempo actual en relación con el contenido original, sin anuncios duplicados dinámicamente. <span class="codeph"> getLocalTime</span> en <span class="codeph"> AdBreak</span> devuelve la hora de inicio del salto en relación con el contenido original. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched</span> , propiedad. Indica si el visor ha visto la publicidad. </td> 
  </tr> 
 </tbody> 
</table>

