---
description: Puede utilizar la API del reproductor de Primetime para personalizar el comportamiento del reproductor. Estas clases describen el reproductor de contenidos y su recurso.
title: Clases de Mediacore
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---

# Clases de Mediacore{#mediacore-classes}

Puede utilizar la API del reproductor de Primetime para personalizar el comportamiento del reproductor. Estas clases describen el reproductor de contenidos y su recurso.

Para ver la documentación completa de la API para TVSDK, vaya a [Referencias de API de Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html).

Estas clases describen el reproductor de contenidos y sus recursos.
Paquete: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>Nombre </p> </th> 
   <th colname="2" class="entry"> <p>Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> ABRControlParameters</a> </span> </td> 
   <td colname="2"> Clase que encapsula todos los parámetros de control de velocidad de bits adaptable. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> BufferControlParameters</a></span> </td> 
   <td colname="2"> Clase que encapsula todos los parámetros de control de búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionStyles.html" format="html" scope="external"> ClosedCaptionsStyles</a></span> </td> 
   <td colname="2"> Clase que define todas las propiedades de estilo del texto en subtítulos opcionales. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionsVisibility.html" format="html" scope="external"> ClosedCaptionsVisibility</a></span> </td> 
   <td colname="2"> Clase que controla si los subtítulos opcionales están visibles. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ContentFactory.html" format="html" scope="external"> ContentFactory</a> </span> </td> 
   <td colname="2"> Clase base de fábrica para crear y administrar varios componentes utilizados en el flujo de trabajo de publicidad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> Implementación predeterminada para comportamientos de reproducción de publicidad. Interfaz que permite a las aplicaciones personalizar los comportamientos de los anuncios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultContentFactory.html" format="html" scope="external"> DefaultContentFactory</a></span> </td> 
   <td colname="2">Implementación predeterminada de <span class="codeph"> MediaPlayerClient</span> de fábrica que proporciona soporte para el proceso de resolución de anuncios y metadatos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2">Implementación de clase predeterminada de <span class="codeph"> MediaPlayer</span> interfaz. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerConfig.html" format="html" scope="external"> DefaultMediaPlayerConfig</a> </span> </td> 
   <td colname="2"> Clase de configuración para la implementación predeterminada del reproductor de contenidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> Clase de configuración predeterminada del elemento del reproductor de contenidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemLoader.html" format="html" scope="external"> DefaultMediaPlayerItemLoader</a></span> </td> 
   <td colname="2"> Cargador de elementos del reproductor de medios predeterminado. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a></span> </td> 
   <td colname="2">Interfaz pública para <span class="codeph"> DefaultMediaPlayer</span> clase. Incluye enumeraciones para Event, PlayerState y Visibility. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerConfig.html" format="html" scope="external"> MediaPlayerConfig</a> </span> </td> 
   <td colname="2"> Clase de configuración del reproductor de contenidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerContext.html" format="html" scope="external"> MediaPlayerContext</a></span> </td> 
   <td colname="2"> Clase que proporciona contexto adicional al reproductor de contenidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a></span> </td> 
   <td colname="2"> Interfaz que representa los medios de audio-vídeo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> Clase de configuración predeterminada del elemento del reproductor de contenidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a></span> </td> 
   <td colname="2">Clase que carga un recurso de reproductor de contenidos y crea el correspondiente <span class="codeph"> MediaPlayerItem</span> objeto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerStatus.html" format="html" scope="external"> MediaPlayerStatus</a></span> </td> 
   <td colname="2"> Clase que contiene los estados compatibles del reproductor de contenidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a></span> </td> 
   <td colname="2">Clase para la vista que utilizará la variable <span class="codeph"> MediaPlayer</span> para el procesamiento de vídeo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> MediaResource</a></span> </td> 
   <td colname="2"> Clase que ajusta toda la información sobre un recurso multimedia. Incluye una enumeración para el tipo de recurso de medios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResourceType.html" format="html" scope="external"> MediaResourceType</a></span> </td> 
   <td colname="2"> Clase que contiene los tipos de recursos multimedia admitidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a></span> </td> 
   <td colname="2"> Clase que encapsula las etiquetas personalizadas utilizadas por el reproductor de medios al realizar la colocación de anuncios, además de las etiquetas de referencia predeterminadas. También incluye los nombres de etiquetas sobre los que la aplicación desea recibir notificaciones. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> TextFormat</a></span> </td> 
   <td colname="2"> Interfaz que encapsula distintos atributos que describen un estilo de texto (por ejemplo, el estilo de subtítulos opcionales). </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> Versión</a></span> </td> 
   <td colname="2"> Clase que proporciona la versión y descripción de TVSDK. </td> 
  </tr> 
 </tbody> 
</table>
