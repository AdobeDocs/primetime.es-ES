---
description: Esta tabla muestra información detallada sobre WARN. escriba notificaciones.
seo-description: Esta tabla muestra información detallada sobre WARN. escriba notificaciones.
seo-title: Códigos de notificación de ADVERTENCIA
title: Códigos de notificación de ADVERTENCIA
uuid: 1ce5be07-f5bf-443c-b907-9768633e1300
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Códigos de notificación de ADVERTENCIA{#warning-notification-codes}

Esta tabla muestra información detallada sobre WARN. escriba notificaciones.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

La mayoría de las advertencias contienen metadatos relevantes, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

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
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FALIL </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"> <p>Se ha producido un error en una operación relacionada con la reproducción, pero es posible que la reproducción continúe. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Resolución de publicidad </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_ NO SE PUBLICÓ </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID </span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>La resolución de publicidad no pudo resolver/insertar el contenido de la publicidad. La reproducción puede continuar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifiestos de antecedentes</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ ADVERTENCIA</span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_NAME</span><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="5"> <p> Error en la descarga del manifiesto en segundo plano. Cualquier problema relacionado con la actualización del manifiesto de fondo se envía como una advertencia TVSDK y no provoca que la reproducción se detenga. </p> </td> 
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
   <td colname="4"><b>AVE</b> <p><span class="codeph"> DESCRIPCIÓN DE NATIVE_ERROR_CODE </span><span class="codeph"> NATIVE_ERROR_NAME </span><span class="codeph"></span> </p> </td> 
   <td colname="5"> <p>La biblioteca AVE de bajo nivel ha generado un error. </p> <p>Consulte <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Detalles de las notificaciones</a> NATIVE_ERROR para obtener información detallada sobre los valores de estos campos de metadatos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">Código de error secundario DRM y cadena de error del servidor DRM. Consulte <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Detalles de las notificaciones</a> NATIVE_ERROR para obtener información detallada sobre los valores de estos campos de metadatos.
   </td> 
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
   <td colname="5"> <p>Marca un evento de advertencia genérico. En realidad no es emitido por TVSDK. Es sólo un marcador para el final del rango de códigos numéricos correspondientes a eventos de advertencia. </p> </td> 
  </tr> 
 </tbody> 
</table>

