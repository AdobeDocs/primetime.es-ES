---
description: Esta tabla proporciona información detallada sobre las notificaciones de tipo ERROR.
title: Códigos de notificación de ERROR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 4%

---


# Códigos de notificación de ERROR{#error-notification-codes}

Esta tabla proporciona información detallada sobre las notificaciones de tipo ERROR.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

La mayoría de los errores contienen metadatos relevantes, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

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
   <td colname="1"><b>Reproducción</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> Se ha producido un error al descargar un fragmento o segmento (vídeo y audio). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> DESIRED_SEEK_POSITION  </span><span class="codeph"> DESIRED_SEEK_PERIOD  </span> </td> 
   <td colname="5"> Se ha producido un error al realizar una operación de búsqueda. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009  </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> Se ha producido un error al realizar una operación de pausa. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102  </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Se ha producido un error al recuperar información sobre un periodo de contenido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103  </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Se ha producido un error al intentar recuperar la posición de reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104  </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Error al intentar recuperar la información de QOS. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200  </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> Error al intentar descargar datos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Recurso no válido</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> RECURSO DE  </span><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Error al cargar un elemento de recurso. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_ ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span> </td> 
   <td colname="5"> Se ha producido un error al colocar un recurso en la línea de tiempo de reproducción. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Procesamiento de publicidad</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID  </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL  </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE  </span> </td> 
   <td colname="4"> Ninguna </td> 
   <td colname="5"> Ninguna </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_ INVALID  </span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> La resolución de la publicidad falló debido a un formato de metadatos de publicidad no válido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
   <td colname="5"> El complemento de publicidad no pudo resolver los anuncios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> PROPOSED_AD_BREAK</span> </td> 
   <td colname="5"> Fase de resolución de publicidad ha fallado. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_CODE  </span> <span class="codeph"> NATIVE_ERROR_NAME  </span> <span class="codeph"> DESCRIPCIÓN  </span> <span class="codeph"> DESCRIPCIÓN</span> <p><b>Detalles de DRM:</b> </p> <span class="codeph"> DRM_ERROR_</span> <span class="codeph"> STRINGNATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>La biblioteca AVE de bajo nivel ha generado un error. </p> <p>Consulte <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Detalles de las notificaciones NATIVE_ERROR</a> para obtener información sobre los valores de estas claves de metadatos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Se ha producido un error al crear una instancia de la biblioteca de nivel bajo de AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Se ha producido un error al lanzar la biblioteca de nivel bajo de AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_ RELEASE_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Se ha producido un error al liberar los recursos de GPU utilizados por la biblioteca AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Error al restablecer la biblioteca AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> Error al adjuntar una vista a la biblioteca AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Configuración</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107000  </span> </td> 
   <td colname="2"><span class="codeph"> SET_VOLUME_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> VOLUMEN DE DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Error al intentar establecer el nivel de volumen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107001  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> Se ha producido un error al intentar cambiar los parámetros de almacenamiento en búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> Se ha producido un error al intentar cambiar la visibilidad de las pistas CC. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> Error al intentar cambiar las opciones de estilo de las pistas CC. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107004  </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> Se ha producido un error al intentar cambiar los parámetros de control de ABR. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107005  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span><span class="codeph"> INITIAL_BUFFER_TIME  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> Se ha producido un error al intentar cambiar los parámetros de control de almacenamiento en búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Audio alternativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR  </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME  </span><span class="codeph"> AUDIO_TRACK_LANGUAGE  </span> </td> 
   <td colname="5"> Se ha producido un error relacionado con una pista de audio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Genéricas</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 19999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR</span> </td> 
   <td colname="3"> Ninguna </td> 
   <td colname="4"> Ninguna </td> 
   <td colname="5"> Marca un evento de error genérico. No es emitido por TVSDK. Esto solo es un marcador para el final del rango de códigos numéricos correspondientes a los eventos de error de TVSDK. </td> 
  </tr> 
 </tbody> 
</table>

