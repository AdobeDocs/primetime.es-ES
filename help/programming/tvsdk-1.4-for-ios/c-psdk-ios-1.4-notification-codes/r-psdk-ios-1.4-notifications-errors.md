---
description: Esta tabla proporciona información detallada sobre las notificaciones de tipo ERROR.
title: Códigos de notificación de ERROR
exl-id: dc65670e-4764-4d68-aee1-87b2d27b09b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 5%

---

# Códigos de notificación de ERROR{#error-notification-codes}

Esta tabla proporciona información detallada sobre las notificaciones de tipo ERROR.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

La mayoría de los errores contienen metadatos relevantes como, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Código </th> 
   <th colname="2" class="entry"> Nombre </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> Claves de metadatos </th> 
   <th colname="5" class="entry"> Comentarios </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE </span><span class="codeph"> MINOR_DRM_CODE </span><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"></td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reproducción</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"></td> 
   <td colname="4"></td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101001 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_PLAYBACK_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span><span class="codeph"> INTERNAL_ERROR </span><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> <p>Error al realizar una operación de búsqueda. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>Se ha producido un error al realizar una operación de pausa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101101 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> <p>  </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Medio no válido</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102000 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_MEDIA_PLAYER_ITEM </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Procesamiento de publicidad</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_ INVALID </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED</span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>Error de resolución de publicidad debido a un formato de metadatos de anuncio no válido. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>Error en la fase de resolución de anuncios. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>Se ha producido un error de iOS de bajo nivel. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Configuración</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> ERROR DE SET_CC_VISIBILITY_ </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>Se ha producido un error al tratar de cambiar la visibilidad de las pistas CC. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> ERROR DE SET_CC_STYLING_ </span> </td> 
   <td colname="3"> <span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>Se ha producido un error al tratar de cambiar las opciones de estilo de las pistas CC. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS único</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_VERSION_ INCOMPATIBLE </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>La versión HLS de los anuncios es más alta que la versión HLS del contenido. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170001 </span> </td> 
   <td colname="2"><span class="codeph"> ARGUMENT_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> <p>Error de argumento </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170002 </span> </td> 
   <td colname="2"><span class="codeph"> M3U8_PARSER_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"> <p>No se pudo analizar m3u8. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170003 </span> </td> 
   <td colname="2"><span class="codeph"> WEBVTT_PARSER_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> <p>No se ha podido analizar Webvtt. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170004 </span> </td> 
   <td colname="2"><span class="codeph"> HLS_SEGMENT_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>El segmento supera el ancho de banda especificado para la variante. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170005 </span> </td> 
   <td colname="2"><span class="codeph"> MBR_MEDIASEQUENCE_OFFSYNC </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> <p>El número de secuencia de medios no está sincronizado en todos los flujos HLS de este MBR. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170006 </span> </td> 
   <td colname="2"><span class="codeph"> MISSING_FILE_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>Falta el archivo o no responde. </p> <p>HTTP 404: archivo no encontrado. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170007 </span> </td> 
   <td colname="2"><span class="codeph"> AD_EMPTY_RESPONSE </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> <p>No se han podido recuperar los anuncios. Respuesta vacía. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TIMEOUT </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> <p>No se han podido recuperar los anuncios. Error de espera. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170009 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> <p>Error al cambiar la pista de subtítulos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170010 </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_ERROR </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"> <p>Error de SiteCatalyst. Consulte la descripción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170011 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TARGET_DURATION_INCOMPATIBLE </span> </td> 
   <td colname="3"> Ninguno </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>La DURACIÓN OBJETIVO del anuncio es mayor que la DURACIÓN OBJETIVO del contenido. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID y la fuente (URL) se pueden recuperar mediante la variable `PTAdAsset` en los metadatos de notificación con `AD_ASSET` clave.
