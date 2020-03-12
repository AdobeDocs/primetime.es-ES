---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
seo-description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
seo-title: Métodos de MediaPlayerItem para acceder a la información de MediaResource
title: Métodos de MediaPlayerItem para acceder a la información de MediaResource
uuid: c6e77eb7-cefd-48aa-9373-2b44a96217a5
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Métodos de MediaPlayerItem para acceder a la información de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

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
   <td colname="2"> <span class="codeph"> List&lt;String&gt; getAdTags() </span> </td> 
   <td colname="3"> Proporciona la lista de etiquetas de publicidad que se utilizan para el proceso de colocación de la publicidad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Flujo en vivo</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive(); </span> </td> 
   <td colname="3"> True si el flujo está activo; false si es VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM protegido</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected(); </span> </td> 
   <td colname="3"> True si el flujo está protegido con DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;DRMMetadataInfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> Enumera todos los objetos de metadatos DRM detectados en el manifiesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Subtítulos opcionales</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions(); </span> </td> 
   <td colname="3"> True si hay pistas de subtítulos opcionales disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;ClosedCaptionsTrack&gt; getClosedCationsTracks(); </span> </td> 
   <td colname="3"> Proporciona una lista de las pistas de subtítulos opcionales disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> Recupera la pista de subtítulos opcionales actual seleccionada con <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (ClosedCaptionsTrack ClosedCaptionsTrack) </span> </td> 
   <td colname="3"> Define una pista de subtítulos cerrados como la pista de subtítulos opcionales actual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Pistas de audio alternativas</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasAlternateAudio(); </span> </td> 
   <td colname="3"> True si el flujo tiene pistas de audio alternativas. <p>Nota:  La pista de audio principal (predeterminada) también forma parte de la lista de pistas de audio alternativas. </p> <p>TVSDK para Android considera que la pista de audio principal es uno de los elementos de la lista de pistas de audio alternativas. Debido a esto, el único caso en el que <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> devuelve false es cuando el flujo no tiene audio. Si el contenido solo tiene una pista de audio, este método devuelve true y <span class="codeph"> MediaPlayerItem.getAudioTracks </span> devuelve una lista con un solo elemento (la pista de audio predeterminada). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;AudioTrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> Proporciona una lista de pistas de audio alternativas disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> Recupera la pista de audio seleccionada con <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> Selecciona una pista de audio para que sea la pista de audio actual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Metadatos temporizados</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata(); </span> </td> 
   <td colname="3"> True si el flujo tiene metadatos temporizados asociados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;TimedMetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> Proporciona una lista de los objetos de metadatos temporizados asociados al flujo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Varios perfiles (velocidades de bits)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic(); </span> </td> 
   <td colname="3"> True si el flujo es un flujo de velocidad de bits múltiple (MBR). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;Profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> Proporciona una lista de los perfiles de velocidad de bits asociados. Para cada perfil, puede recuperar su velocidad de bits y la altura y anchura del perfil. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Perfil getSelectedProfile() </span> </td> 
   <td colname="3"> Recupera el perfil seleccionado actualmente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Juego de trucos</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported(); </span> </td> 
   <td colname="3"> True si el reproductor admite avance rápido, rebobinado y reanudación. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> Proporciona la lista de las tasas de reproducción disponibles en el contexto de la función de reproducción mediante trucos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Float getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> Recupera la velocidad de reproducción seleccionada actualmente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> Devuelve la <span class="codeph"> instancia MediaPlayerItemConfig </span> asociada a este elemento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Recurso multimedia</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> Devuelve el recurso de medios asociado a este elemento. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> Devuelve el identificador de medios asociado a este elemento. Este ID se establece cuando el elemento se carga mediante <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
