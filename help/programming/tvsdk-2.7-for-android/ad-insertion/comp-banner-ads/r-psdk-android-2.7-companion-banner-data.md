---
description: El contenido de un AdAsset describe una pancarta adjunta.
seo-description: El contenido de un AdAsset describe una pancarta adjunta.
seo-title: Datos de pancarta complementarios
title: Datos de pancarta complementarios
uuid: 4a5d78e1-5abe-45a8-b50f-14f73fdcc879
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Datos de pancarta complementarios {#companion-banner-data}

El contenido de un AdAsset describe una pancarta adjunta.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Cada `AdAsset` proporciona información sobre cómo mostrar el recurso.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Información disponible </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Anchura de la pancarta adjunta en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Altura del letrero acompañante en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">El tipo de recurso para esta pancarta complementaria: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Los datos están en código HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Los datos son una dirección URL de iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dirección URL estática </td> 
   <td colname="col2"> <p>A veces, el titular acompañante también tiene una <span class="codeph"> dirección URL estática</span> que es una dirección URL directa a la imagen o a un <span class="codeph"> .swf</span> (titular Flash). </p> <p>Si no desea utilizar html o iframe, puede utilizar una URL directa a una imagen o swf para mostrar la pancarta en la etapa de Flash. En este caso, puede utilizar la <span class="codeph"> dirección URL estática</span> para mostrar la pancarta. </p> <p>Importante:  Debe comprobar si la dirección URL estática es una cadena válida, ya que es posible que esta propiedad no siempre esté disponible. </p> </td> 
  </tr> 
 </tbody> 
</table>

