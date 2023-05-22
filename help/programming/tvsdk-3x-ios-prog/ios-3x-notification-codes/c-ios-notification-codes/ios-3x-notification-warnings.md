---
description: Esta tabla proporciona información detallada sobre las notificaciones de tipo WARN.
title: Códigos de notificación de ADVERTENCIA
exl-id: de922934-9775-463f-a28f-fc891d7a914b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 3%

---

# Códigos de notificación de ADVERTENCIA {#warning-notification-codes}

Esta tabla proporciona información detallada sobre las notificaciones de tipo WARN.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

La mayoría de las advertencias contienen metadatos relevantes como, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Código</b></th> 
   <th colname="2" class="entry"><b>Nombre</b></th> 
   <th colname="3" class="entry"><b>InnerNotification&gt;/b&gt;</th> 
   <th colname="4" class="entry"><b>Claves de metadatos</b></th> 
   <th colname="5" class="entry"><b>Comentarios</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Resolución de anuncios</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td colname="5"> <p></p> </td> 
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
   <td colname="1"><b>Específico de iOS</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>El anuncio no se insertó en la secuencia. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>El anuncio no contiene secuencias de solo audio </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>No se ha encontrado ningún flujo de publicidad coincidente para la velocidad de bits actual del contenido. </p> <p>  </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270005 </span> </td> 
   <td colname="2"><span class="codeph"> AVASSET_FAILED_TO_CREATE </span> </td> 
   <td colname="3"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="4"> <p>Ninguno </p> </td> 
   <td colname="5"> <p>Error al crear el recurso AVA. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270006 </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_ADVERTENCIA </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="5"> <p>Advertencia: Consulte la descripción de la advertencia de SiteCatalyst. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270007 </span> </td> 
   <td colname="2"><span class="codeph"> NETWORK_ERROR </span> </td> 
   <td colname="3"> <p>Ninguno </p> </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>Error al obtener datos de la red. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID y el origen (URL) se pueden recuperar mediante PTAdAsset en los metadatos de notificación con `AD_ASSET` clave.
>
>El [] especifica una clave opcional para la notificación.
