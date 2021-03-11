---
description: El contenido de un AdAsset describe un banner complementario.
title: Datos de banner complementario
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Datos del banner Companion {#companion-banner-data}

El contenido de un AdAsset describe un banner complementario.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Cada `AdAsset` proporciona información sobre cómo mostrar el recurso.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Información disponible  </b></th> 
   <th colname="col2" class="entry"> <b>Descripción</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Anchura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Altura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">El tipo de recurso para este banner complementario: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Los datos están en código HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Los datos son una URL de iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dirección URL estática </td> 
   <td colname="col2"> <p>A veces, el banner complementario también tiene una <span class="codeph"> dirección URL estática</span> que es una dirección URL directa a la imagen o a un <span class="codeph"> .swf</span> (titular flash). </p> <p>Si no desea utilizar html o iframe, puede utilizar una dirección URL directa para una imagen o un swf para mostrar el banner en la fase de Flash. En este caso, puede utilizar la <span class="codeph"> staticURL</span> para mostrar el banner. </p> <p>Importante:  Debe comprobar si la dirección URL estática es una cadena válida, ya que es posible que esta propiedad no siempre esté disponible. </p> </td> 
  </tr> 
 </tbody> 
</table>