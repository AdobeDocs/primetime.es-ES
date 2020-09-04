---
description: TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
seo-description: TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
seo-title: Elementos de API para reproducción de publicidad
title: Elementos de API para reproducción de publicidad
uuid: 61ebbfd7-696c-4a5b-8dbb-682770cd5840
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Elementos de API para reproducción de publicidad{#api-elements-for-ad-playback}

TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.

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
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">Controle si un salto de publicidad debe marcarse como visto por un visor y, en caso afirmativo, cuándo debe marcarse. Configurar y obtener la directiva observada mediante 
    <pre>
     la <span class="codeph"> propiedad adBreakAsWatched</span> .
    </pre> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción para pausas publicitarias. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera las posibles políticas de reproducción de las publicidades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> Interfaz que permite personalizar el comportamiento de la publicidad TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> Clase que implementa el comportamiento predeterminado de TVSDK. La aplicación puede anular esta clase para personalizar los comportamientos predeterminados sin implementar la interfaz completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>Es la hora local de la reproducción, excluyendo las pausas publicitarias colocadas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> searchToLocal</span>. <p>Aquí, la búsqueda se produce en relación con una hora local del flujo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posición virtual en la línea de tiempo se convierte a la posición local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> TimelineItem</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> mirado</span>. <p>Indica si el visor ha visto la publicidad. </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>La posición inicial y la duración de una pausa publicitaria o una publicidad en relación con el contenido original. </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>. <p>La posición inicial y la duración de una pausa publicitaria o una publicidad en la línea de tiempo virtual después de considerar todos los saltos de publicidad colocados. </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

