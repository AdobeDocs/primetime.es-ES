---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
title: Métodos de MediaPlayer para acceder a la información de MediaResource
exl-id: 8849411a-e94b-43a9-9fa1-143725264304
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '405'
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
   <td colname="1"> <b>Etiquetas de publicidad</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> <p>Proporciona la lista de etiquetas de anuncio que se utilizan en el proceso de colocación de anuncios. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Emisión en directo</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isLive(); </span> </td> 
   <td colname="3"> <p>True si el flujo está activo; False si es VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Protegido por DRM</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isProtected(); </span> </td> 
   <td colname="3"> <p>True si el flujo está protegido mediante DRM. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;drmmetadatainfo&gt; getDRMetadataInfos(); </span> </td> 
   <td colname="3"> <p>Enumera todos los objetos de metadatos DRM detectados en el manifiesto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Subtítulos opcionales</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasClosedCaptions(); </span> </td> 
   <td colname="3"> <p>True si están disponibles las pistas de subtítulos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;closedcaptionstrack&gt; getClosedActionsTracks(); </span> </td> 
   <td colname="3"> <p>Proporciona una lista de las pistas de subtítulos opcionales disponibles. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedCaptionsTrack(); </span> </td> 
   <td colname="3"> <p>Recupera la pista de subtítulos seleccionados actualmente con <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> <p>Define una pista de subtítulos para que sea la pista de subtítulos cerrados actual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Pistas de audio alternativas</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio(); </span> </td> 
   <td colname="3"> <p>True si el flujo tiene pistas de audio alternativas. </p> <p>Sugerencia: La pista de audio principal (predeterminada) también forma parte de la lista de pistas de audio alternativas. </p> <p>TVSDK para Android considera que la pista de audio principal es uno de los elementos de la lista de pistas de audio alternativas. Debido a esto, el único caso donde <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> devuelve "false" cuando el flujo no tiene audio. Si el contenido solo tiene una pista de audio, este método devuelve true y <span class="codeph"> MediaPlayerItem.getAudioTracks </span> devuelve una lista con un solo elemento (la pista de audio predeterminada). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> Proporciona una lista de pistas de audio alternativas disponibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> <p>Proporciona una lista de pistas de audio alternativas disponibles. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> <p>Recupera la pista de audio seleccionada con <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> <p>Selecciona una pista de audio para que sea la pista de audio actual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Metadatos cronometrados</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasTimedMetadata(); </span> </td> 
   <td colname="3"> <p>True si el flujo tiene metadatos sincronizados asociados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;timedmetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> <p>Proporciona una lista de los objetos de metadatos cronometrados asociados a la secuencia. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isDynamic(); </span> </td> 
   <td colname="3"> <p>True si el flujo es un flujo de velocidad de bits múltiple (MBR). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> <p>Proporciona una lista de los perfiles de velocidad de bits asociados. Para cada perfil, puede recuperar su velocidad de bits y la altura y anchura del perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Juego de trucos</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isTrickPlaySupported(); </span> </td> 
   <td colname="3"> <p>True si el reproductor admite avance rápido, rebobinado y reanudación. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates </span> </td> 
   <td colname="3"> <p>Proporciona la lista de velocidades de reproducción disponibles en el contexto de la función de truco. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Recurso de medios</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource.getResource(); </span> </td> 
   <td colname="3"> <p>Devuelve el recurso multimedia asociado a este elemento. </p> </td> 
  </tr> 
 </tbody> 
</table>
