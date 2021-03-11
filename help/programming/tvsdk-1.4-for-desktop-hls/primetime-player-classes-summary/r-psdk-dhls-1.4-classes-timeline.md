---
description: Estas clases proporcionan información sobre la cronología de los medios en particular, incluida la colocación de los anuncios.
title: Clases de cronología
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Clases de línea de tiempo{#timeline-classes}

Estas clases proporcionan información sobre la cronología de los medios en particular, incluida la colocación de los anuncios.

Paquete: [com.adobe.mediacore.cronología](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nombre </th> 
   <th colname="2" class="entry"> <p>Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker  </a> </span> </td> 
   <td colname="2"> Interfaz que define el protocolo que debe implementar si desea crear un módulo de seguimiento de contenido diseñado para integrarse con la biblioteca TVSDK. <p>Esta interfaz requiere que defina la forma en que se informan los eventos de progreso al sistema de seguimiento remoto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> Oportunidad  </a> </span> </td> 
   <td colname="2"> Clase base para todas las clases de oportunidad. Una clase de oportunidad representa un punto "interesante" en la cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> Colocación  </a> </span> </td> 
   <td colname="2"> Clase que ajusta información relacionada con la ubicación de la línea de tiempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> PlacementMode  </a> </span> </td> 
   <td colname="2"> Enumeración de los modos de colocación, como si se va a insertar o reemplazar contenido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType  </a> </span> </td> 
   <td colname="2"> Enumeración de tipos de ubicación que indican dónde se realiza la ubicación en la cronología; por ejemplo, PRE_ROLL. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> Reserva  </a> </span> </td> 
   <td colname="2"> Una reserva se utiliza para limitar o impedir el procesamiento posterior de un determinado intervalo de tiempo en la cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Cronología  </a> </span> </td> 
   <td colname="2"> Interfaz que proporciona un iterador para procesar marcadores de cronología. Representa la cronología del contenido, incluidas las pausas publicitarias. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> ElementoLíneaDeTiempo  </a> </span> </td> 
   <td colname="2"> Clase. Representación inmutable genérica de un elemento de línea de tiempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> Marcador de cronología  </a> </span> </td> 
   <td colname="2"> Clase que representa un marcador en la línea de tiempo. Esto marca una región de interés en la cronología real. Actualmente, las regiones de interés son los anuncios, que puede que desee marcar, por ejemplo, con un color diferente en la interfaz de usuario de la barra de desplazamiento. Cada marcador se define mediante una posición y una duración (cada una expresada en milisegundos). </td> 
  </tr> 
 </tbody> 
</table>

