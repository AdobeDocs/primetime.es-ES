---
description: TVSDK proporciona clases y métodos que se pueden utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
seo-description: TVSDK proporciona clases y métodos que se pueden utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
seo-title: Elementos de API para reproducción de publicidad
title: Elementos de API para reproducción de publicidad
uuid: 56844663-d635-4b04-b61b-cb8f33ef5732
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Elementos de API para reproducción de publicidad {#api-elements-for-ad-playback}

TVSDK proporciona clases y métodos que se pueden utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.

Los siguientes elementos de API son útiles para personalizar la reproducción:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento API  </b></th> 
   <th colname="col2" class="entry"> <b>Contenido que admite publicidad</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata  </span> </td> 
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
   <td colname="col1"><span class="apiname"> AdPolicySelector  </span> </td> 
   <td colname="col2"> Interfaz que permite personalizar el comportamiento de la publicidad TVSDK. </td> 
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
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> searchToLocal</span>. <p>Aquí, la búsqueda se produce en relación con una hora local del flujo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posición virtual en la línea de tiempo se convierte a la posición local. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> en <span class="codeph"> MediaPlayer</span> devuelve el tiempo actual en relación con el contenido original, sin anuncios replicados dinámicamente. <span class="codeph"> </span> getLocalTimein  <span class="codeph"> </span> AdBreakeves devuelve el tiempo de inicio del salto en relación con el contenido original. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> </span> isWatchedproperty. Indica si el visor ha visto la publicidad. </td> 
  </tr> 
 </tbody> 
</table>