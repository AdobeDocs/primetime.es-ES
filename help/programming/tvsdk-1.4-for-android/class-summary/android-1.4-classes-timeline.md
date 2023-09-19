---
description: Estas clases proporcionan información sobre la cronología de los medios concretos, incluida la colocación de anuncios.
title: Clases de cronología
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Clases de cronología{#timeline-classes}

Estas clases proporcionan información sobre la cronología de los medios concretos, incluida la colocación de anuncios.

Paquete: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nombre </th> 
   <th colname="2" class="entry"> <p>Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/PlacementOpportunity.html" format="html" scope="external"> PlacementOpportunity</a></span> </td> 
   <td colname="2"> Una clase de oportunidad representa un punto de interés en la cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Cronología</a> </td> 
   <td colname="2"> Interfaz que proporciona un iterador para procesar marcadores de cronología. Representa la cronología del contenido, incluidas las pausas publicitarias. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem</a> </span> </td> 
   <td colname="2"> Clase. Representación genérica inmutable de un elemento de cronología. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TimelineMarker</a> </span> </td> 
   <td colname="2"> Interfaz que representa un marcador en la cronología. Esto marca una región de interés en la cronología real. Actualmente, las regiones de interés son los anuncios, que es posible que desee marcar, por ejemplo, con un color diferente en la interfaz de usuario de la barra de desplazamiento. Cada marcador se define mediante una posición y una duración (cada una expresada en milisegundos). </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineOperation.html" format="html" scope="external"> TimelineOperation</a> </td> 
   <td colname="2"> Clase base para todas las operaciones que afectan a la cronología. </td> 
  </tr> 
 </tbody> 
</table>
