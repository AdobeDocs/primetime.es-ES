---
description: Puede usar la siguiente información para ayudarlo a despellejar al reproductor. Para cada construcción visual, los comportamientos correspondientes se mencionan en el comportamiento predeterminado.
title: Despellejar al reproductor
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Despellejar al reproductor {#skinning-the-player}

Puede usar la siguiente información para ayudarlo a despellejar al reproductor. Para cada construcción visual, los comportamientos correspondientes se mencionan en el comportamiento predeterminado.

>[!IMPORTANT]
>
>Los detalles de desollado de este documento son para los elementos de interfaz de usuario predeterminados que crea el marco de trabajo de la interfaz de usuario. Si el reproductor ha modificado estos elementos, también es necesario cambiar los elementos de desollado.

## Divisas de contenedor {#section_99B0D598219D4150B57E97D5381B118F}

Estos son los estilos para los divs de contenedor:

>[!TIP]
>
>Estos divs se enumeran en la `common-styles.css` archivo.

Estos son los estilos para el div principal:

<table id="table_AC5745DF725543ADBBCD68BA6130DF12"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><b>Div principal</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-main-video-div-style</span> </td> 
   <td colname="col2"> <p>Estilo del div principal en el que se reproduce el vídeo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .pip-mode-active</span> </td> 
   <td colname="col2"> <p>Se utiliza cuando el modo PIP está activo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> videoBehavior</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>Imagen en imagen (PIP)</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-pip-video-div</span> </td> 
   <td colname="col2"> <p>Estilo del div en el que se reproduce el vídeo PIP. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .view-as-main-video</span> </td> 
   <td colname="col2"> <p>Se aplica a la PIP inicial cuando se ha intercambiado y se muestra como vídeo principal. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>Vista de varios vídeos</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-multi-view-container</span> </td> 
   <td colname="col2"> <p>Se utiliza en la vista de varios vídeos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-multi-view-view</span> </td> 
   <td colname="col2"> <p>Un estilo css común que se coloca en cada vídeo de la vista múltiple. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .multiview</span> </td> 
   <td colname="col2"> <p>Cuando el contenedor que aloja cada uno de los vídeos en vista multivariable está en vista multivariable. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Varios controles {#section_E9E4A8E3AEBF4BDC89840B84B3B0E737}

Estos son los estilos para los controles de reproductor genéricos:

>[!TIP]
>
>Estos estilos se enumeran en la variable `default-controls.css` archivo.

<table id="table_0ACB6BAB5DAD42DBBD18CA7C0385A261"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control</span> </td> 
   <td colname="col2"> <p>Aplicable a todos los controles de la barra de control, excepto al depurador y al espacio </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-input-slider</span> </td> 
   <td colname="col2"> <p>Reguladores de entrada </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-header</span> </td> 
   <td colname="col2"> <p>Encabezado de los paneles </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-vertical-list-menu-item</span> </td> 
   <td colname="col2"> <p>Lista de menús en estilo vertical </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-fill-spacer</span> </td> 
   <td colname="col2"> <p>Espacio en la barra de control </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-hr-separator</span> </td> 
   <td colname="col2"> <p>Separador de reglas horizontales </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-title</span> </td> 
   <td colname="col2"> <p>Título de los paneles </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-close-btn</span> </td> 
   <td colname="col2"> <p>Botón para cerrar el panel </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-button-background</span> </td> 
   <td colname="col2"> <p>Fondo de todos los botones </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-txt-control</span> </td> 
   <td colname="col2"> <p>Estilos predeterminados para los controles de texto. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Barra de control {#section_B683B51EC746484B9AA90CB481D637BD}

Estos son los estilos de la barra de control:

<table id="table_681E13F264674F849FAA2523EB65F094"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control-bar</span> (comportamiento predeterminado)</td>
   <td colname="col2"> <p>Aplicable para la barra de control </p> </td> 
  </tr> 
 </tbody> 
</table>

## Botones de función {#section_57FFD242FF674EA2867BCF6CA7F6B855}

>[!NOTE]
>
>Las letras de las tablas siguientes corresponden a las letras de esta ilustración.

Estos son los estilos de la barra de desplazamiento:

<table id="table_2207AD72E72A47FFA03AC748F06A54FD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo (A) </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar</span> </td> 
   <td colname="col2"> <p>Barra de desplazamiento en la barra de control </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-buffer-progress-bar</span> </td> 
   <td colname="col2"> <p>Barra de progreso del búfer en la barra de desplazamiento </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-seek-to-bar</span> </td> 
   <td colname="col2"> <p>Estado de la barra de desplazamiento cuando el usuario realiza una búsqueda en ella </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-playback-progress-bar</span> </td> 
   <td colname="col2"> <p>Estado de la barra de desplazamiento en la reproducción normal </p> </td> 
  </tr>
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-progress-bar-play-head</span> </td>
   <td colname="col2"> <p>Reproducir la cabeza en la barra de desplazamiento mientras se reproduce </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad-marker-bar</span> </td>
   <td colname="col2"> <p>Barra de marcador de anuncio </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad-marker</span> </td>
   <td colname="col2"> <p>Marcador de anuncio </p> </td>
  </tr>
 </tbody>
</table>

Los comportamientos predeterminados son:

* `scrubBarBehavior`
* `bufferProgressBarBehavior`
* `playHeadBehavior`
* `playProgressBarBehavior`
* `seekToBarBehavior`

## Botón Reproducir/Pausa {#section_F1F40A948D0049C5A4D8EA5F2A475CAA}

Estos son los estilos del botón de reproducción/pausa:

<table id="table_975C2293222A4782A8C75A6149C1AD27">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (B) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause</span> </td>
   <td colname="col2"> <p>Botón Reproducir pausa en la barra de control. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td>
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> en estado de pausa </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td> 
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> en estado de reproducción </p> </td>
  </tr>
 </tbody>
</table>

El comportamiento predeterminado es `playPauseButtonBehavior`.

## Volumen {#section_23E17BD2343948F8A2CEE1C8BEE2F874}

Estos son los estilos para configurar el botón de volumen:

<table id="table_8F9831F36A4D427CA31C9FFA4173170D">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (C) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><span class="codeph"> .ptp-volume-control</span>
     <ul id="ul_B12ADDFB83EA40FD8B4E92AF418AA4B4">
      <li id="li_7DA8143A69ED4E7D8A560B9FF75D6BA7"><span class="codeph"> .expandido</span> </li>
      <li id="li_D8CCAD45D81C4850B6903FE261833AE6"><span class="codeph"> .vertical</span> </li>
     </ul> </p> </td>
   <td colname="col2"> <p>Control de volumen en la barra de control
     <ul id="ul_2C60F018FDCB458885738AC378C02F61">
      <li id="li_6B19572B504A4BBF9C97DC29C0E92A1D">Cuando el control está expandido </li>
      <li id="li_6489E422E1944D5194CBDFC8383D2F30">Cuando el control está en forma vertical </li>
     </ul> </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume</span> </td>
   <td colname="col2"> <p>Botón Volumen de la barra de control </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.min-volume-state</span> </td>
   <td colname="col2"> <p>Cuando el volumen está en estado mínimo </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.mute-state</span> </td>
   <td colname="col2"> <p>Cuando el volumen está en estado silencioso </p> </td>
  </tr>
 </tbody>
</table>

Los comportamientos predeterminados son `volumeBehavior` y `muteButtonBehavior`.

Estos son los estilos del regulador de volumen:

<table id="table_E3DC93F8FC614C30AADAE259D18F10EF">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (D) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-slider</span> </td>
   <td colname="col2"> <p>El regulador de volumen. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-hidden</span> </td>
   <td colname="col2"> <p>El regulador de volumen está en estado oculto. </p> </td>
  </tr>
 </tbody>
</table>

El comportamiento predeterminado es `volumeSliderBehavior`.

## Rebobinar {#section_06EE608FC54A4CF5B5DF9DC743CFC740}

Este es el estilo del botón de rebobinado:

<table id="table_0ACB116582D54B188E9F5B5C03D3A615">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (E) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>Botón de rebobinado de la barra de control. </p> </td>
  </tr>
 </tbody>
</table>

El comportamiento predeterminado es `rewindButtonBehavior`.

## Hora {#section_0E6549B3DF6D4C10947D445A5F8EEA7F}

Este es el estilo para mostrar el tiempo restante en la barra de control:

<table id="table_CEE62BFF5FB04FDCBBE1331E0D727EBA">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (F) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-txt-display-time</span> </td>
   <td colname="col2"> <p>Muestra el tiempo restante en la barra de control </p> </td>
  </tr>
</tbody>
</table>

El comportamiento predeterminado es `timeRemainingBehavior`.

## Rebobinado rápido {#section_F6E6C65BD3BD493A89915DF9B92933BA}

Este es el estilo del botón de rebobinado rápido:

<table id="table_25BB4966B709402383AB6A6822FC1999">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (G) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>Botón de rebobinado rápido de la barra de control. </p> </td>
  </tr>
 </tbody>
</table>

El comportamiento predeterminado es `fastRewindButtonBehavior`.

## Rebobinado lento {#section_38A22BB8681B430F8C6808C3BD21FB4E}

Este es el estilo del botón de rebobinado lento:

<table id="table_E623C374622A497C91E22333D77AF8F6">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (H) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-slowRewind</span> </td>
   <td colname="col2"> <p>Botón de rebobinado lento de la barra de control. </p> </td>
  </tr>
 </tbody>
</table>

El comportamiento predeterminado es `slowRewindButtonBehavior`.

## Avance lento {#section_92ACF092EECC4A5EAF6AA090C05E552E}

Este es el estilo del botón de avance lento:

<table id="table_88C1CF5DB2D84EDBA01AC62B70509B08">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (I) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-slow-forward</span> </td>
   <td colname="col2"> <p>Botón de avance lento de la barra de control. </p> </td>
  </tr>
 </tbody>
</table>

El comportamiento predeterminado es `slowForwardButtonBehavior`.

## Avance rápido {#section_F90ED8B3739B49ACAB1F12DF18F0E4D6}

Este es el estilo del botón de avance rápido:

<table id="table_F166BD1E8B934B34AF3690BBBAD894B7">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (J) </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastforward</span> </td>
   <td colname="col2"> <p>Botón de avance rápido de la barra de control. </p> </td>
  </tr>
 </tbody>
</table>

El comportamiento predeterminado es `fastForwardButtonBehavior`.

## Pista de audio {#section_1CDF4FA5A1C14DB6B9C96579FFA1057C}

Estos son los estilos para configurar la pista de audio:

<table id="table_22FC521D786B45EB84F230894FFECE79">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Botón Pista de audio (K)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-audio-track</span> </td>
   <td colname="col2"> <p>Botón de pista de audio de la barra de control. </p> </td>
  </tr>
  <tr>
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> audioTrackButtonBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Panel de selección de pista de audio (L)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-panel</span> </td> 
   <td colname="col2"> <p>Panel para seleccionar la pista de audio. </p> </td>
  </tr>
  <tr>
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> audioTrackSelectionPanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Encabezado de selección de pista de audio (M)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>El encabezado del <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Menú de selección de pistas de audio (N)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-menu</span> </td>
   <td colname="col2"> <p>Los elementos de menú del <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
 </tbody>
</table>

## Uso compartido {#section_B2ADC76E76304A68AD648A00A12B676E}

Estos son los estilos para configurar el uso compartido:

<table id="table_3264C472809D462B8FC16680B96B1AC9">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Botón Compartir en redes sociales (O)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video</span> </td> 
   <td colname="col2"> <p>Botón de uso compartido de medios sociales en la barra de control que se abrirá <span class="codeph"> ptp-share-video-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> shareVideoButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Compartir panel de vídeo (P)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel</span> </td>
   <td colname="col2"> <p>Panel que muestra las opciones de uso compartido en redes sociales. </p> </td>
  </tr>
  <tr>
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> shareVideoPanelBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Menú Compartir Vídeo (Q)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>El encabezado del <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .share-video-panel-menu</span> </td>
   <td colname="col2"> <p>El menú de <span class="codeph"> ptp-share-video-panel</span> que muestra todas las opciones para compartir contenido en medios sociales. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel-menu-item</span> </td>
   <td colname="col2"> <p>El elemento de menú del <span class="codeph"> share-video-panel-menu</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-facebook</span> </td>
   <td colname="col2"> <p>Elemento de menú que le permite compartir contenido en Facebook. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-twitter</span> </td>
   <td colname="col2"> <p>Elemento de menú que le permite compartir contenido en el Twitter. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-google-plus</span> </td>
   <td colname="col2"> <p>Elemento de menú que le permite compartir contenido en Google Plus. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-linkedin</span> </td>
   <td colname="col2"> <p>Elemento de menú que le permite compartir contenido en LinkedIn. </p> </td>
  </tr>
 </tbody>
</table>

## Subtítulos opcionales {#section_A01BA68218564DA0B7D6BF51F045D7AB}

Estos son los estilos para configurar subtítulos:

<table id="table_777C7034C9424F8C841DABD480FFAC47">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo </th>
   <th colname="col2" class="entry"> Descripción </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Botón Subtítulos (R)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-closed-caption</span> </td>
   <td colname="col2"> <p>El <span class="uicontrol"> Subtítulos opcionales</span> en la barra de control. </p> </td>
  </tr>
  <tr>
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> closedCaptionButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .on-state</span> </td>
   <td colname="col2"> <p>Se han habilitado los subtítulos para un vídeo. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Panel De Subtítulos (S)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-panel</span> </td>
   <td colname="col2"> <p>Panel para subtítulos cerrados. </p> </td>
  </tr>
  <tr>
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> closedCaptionLanguagePanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Idiomas de los subtítulos (T)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-panel:</span> </td>
   <td colname="col2"> <p>El encabezado del <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-menu: </span> </td>
   <td colname="col2"> <p>Menú en el panel de subtítulos. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Opciones de subtítulos (U)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-btn</span> </td>
   <td colname="col2"> <p>El <span class="uicontrol"> Opciones</span> en el panel de opciones de subtítulos. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-panel</span> </td>
   <td colname="col2"> <p>El panel Opciones del panel de subtítulos opcionales. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-menu-item</span> </td>
   <td colname="col2"> <p>Elemento de menú del panel de subtítulos. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .selected</span> </td>
   <td colname="col2"> <p>En el estado seleccionado. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-done-btn</span> </td> 
   <td colname="col2"> <p>El <span class="uicontrol"> Listo</span> en el encabezado del panel de opciones de subtítulos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-menu</span> </td> 
   <td colname="col2"> <p>El menú Opciones en subtítulos opcionales. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-main-menu</span> </td> 
   <td colname="col2"> <p>Menú principal de las opciones de subtítulos opcionales. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-sub-menu</span> </td> 
   <td colname="col2"> <p>El submenú para las opciones de subtítulos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-opacity-slider</span> </td> 
   <td colname="col2"> <p>El control deslizante de opacidad para las opciones de subtítulos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-separator</span> </td> 
   <td colname="col2"> <p>El separador de opciones de subtítulos opcionales. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-item</span> </td> 
   <td colname="col2"> <p>El pie de ilustración cerrado <span class="uicontrol"> Opciones</span> elemento de menú. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-preview-panel</span> </td> 
   <td colname="col2"> <p>El panel de vista previa de subtítulos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-footer</span> </td> 
   <td colname="col2"> <p>Pie de página de opciones de subtítulos opcionales. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-reset-button</span> </td> 
   <td colname="col2"> <p>El <span class="uicontrol"> Restablecer</span> en el pie de página del panel de opciones de subtítulos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-apply-button</span> </td> 
   <td colname="col2"> <p>El <span class="uicontrol"> Aplicar</span> en el pie de página del panel de opciones de subtítulos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> closedCaptionOptionsPanelBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## Más opciones (V) {#section_18E25CF8A8964FFD9026A8A833089CE3}

Estos son los estilos para configurar opciones adicionales:
<table id="table_EC6EF88E2EDE4B8EBB1C14F87A6161FA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options</span> </td> 
   <td colname="col2"> <p>El <span class="uicontrol"> Más opciones</span> botón. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options.ptp-control-bar-btn</span> </td> 
   <td colname="col2"> <p>El <span class="codeph"> ptp-btn-more-options</span> que se utilizan en la barra de control. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel</span> </td> 
   <td colname="col2"> <p>Panel de control Más opciones. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu</span> </td> 
   <td colname="col2"> <p>Menú del panel de control Más opciones. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu-item</span> </td> 
   <td colname="col2"> <p>Elemento de menú del panel de control Más opciones. </p> </td> 
  </tr> 
 </tbody> 
</table>

El comportamiento predeterminado es `moreOptionsButtonBehavior`.

## Botón PIP (W) {#section_1EE039DEA99541D391B30BD1DF72A83E}

Este es el estilo de la [!UICONTROL PIP<] botón:

<table id="table_EE2E882C87E24D39B8D5347686F29E55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-pip</span> </td> 
   <td colname="col2"> <p>Botón PIP de la barra de control. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> pipButtonBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## Pantalla Completa (X) {#section_158A19DFB30E4432A67E4A74A7CBA563}

Este es el estilo para configurar la pantalla completa:

<table id="table_5941835F31AC4E9CBA9702AB8D813B8F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-fullscreen</span> </td> 
   <td colname="col2"> <p>El <span class="uicontrol"> Pantalla completa</span> botón de la barra de control. </p> </td> 
  </tr> 
 </tbody> 
</table>

El comportamiento predeterminado es `fullScreenButtonBehavior`.

## Juego de trucos (Y) {#section_AE6F83BB7EE2497FB13CD94A8316192D}

Este es el estilo para configurar el juego de trucos:

<table id="table_F1ADAC0A4B4E48669828690BDEB4BC09"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-control-bar-trick-play-rate</span> </td> 
   <td colname="col2"> <p>El componente de visualización de la tasa de trucos en la barra de control. </p> </td> 
  </tr> 
 </tbody> 
</table>

El comportamiento predeterminado es `trickPlayRateDisplayBehavior`.

## Vista múltiple (Z) {#section_58EFAE7263BA45D3A4E2AB7309A9CAA7}

Este es el estilo para configurar una vista múltiple:

<table id="table_84B37D7410EE40DFA7A8BB8431C6DCF0"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-multiview</span> </td> 
   <td colname="col2"> <p>El <span class="uicontrol"> MultiView</span> botón de la barra de control y el estado inicial de <span class="uicontrol"> Vista múltiple</span> botón. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">El comportamiento predeterminado es <span class="codeph"> multiViewButtonBehavior</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
 </tbody> 
</table>

## Miniatura {#section_0AFD932975634BB08387EEE7D3BFC438}

Este es el estilo para configurar las miniaturas:

<table id="table_968136A8BBA042A7A8E79739B8F92F55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-progress-bar-thumb-nail</span> </td> 
   <td colname="col2"> <p>La barra de progreso de las miniaturas. </p> </td> 
  </tr> 
 </tbody> 
</table>

El comportamiento predeterminado es `thumbnailPreviewBehavior`.

## Mensajes de error {#section_AC9858EE1B5A4FF4947E383C663B6AB5}

Este es el estilo para configurar los mensajes de error:

<table id="table_7F4C156170DB4AFFA7DEE06F00449506"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel</span> </td> 
   <td colname="col2"> <p>Panel que muestra los mensajes de error del reproductor. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-icon</span> </td> 
   <td colname="col2"> <p>El icono que se muestra en el panel cuando hay un mensaje de error. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-message</span> </td> 
   <td colname="col2"> <p>El mensaje de error que se muestra. </p> </td> 
  </tr> 
 </tbody> 
</table>

El comportamiento predeterminado es `errorMessagePanelBehavior`.

## Superposición de almacenamiento en búfer {#section_2FE8FDE2599E42BAA7411D0D38FA0A88}

Este es el estilo para configurar las miniaturas:

<table id="table_1FECE1DC29B8434B886751A29455F004"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-buffering-overlay</span> </td> 
   <td colname="col2"> <p>El control de superposición de almacenamiento en búfer. </p> </td> 
  </tr> 
 </tbody> 
</table>

La superposición predeterminada es `bufferingOverlayBehavior`.

## Selectores específicos {#section_51F735AEF82E41E890FF59E031A0DB89}

Este es el estilo del botón de avance rápido:

<table id="table_E77EDC7D227348E79C7E73FB5D46F992"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ad-break</span> </td> 
   <td colname="col2"> <p>Estado del panel de control mientras se reproduce el anuncio. </p> <p>Se aplica a lo siguiente: 
     <ul id="ul_D5076303DCD94D968682289823D1A9F2"> 
      <li id="li_4290C4B2D48546E3AD023BED6CAAE395"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_72A3D3E916E44A55BA170407EAB0527D"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_A0BAEBB0E01B402EB83E3CE9B92B15CC"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_FDF2CEDB0A854098907FF9CBCF1A61C1"><span class="codeph"> .ptp-btn-slow-forward</span> </li> 
      <li id="li_CD2E14DB3DD64C10A253DA23FBE04A04"><span class="codeph"> .ptp-btn-slow-forward</span> </li> 
      <li id="li_A230359E8F7F4571A9EBFF0E4C2462D7"><span class="codeph"> .ptp-btn-slowRewind</span> </li> 
      <li id="li_5711A315872F4FA59FDDF0EF0AFD03C6"><span class="codeph"> .ptp-btn-more-options </span> </li> 
      <li id="li_71C8E76077A84ED590160AB5ABFCC0D7"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_4A3113C0360F4F708AAA96AB316FA057"><span class="codeph"> .ptp-btn-closed-caption </span> </li> 
      <li id="li_901A0186D65A48A1B774DC555CEC5367"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
      <li id="li_2331583C01C2482B8EE72979FBF111DB"><span class="codeph"> .ptp-btn-pip </span> </li> 
      <li id="li_7BB39BDF5E294AEB8FA3DCD9F9A29468"><span class="codeph"> .ptp-btn-rewind</span> </li> 
      <li id="li_E4FEF5A7486A40F6A5FE1119BD63AFEF"><span class="codeph"> .ptp-scrub-bar</span> </li> 
      <li id="li_12153547558A4871842EE0416BCCA8B2"><span class="codeph"> .ptp-seek-to-bar</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .multi-view</span> </td> 
   <td colname="col2"> <p>El estado del control mientras está en vista multivariable. </p> <p>Se aplica a lo siguiente: 
     <ul id="ul_A8AC653C30814AC49041F3B58A2106F4"> 
      <li id="li_0407167DA21647A8A6960DFE55A33F42"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_EA71CAF41CDC41DE859A85CE482BE97C"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_F3A998C51A034C22A914EAEFF19FFEA7"><span class="codeph"> .ptp-btn-closed-caption</span> </li> 
      <li id="li_022F871ABC894C9BA879B3AF3D341202"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .fullscreen-state</span> </td> 
   <td colname="col2"> <p>El reproductor está en modo de pantalla completa. </p> <p>Se aplica a lo siguiente: 
     <ul id="ul_B235C1D339F64B2FAC6BC72F03807616"> 
      <li id="li_6E050EE74C604FDAB4C9C0447F547A9D"><span class="codeph"> .ptp-control-bar </span> </li> 
      <li id="li_67D54B1A41764B2DA544479CDA1C901C"><span class="codeph"> .ptp-btn-fullscreen</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
