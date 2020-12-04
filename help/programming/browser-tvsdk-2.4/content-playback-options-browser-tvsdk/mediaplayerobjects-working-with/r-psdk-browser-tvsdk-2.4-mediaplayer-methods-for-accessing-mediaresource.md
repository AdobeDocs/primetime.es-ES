---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido que representa un MediaResource cargado.
seo-description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido que representa un MediaResource cargado.
seo-title: Atributos de MediaPlayer para acceder a la información de MediaResource
title: Atributos de MediaPlayer para acceder a la información de MediaResource
uuid: d26f39d6-0a6b-4072-b99a-8767a511a846
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Atributos de MediaPlayer para acceder a la información de MediaResource{#mediaplayer-attributes-to-access-mediaresource-information}

Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido que representa un MediaResource cargado.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Propósito </th> 
   <th colname="2" class="entry"> Atributo </th> 
   <th colname="3" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Flujo en vivo </td> 
   <td colname="2"> <span class="codeph"> live  </span> </td> 
   <td colname="3"> True si el flujo está activo; false si es VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Subtítulos opcionales </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions  </span> </td> 
   <td colname="3"> True si hay pistas de subtítulos opcionales disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks  </span> </td> 
   <td colname="3"> Proporciona una lista de las pistas de subtítulos opcionales disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack  </span> </td> 
   <td colname="3"> Recupera la pista de subtítulos cerrados seleccionada con <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Audio alternativo </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio  </span> </td> 
   <td colname="3"> <p>True si el flujo tiene pistas de audio alternativas. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks  </span> </td> 
   <td colname="3"> Proporciona una lista de las pistas de audio alternativas disponibles. </td> 
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
   <td colname="1" morerows="1"> Varios perfiles (velocidades de bits) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> perfiles  </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Proporciona una lista de los perfiles de velocidad de bits asociados a este flujo. <p>Nota:  Puede recuperar la velocidad de bits de cada perfil y la altura y anchura del perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Recurso multimedia </td> 
   <td colname="2"> <span class="codeph"> recurso  </span> </td> 
   <td colname="3"> Devuelve el recurso de medios asociado a este elemento. </td> 
  </tr> 
 </tbody> 
</table>

