---
description: Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.
seo-description: Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.
seo-title: Clases de publicidad de línea de tiempo
title: Clases de publicidad de línea de tiempo
uuid: df970e8f-4bf8-4367-9d70-42ebcb11c025
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# Clases publicitarias de escala de tiempo {#timeline-advertising-classes}

Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.

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
   <td colname="2">Clase que define la abstracción de publicidad y contiene toda la información de publicidad. Se define mediante un ID único, una duración y un MediaResource. MediaResource contiene la dirección URL donde reside el contenido de la publicidad real. 
    <pre>
      Representa un recurso lineal principal dividido en el contenido. Opcionalmente, puede contener una matriz de recursos complementarios que se deben mostrar junto con el recurso lineal.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">Clase que representa un recurso que se va a mostrar. 
    <pre>
      Representa un recurso que se va a mostrar.
    </pre> 
    <pre>
      Clase que representa un recurso de publicidad.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      Muestra un recurso de pancarta. La aplicación debe crear una nueva instancia de esta clase de utilidad, establecer el recurso de pancarta y agregarlo a una vista. Esta clase administra internamente el rastreo de clics e impresiones para la pancarta.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">Clase que proporciona una vista unificada en varios anuncios que se reproducirán en algún momento durante la reproducción. 
    <pre>
      Representa una secuencia continua de publicidades empalmadas en el contenido.
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
   <td colname="2"> Protocolo que define las propiedades de las llamadas a la API de AdPolicySelector. Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> Un protocolo de selector de directivas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden cumplir este protocolo implementando todos los métodos requeridos o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAdTimeline</a></td> 
   <td colname="2"> Clase que representa la línea de tiempo de los saltos dentro del contenido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> </a> PTContentResolverclass,  
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> </a> PTContentResolverprotocol
    </pre> </td> 
   <td colname="2"> Clase que gestiona la parte de resolución de publicidad en el proceso de toma de decisiones de publicidad de Adobe Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> Protocolo que describe los métodos que debe utilizar la resolución de contenido personalizado ( <span class="codeph"> PTContentResolver</span> ) para comunicar al delegado el estado de la resolución de contenido. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">Clase que abstrae una solicitud de información de colocación. Cada publicidad resuelta debe tener una información de colocación adjunta. La información de colocación describe dónde se va a colocar la publicidad en la línea de tiempo. Contiene información como: 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">Posición de colocación (en ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">Tipo de colocación (previo, medio rollo o posterior) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">Duración del fragmento de contenido principal que se va a reemplazar </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>