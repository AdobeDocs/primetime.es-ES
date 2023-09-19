---
description: TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
title: Elementos de API para la reproducción de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Elementos de API para la reproducción de publicidad {#api-elements-for-ad-playback}

TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.

Los siguientes elementos de la API son útiles para personalizar la reproducción:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento API </b></th> 
   <th colname="col2" class="entry"> <b>Contenido que admite publicidad</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata </span> </td> 
   <td colname="col2">Controle si una pausa publicitaria debe marcarse como si hubiera sido visualizada por un visor y, en caso afirmativo, cuándo marcarla. Configurar y obtener la directiva vigilada mediante <span class="codeph"> setAdBreakAsWatched</span> y <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción para las pausas publicitarias. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción de anuncios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> Interfaz que permite personalizar el comportamiento de anuncios de TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Clase que implementa el comportamiento predeterminado de TVSDK. La aplicación puede invalidar esta clase para personalizar los comportamientos predeterminados sin implementar la interfaz completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>Es la hora local de la reproducción, excluidas las pausas publicitarias colocadas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>En este caso, la búsqueda se produce en relación con una hora local de la secuencia. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posición virtual en la cronología se convierte a la posición local. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> in <span class="codeph"> MediaPlayer</span> devuelve el tiempo actual en relación con el contenido original, sin anuncios asociados dinámicamente. <span class="codeph"> getLocalTime</span> in <span class="codeph"> AdBreak</span> devuelve la hora de inicio de la pausa en relación con el contenido original. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched</span> propiedad. Indica si el visualizador ha visto el anuncio. </td> 
  </tr> 
 </tbody> 
</table>
