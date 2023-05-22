---
description: Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.
title: Clases de publicidad de cronología
exl-id: 4411c86d-8c40-457b-bfc1-40fbea77154e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Clases de publicidad de cronología {#timeline-advertising-classes}

Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Nombre</b></th> 
   <th colname="2" class="entry"><b>Descripción</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">Clase que define la abstracción de publicidad y contiene toda la información de la publicidad. Se define mediante un ID único, una duración y un MediaResource. MediaResource contiene la dirección URL donde se encuentra el contenido del anuncio real. 
    <pre>
      Representa un recurso lineal principal unido al contenido. Opcionalmente, puede contener una matriz de recursos complementarios que deben mostrarse junto con el recurso lineal.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">Clase que representa un recurso que se va a mostrar. 
    <pre>
      Representa un recurso que se va a mostrar.
    </pre> 
    <pre>
      Clase que representa un recurso publicitario.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      Muestra un recurso de banner. La aplicación debe crear una nueva instancia de esta clase de utilidad, establecer el recurso de banner y agregarlo a una vista. Esta clase administra internamente la impresión y el rastreo de clics del titular.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">Clase que proporciona una vista unificada de varios anuncios que se reproducirán en algún momento durante la reproducción. 
    <pre>
      Representa una secuencia continua de anuncios insertados en el contenido.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">Clase que representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario. 
    <pre>
      Representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> Protocolo que define propiedades para llamadas a la API AdPolicySelector. Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> Un protocolo de selector de políticas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden ajustarse a este protocolo implementando todos los métodos necesarios o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAdTimeline</a></td> 
   <td colname="2"> Clase que representa la cronología de los saltos dentro del contenido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> clase, 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> protocolo
    </pre> </td> 
   <td colname="2"> Clase que administra la parte de resolución de anuncios en el proceso de Adobe Primetime y decisiones. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> Protocolo que describe los métodos que utiliza el solucionador de contenido personalizado ( <span class="codeph"> PTContentResolver</span> ) debe utilizar para comunicar al delegado el estado de la resolución del contenido. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">Clase que resume una solicitud de información de ubicación. Cada anuncio resuelto debe tener adjunta una información de ubicación. La información de ubicación describe dónde se pretende colocar el anuncio en la cronología. Contiene información como: 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">Posición de colocación (en ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">Tipo de ubicación (pre-roll, mid-roll o post-roll) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">Duración del fragmento de contenido principal que se va a reemplazar </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
