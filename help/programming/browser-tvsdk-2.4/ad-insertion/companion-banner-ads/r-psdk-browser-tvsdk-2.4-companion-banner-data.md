---
description: El contenido de un AdBannerAsset describe un banner complementario.
title: Datos de banner complementario
exl-id: 94954233-4357-43be-a61f-6d8010c930ca
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Datos de banner complementario{#companion-banner-data}

El contenido de un AdBannerAsset describe un banner complementario.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

El `AdobePSDK.PSDKEventType.AD_STARTED` el evento devuelve un `Ad` instancia que contiene un `companionAssets` property ( `Array<AdBannerAsset>`).
Cada `AdBannerAsset` proporciona información sobre cómo mostrar el recurso.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Información disponible </th> 
   <th colname="col2" class="entry"> Descripción </th> 
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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">static: los datos son una URL de imagen estática (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      datos de banner
    </pre> </td> 
   <td colname="col2"> Los datos del tipo especificado por. <span class="codeph"> resourceType</span> para este banner complementario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estática </td> 
   <td colname="col2"> <p>A veces, el banner complementario también puede tener una URL estática que es una URL directa a la imagen. </p> <p>Si no desea utilizar html o iframe, puede utilizar una dirección URL directa para agregar una imagen. En este caso, puede utilizar la dirección URL estática para mostrar el titular. </p> <p>Importante: Debe comprobar si la dirección URL estática es una cadena válida, ya que esta propiedad podría no estar siempre disponible. </p> </td> 
  </tr> 
 </tbody> 
</table>
