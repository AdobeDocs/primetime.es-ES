---
description: Esta tabla proporciona información detallada sobre las notificaciones de tipo WARN.
title: Códigos de notificación de ADVERTENCIA
exl-id: e787fad5-fbdc-416d-b03d-8c84f4884c5a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---

# Códigos de notificación de ADVERTENCIA {#warning-notification-codes}

Esta tabla proporciona información detallada sobre las notificaciones de tipo WARN.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

La mayoría de las advertencias contienen metadatos relevantes como, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
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
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> _FAIL DE OPERACIÓN_DE_REPRODUCCIÓN </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"> <p>Se ha producido un error en una operación relacionada con la reproducción, pero la reproducción puede continuar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Resolución de anuncios</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> ERROR DE RESOURCE_PLACEMENT_ </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID </span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>El solucionador de anuncios no ha podido resolver o insertar el contenido del anuncio. La reproducción puede continuar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>Se ha producido un error al intentar cargar un creativo de publicidad. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_ RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> ERROR_INTERNO, AD_ID,DESCRIPCIÓN</span> </td> 
   <td colname="5"> <p>Error en la resolución de anuncios debido a una URL de VAST no válida o porque no se devolvió ningún anuncio desde el contenedor de VAST. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifiestos de fondo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING</span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span> <span class="codeph"> BACKGROUND_MANIFEST_WARNING_NAME</span> <span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> <p> Error al descargar el manifiesto en segundo plano. Cualquier problema al actualizar el manifiesto en segundo plano se envía como advertencia de TVSDK y no hace que se detenga la reproducción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_ WARNING</span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING </span> </td> 
   <td colname="3" morerows="1"> <p>Ninguno </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> NATIVE_ERROR_NAME </span><span class="codeph"> DESCRIPCIÓN </span> </p> </td> 
   <td colname="5"> <p>La biblioteca AVE de bajo nivel ha emitido un error. </p> <p>Consulte <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Detalles de las notificaciones NATIVE_ERROR</a> para obtener información detallada sobre los valores de estos campos de metadatos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5"> Código de error menor DRM y cadena de error del servidor DRM. Consulte <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Detalles de las notificaciones NATIVE_ERROR</a> para obtener información detallada sobre los valores de estos campos de metadatos.</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000 </span> </td> 
   <td colname="2"><span class="codeph"> UNDEFINED_TIME_RANGES </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> Ninguno </td> 
   <td colname="5"> El modo de señalización de publicidad se define como intervalos personalizados, pero no hay ningún intervalo definido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_RANGES </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"> <p> Uno o más intervalos de tiempo no son válidos y se ignorarán o modificarán. </p> <p> DESCRIPTION es una cadena que contiene la descripción de los intervalos no válidos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Modo de truco</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 280000 </span> </td> 
   <td colname="2"><span class="codeph"> TRICKPLAY_RATE_ CHANGE_FAIL</span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> <p> Error de cambio de tarifa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Genérico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>Marca un evento de advertencia genérico. No emitido realmente por TVSDK. Solo es un marcador para el final del rango de códigos numéricos correspondientes a eventos de advertencia. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[¡NOTA!] adID y el origen (URL) se pueden recuperar mediante PTAdAsset en los metadatos de notificación con `AD_ASSET` clave.
