---
description: TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
title: Elementos de API para la reproducción de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Elementos de API para la reproducción de publicidad{#api-elements-for-ad-playback}

TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.

Los siguientes elementos de la API son útiles para personalizar la reproducción:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento API </th> 
   <th colname="col2" class="entry"> Contenido que admite publicidad </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">Controle si una pausa publicitaria debe marcarse como si hubiera sido visualizada por un visor y, en caso afirmativo, cuándo marcarla. Configurar y obtener la directiva vigilada mediante 
    <pre>
     el 
     <span class="codeph"> adBreakAsWatched</span> propiedad.
    </pre> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción para las pausas publicitarias. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción de anuncios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> Interfaz que permite personalizar el comportamiento de anuncios de TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> Clase que implementa el comportamiento predeterminado de TVSDK. La aplicación puede invalidar esta clase para personalizar los comportamientos predeterminados sin implementar la interfaz completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>Es la hora local de la reproducción, excluidas las pausas publicitarias colocadas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocal</span>. <p>En este caso, la búsqueda se produce en relación con una hora local de la secuencia. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posición virtual en la cronología se convierte a la posición local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> TimelineItem</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> vigilado</span>. <p>Indica si el visualizador ha visto el anuncio. </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>La posición inicial y la duración de una pausa publicitaria o un anuncio en relación con el contenido original. </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>. <p>La posición inicial y la duración de una pausa publicitaria o anuncio en la cronología virtual después de tener en cuenta todas las pausas publicitarias colocadas. </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
