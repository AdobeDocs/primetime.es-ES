---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
title: Métodos MediaPlayerItem para acceder a la información de MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# Métodos MediaPlayerItem para acceder a la información de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Método </th> 
   <th colname="3" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Etiquetas de publicidad</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;string&gt; ListgetAdTags()  </span> </td> 
   <td colname="3"> Proporciona la lista de etiquetas de publicidad que se usan en el proceso de colocación de publicidad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Emisión en directo</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive();  </span> </td> 
   <td colname="3"> True si el flujo está activo; false si es VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Protegido por DRM</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtection();  </span> </td> 
   <td colname="3"> True si el flujo está protegido por DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;drmmetadatainfo&gt; ListgetDRMMetadataInfos();  </span> </td> 
   <td colname="3"> Enumera todos los objetos de metadatos DRM descubiertos en el manifiesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Subtítulos</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasClosedCaptions();  </span> </td> 
   <td colname="3"> True si hay disponibles pistas de subtítulos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;closedcaptionstrack&gt; ListgetClosedCationsTracks();  </span> </td> 
   <td colname="3"> Proporciona una lista de las pistas de subtítulos cerrados disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack();  </span> </td> 
   <td colname="3"> Recupera la pista de subtítulos cerrados actual seleccionada con <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack )  </span> </td> 
   <td colname="3"> Define una pista de subtítulos para que sea la pista de subtítulos actual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Pistas de audio alternativas</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasAlternateAudio();  </span> </td> 
   <td colname="3"> True si el flujo tiene pistas de audio alternativas. <p>Nota:  La pista de audio principal (predeterminada) también forma parte de la lista de pistas de audio alternativas. </p> <p>TVSDK para Android considera que la pista de audio principal es uno de los elementos de la lista de pistas de audio alternativas. Debido a esto, el único caso en el que <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> devuelve false es cuando el flujo no tiene audio. Si el contenido tiene una sola pista de audio, este método devuelve el valor "True" y <span class="codeph"> MediaPlayerItem.getAudioTracks </span> devuelve una lista con un solo elemento (la pista de audio predeterminada). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> Proporciona una lista de pistas de audio alternativas disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack();  </span> </td> 
   <td colname="3"> Recupera la pista de audio seleccionada con <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack )  </span> </td> 
   <td colname="3"> Selecciona una pista de audio para que sea la pista de audio actual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Metadatos temporizados</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata();  </span> </td> 
   <td colname="3"> True si el flujo tiene metadatos temporizados asociados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;timedmetadata&gt; ListgetTimedMetadata();  </span> </td> 
   <td colname="3"> Proporciona una lista de los objetos de metadatos temporizados asociados al flujo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Varios perfiles (tasas de bits)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic();  </span> </td> 
   <td colname="3"> True si el flujo es un flujo de velocidad de bits múltiple (MBR). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;profile&gt; ListgetProfiles();  </span> </td> 
   <td colname="3"> Proporciona una lista de los perfiles de velocidad de bits asociados. Para cada perfil, puede recuperar su velocidad de bits y la altura y anchura del perfil. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Perfil getSelectedProfile()  </span> </td> 
   <td colname="3"> Recupera el perfil seleccionado actualmente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Reproducción complicada</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isTrickPlaySupported();  </span> </td> 
   <td colname="3"> True si el reproductor admite el avance rápido, el rebobinado y la reanudación. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt; Float=""&gt; ListgetAvailablePlaybackRates()  </span> </td> 
   <td colname="3"> Proporciona la lista de tasas de reproducción disponibles en el contexto de la función de reproducción mediante trucos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Float getSelectedPlaybackRate()  </span> </td> 
   <td colname="3"> Recupera la tasa de reproducción seleccionada actualmente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig()  </span> </td> 
   <td colname="3"> Devuelve la instancia <span class="codeph"> MediaPlayerItemConfig </span> asociada a este elemento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Recurso de medios</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> Devuelve el recurso de medios asociado a este elemento. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId()  </span> </td> 
   <td colname="3"> Devuelve el identificador de medios asociado a este elemento. Este ID se establece cuando el elemento se carga mediante <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
