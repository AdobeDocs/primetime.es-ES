---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
title: Métodos MediaPlayerItem para acceder a la información de MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
   <td colname="2"> <span class="codeph"> Lista&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> Proporciona la lista de etiquetas de anuncio que se utilizan en el proceso de colocación de anuncios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Emisión en directo</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isLive(); </span> </td> 
   <td colname="3"> True si el flujo está activo; False si es VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Protegido por DRM</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isProtected(); </span> </td> 
   <td colname="3"> True si el flujo está protegido mediante DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;drmmetadatainfo&gt; getDRMetadataInfos(); </span> </td> 
   <td colname="3"> Enumera todos los objetos de metadatos DRM detectados en el manifiesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Subtítulos opcionales</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasClosedCaptions(); </span> </td> 
   <td colname="3"> True si están disponibles las pistas de subtítulos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;closedcaptionstrack&gt; getClosedActionsTracks(); </span> </td> 
   <td colname="3"> Proporciona una lista de las pistas de subtítulos opcionales disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedCaptionsTrack(); </span> </td> 
   <td colname="3"> Recupera la pista de subtítulos seleccionados actualmente con <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> Define una pista de subtítulos para que sea la pista de subtítulos cerrados actual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Pistas de audio alternativas</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio(); </span> </td> 
   <td colname="3"> True si el flujo tiene pistas de audio alternativas. <p>Nota: La pista de audio principal (predeterminada) también forma parte de la lista de pistas de audio alternativas. </p> <p>TVSDK para Android considera que la pista de audio principal es uno de los elementos de la lista de pistas de audio alternativas. Debido a esto, el único caso donde <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> devuelve "false" cuando el flujo no tiene audio. Si el contenido solo tiene una pista de audio, este método devuelve true y <span class="codeph"> MediaPlayerItem.getAudioTracks </span> devuelve una lista con un solo elemento (la pista de audio predeterminada). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
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
   <td colname="2"> <b>Metadatos cronometrados</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasTimedMetadata(); </span> </td> 
   <td colname="3"> True si el flujo tiene metadatos sincronizados asociados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;timedmetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> Proporciona una lista de los objetos de metadatos cronometrados asociados a la secuencia. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Varios perfiles (tasas de bits)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isDynamic(); </span> </td> 
   <td colname="3"> True si el flujo es un flujo de velocidad de bits múltiple (MBR). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;profile&gt; getProfiles(); </span> </td> 
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
   <td colname="2"> <span class="codeph"> booleano isTrickPlaySupported(); </span> </td> 
   <td colname="3"> True si el reproductor admite avance rápido, rebobinado y reanudación. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> Proporciona la lista de velocidades de reproducción disponibles en el contexto de la función de truco. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Flotante getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> Recupera la velocidad de reproducción seleccionada actualmente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> Devuelve el <span class="codeph"> MediaPlayerItemConfig </span> instancia asociada a este elemento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Recurso de medios</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource.getResource(); </span> </td> 
   <td colname="3"> Devuelve el recurso multimedia asociado a este elemento. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> Devuelve el identificador de medios asociado con este elemento. Este ID se establece cuando el elemento se carga mediante <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
