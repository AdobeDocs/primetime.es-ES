---
description: El contenido de un AdBannerAsset describe una pancarta adjunta.
seo-description: El contenido de un AdBannerAsset describe una pancarta adjunta.
seo-title: Datos de pancarta complementarios
title: Datos de pancarta complementarios
uuid: b2c709da-9d19-49d1-8116-9c947371b77c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Datos de pancarta complementarios{#companion-banner-data}

El contenido de un AdBannerAsset describe una pancarta adjunta.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

El `AdobePSDK.PSDKEventType.AD_STARTED` evento devuelve una `Ad` instancia que contiene una `companionAssets` propiedad ( `Array<AdBannerAsset>`).
Cada uno `AdBannerAsset` proporciona información sobre cómo mostrar el recurso.

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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">static: Los datos son una dirección URL de imagen estática (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <ph>
      datos de pancarta
    </ph> </td> 
   <td colname="col2"> Datos del tipo especificado por <span class="codeph"> resourceType</span> para este letrero complementario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dirección URL estática </td> 
   <td colname="col2"> <p>A veces, el letrero acompañante también puede tener una dirección URL estática que sea una dirección URL directa a la imagen. </p> <p>Si no desea utilizar html o iframe, puede utilizar una dirección URL directa para una imagen. En este caso, puede utilizar staticURL para mostrar la pancarta. </p> <p>Importante:  Debe comprobar si la dirección URL estática es una cadena válida, ya que es posible que esta propiedad no siempre esté disponible. </p> </td> 
  </tr> 
 </tbody> 
</table>

