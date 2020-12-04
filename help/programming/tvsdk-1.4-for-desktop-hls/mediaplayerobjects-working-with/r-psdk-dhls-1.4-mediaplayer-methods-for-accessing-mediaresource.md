---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
seo-description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
seo-title: Métodos de MediaPlayer para acceder a la información de MediaResource
title: Métodos de MediaPlayer para acceder a la información de MediaResource
uuid: c2d18f8e-4107-42bc-a975-9b881aadd27b
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# Métodos de MediaPlayer para acceder a la información de MediaResource{#mediaplayer-methods-for-accessing-mediaresource-information}

Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Método </th> 
   <th colname="3" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Flujo en vivo  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isLive():Boolean;  </span> </td> 
   <td colname="3"> <p>True si el flujo está activo; false si es VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM protegido</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isProtected():Boolean;  </span> </td> 
   <td colname="3"> <p>True si el flujo está protegido con DRM. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get drmMetadataInfos(): Vector.&lt;drmmetadatainfo&gt;;  </span> </td> 
   <td colname="3"> <p>Lista todos los objetos de metadatos DRM detectados en el manifiesto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Subtítulos opcionales</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasClosedCaptions():Boolean;  </span> </td> 
   <td colname="3"> <p>True si hay pistas de subtítulos opcionales disponibles. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get closeCaptionsTracks():Vector.&lt;closedcaptionstrack&gt;;  </span> </td> 
   <td colname="3"> <p>Proporciona una lista de las pistas de subtítulos opcionales disponibles. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get selectedClosedCaptionsTrack():ClosedCaptionsTrack  </span> </td> 
   <td colname="3"> <p>Recupera la pista de subtítulos cerrados actual seleccionada con <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (closedCaptionsTrack: com.adobe.mediacore.info:ClosedCaptionsTrack )  </span> </td> 
   <td colname="3"> <p>Define una pista de subtítulos cerrados como la pista de subtítulos opcionales actual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Pistas de audio alternativas  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasAlternateAudio():Boolean;  </span> </td> 
   <td colname="3"> <p>True si el flujo tiene pistas de audio alternativas. </p> <p>Sugerencia:  La pista de audio principal (predeterminada) también forma parte de la lista de pista de audio alternativa. </p> <p>TVSDK for Desktop HLS considera que la pista de audio principal es uno de los elementos de la lista de pista de audio alternativa. Debido a esto, el único caso en el que <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> devuelve false es cuando el flujo no tiene audio. Si el contenido solo tiene una pista de audio, este método devuelve true y <span class="codeph"> get AudioTracks </span> devuelve una lista con un solo elemento (la pista de audio predeterminada). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get audioTracks():Vector.&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> Proporciona una lista de las pistas de audio alternativas disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get audioTracks():Vector.&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> <p>Proporciona una lista de las pistas de audio alternativas disponibles. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get selectedAudioTrack():AudioTrack;  </span> </td> 
   <td colname="3"> <p>Recupera la pista de audio seleccionada con <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack: AudioTrack )  </span> </td> 
   <td colname="3"> <p>Selecciona una pista de audio para que sea la pista de audio actual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Metadatos temporizados</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasTimedMetadata():Boolean;  </span> </td> 
   <td colname="3"> <p>True si el flujo tiene metadatos temporizados asociados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get timedMetadata():Vector.&lt;timedmetadata&gt;;  </span> </td> 
   <td colname="3"> <p>Proporciona una lista de los objetos de metadatos temporizados asociados al flujo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isDynamic():Boolean;  </span> </td> 
   <td colname="3"> <p>True si el flujo es un flujo de velocidad de bits múltiple (MBR). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get perfiles():Vector.&lt;profile&gt;;  </span> </td> 
   <td colname="3"> <p>Proporciona una lista de los perfiles de velocidad de bits asociados. Para cada perfil, puede recuperar su velocidad de bits y la altura y anchura del perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Juego de trucos  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isTrickPlaySupported():Boolean;  </span> </td> 
   <td colname="3"> <p>True si el reproductor admite avance rápido, rebobinado y reanudación. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> función get availablePlaybackRates():Vector.&lt;number&gt; </span> </td> 
   <td colname="3"> <p>Proporciona la lista de las tasas de reproducción disponibles en el contexto de la función de reproducción mediante trucos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Reproductor multimedia  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get player():MediaPlayer  </span> </td> 
   <td colname="3"> <p>Devuelve el reproductor de medios asociado actualmente a este reproductor. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Recurso multimedia</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get resource():MediaResource;  </span> </td> 
   <td colname="3"> <p>Devuelve el recurso de medios asociado a este elemento. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> function get resourceId():int  </span> </td> 
   <td colname="3"> <p>Devuelve el identificador de medios asociado a este elemento. </p> </td> 
  </tr> 
 </tbody> 
</table>

