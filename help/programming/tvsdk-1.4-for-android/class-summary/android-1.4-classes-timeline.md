---
description: Estas clases proporcionan información sobre la cronología de los medios en particular, incluida la colocación de los anuncios.
seo-description: Estas clases proporcionan información sobre la cronología de los medios en particular, incluida la colocación de los anuncios.
seo-title: Clases de escala de tiempo
title: Clases de escala de tiempo
uuid: dd4af4b4-215e-45cb-8bac-574a461ac1ce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Clases de línea de tiempo{#timeline-classes}

Estas clases proporcionan información sobre la cronología de los medios en particular, incluida la colocación de los anuncios.

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
   <td colname="2"> Una clase de oportunidad representa un punto de interés en la línea de tiempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Cronograma</a> </td> 
   <td colname="2"> Interfaz que proporciona un iterador para procesar marcadores de línea de tiempo. Representa la línea de tiempo del contenido, incluidos los saltos de publicidad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem</a> </span> </td> 
   <td colname="2"> Clase. Representación inmutable genérica de un elemento de línea de tiempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> Marcador de línea de tiempo</a> </span> </td> 
   <td colname="2"> Interfaz que representa un marcador en la línea de tiempo. Esto marca una región de interés en la línea de tiempo real. Actualmente, las regiones de interés son las publicidades, que puede que desee marcar, por ejemplo, con un color diferente en la IU de la barra de desplazamiento. Cada marcador se define mediante una posición y una duración (cada una expresada en milisegundos). </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineOperation.html" format="html" scope="external"> TimelineOperation</a> </td> 
   <td colname="2"> Clase base para todas las operaciones que afectan a la línea de tiempo. </td> 
  </tr> 
 </tbody> 
</table>

