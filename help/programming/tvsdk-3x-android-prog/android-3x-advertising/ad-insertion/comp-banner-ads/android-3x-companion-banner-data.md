---
description: El contenido de un recurso publicitario describe un banner complementario.
title: Datos de banner complementario
exl-id: fae96cb8-0092-43ed-a26b-cdaa1389a368
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Datos de banner complementario {#companion-banner-data}

El contenido de un recurso publicitario describe un banner complementario.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Cada `AdAsset` proporciona información sobre cómo mostrar el recurso.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Información disponible </b></th> 
   <th colname="col2" class="entry"> <b>Descripción</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> anchura </td> 
   <td colname="col2"> Anchura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altura </td> 
   <td colname="col2"> Altura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">El tipo de recurso para este banner complementario: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: los datos están en código de HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: los datos son una dirección URL de iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estática </td> 
   <td colname="col2"> <p>A veces, el banner complementario también tiene un <span class="codeph"> staticURL</span> que es una URL directa a la imagen o a un <span class="codeph"> .swf</span> (titular de flash). </p> <p>Si no desea utilizar html o iframe, puede utilizar una URL directa a una imagen o swf para mostrar el titular en la fase de Flash en su lugar. En este caso, puede utilizar la variable <span class="codeph"> staticURL</span> para mostrar el titular. </p> <p>Importante: Debe comprobar si la dirección URL estática es una cadena válida, ya que esta propiedad podría no estar siempre disponible. </p> </td> 
  </tr> 
 </tbody> 
</table>
