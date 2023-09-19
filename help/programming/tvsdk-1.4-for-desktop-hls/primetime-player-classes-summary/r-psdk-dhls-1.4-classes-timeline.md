---
description: Estas clases proporcionan información sobre la cronología de los medios concretos, incluida la colocación de anuncios.
title: Clases de cronología
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Clases de cronología{#timeline-classes}

Estas clases proporcionan información sobre la cronología de los medios concretos, incluida la colocación de anuncios.

Paquete: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nombre </th> 
   <th colname="2" class="entry"> <p>Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker </a> </span> </td> 
   <td colname="2"> Interfaz que define el protocolo que debe implementar si desea crear un módulo de seguimiento de contenido diseñado para integrarse con la biblioteca TVSDK. <p>Esta interfaz requiere que defina la forma en que se notifican los eventos de progreso al sistema de seguimiento remoto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> Oportunidad </a> </span> </td> 
   <td colname="2"> Clase base para todas las clases de oportunidad. Una clase de oportunidad representa un punto "interesante" en la cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> Ubicación </a> </span> </td> 
   <td colname="2"> Clase que ajusta la información relacionada con la ubicación de la cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> PlacementMode </a> </span> </td> 
   <td colname="2"> Enumeración de los modos de colocación, como si se debe insertar o reemplazar contenido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType </a> </span> </td> 
   <td colname="2"> Enumeración de los tipos de ubicación que indican dónde se realiza la ubicación en la cronología; por ejemplo, PRE_ROLL. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> Reserva </a> </span> </td> 
   <td colname="2"> Una reserva se utiliza para limitar o evitar un procesamiento posterior de un intervalo de tiempo determinado en la cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Cronología </a> </span> </td> 
   <td colname="2"> Interfaz que proporciona un iterador para procesar marcadores de cronología. Representa la cronología del contenido, incluidas las pausas publicitarias. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem </a> </span> </td> 
   <td colname="2"> Clase. Representación genérica inmutable de un elemento de cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TimelineMarker </a> </span> </td> 
   <td colname="2"> Clase que representa un marcador en la cronología. Esto marca una región de interés en la cronología real. Actualmente, las regiones de interés son los anuncios, que es posible que desee marcar, por ejemplo, con un color diferente en la interfaz de usuario de la barra de desplazamiento. Cada marcador se define mediante una posición y una duración (cada una expresada en milisegundos). </td> 
  </tr> 
 </tbody> 
</table>
