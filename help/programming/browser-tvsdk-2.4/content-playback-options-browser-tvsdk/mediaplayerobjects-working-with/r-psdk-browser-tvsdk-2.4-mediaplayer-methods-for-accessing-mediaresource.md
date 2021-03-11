---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
title: Atributos de MediaPlayer para acceder a la información de MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Atributos de MediaPlayer para acceder a la información de MediaResource{#mediaplayer-attributes-to-access-mediaresource-information}

Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Objetivo </th> 
   <th colname="2" class="entry"> Atributo </th> 
   <th colname="3" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Emisión en directo </td> 
   <td colname="2"> <span class="codeph"> live  </span> </td> 
   <td colname="3"> True si el flujo está activo; false si es VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Subtítulos </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions  </span> </td> 
   <td colname="3"> True si hay disponibles pistas de subtítulos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks  </span> </td> 
   <td colname="3"> Proporciona una lista de las pistas de subtítulos cerrados disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack  </span> </td> 
   <td colname="3"> Recupera el seguimiento de subtítulos cerrados seleccionado con <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Audio alternativo </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio  </span> </td> 
   <td colname="3"> <p>True si el flujo tiene pistas de audio alternativas. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks  </span> </td> 
   <td colname="3"> Proporciona una lista de pistas de audio alternativas disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack  </span> </td> 
   <td colname="3"> 
    <pre>
      Recupera la pista de audio seleccionada actualmente con 
     <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Metadatos temporizados </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata  </span> </td> 
   <td colname="3"> True si el flujo tiene metadatos temporizados asociados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata  </span> </td> 
   <td colname="3"> Proporciona una lista de los objetos de metadatos temporizados asociados al flujo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Varios perfiles (tasas de bits) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> perfiles  </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Proporciona una lista de los perfiles de velocidad de bits asociados a este flujo. <p>Nota:  Puede recuperar la velocidad de bits de cada perfil y la altura y anchura del perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Recurso de medios </td> 
   <td colname="2"> <span class="codeph"> recurso  </span> </td> 
   <td colname="3"> Devuelve el recurso de medios asociado a este elemento. </td> 
  </tr> 
 </tbody> 
</table>

