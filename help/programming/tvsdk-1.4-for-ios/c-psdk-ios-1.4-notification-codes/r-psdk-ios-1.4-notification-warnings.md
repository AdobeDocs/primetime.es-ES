---
description: Esta tabla proporciona información detallada sobre las notificaciones de tipo WARN.
title: ADVERTENCIA de códigos de notificación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 4%

---


# WARNING notification codes{#warning-notification-codes}

Esta tabla proporciona información detallada sobre las notificaciones de tipo WARN.

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
   <td colname="1"><b>Resolución de anuncios</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>Se ha producido un error al intentar cargar un creativo de publicidad. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR, AD_ID,DESCRIPCIÓN</span> </td> 
   <td colname="5"> <p>La resolución de la publicidad falló debido a una dirección URL VAST no válida o porque no se devolvió ningún anuncio del envoltorio VAST. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifiestos de fondo</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000  </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING</span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_</span> <span class="codeph"> ERRORBACKGROUND_MANIFEST_ WARNING_</span> <span class="codeph"> NAMEDESCRIPTION</span> </td> 
   <td colname="5"> <p> Error en la descarga del manifiesto en segundo plano. Cualquier problema en la actualización del manifiesto de fondo se envía como advertencia de TVSDK y no provoca que se detenga la reproducción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_ WARNING</span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
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
   <td colname="1"><span class="codeph"> 210000  </span> </td> 
   <td colname="2"><span class="codeph"> UNDEFINED_ TIME_RANGES  </span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"> Ninguna </td> 
   <td colname="5"> El modo de señalización de anuncio se define como rangos personalizados, pero no hay ningún rango definido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_RANGES  </span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> <p> Uno o más intervalos de tiempo no son válidos y se ignorarán o modificarán. </p> <p> DESCRIPCIÓN es una cadena que contiene una descripción de los intervalos no válidos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Específico de iOS</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_NOT_READY  </span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"> <p>Ninguna </p> </td> 
   <td colname="5"> <p>No se insertó el AD en la emisión. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002  </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING  </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="4"> <p>Ninguna </p> </td> 
   <td colname="5"> <p>El anuncio no contiene flujo de solo audio </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING  </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="4"> <p>Ninguna </p> </td> 
   <td colname="5"> <p>No se ha encontrado ningún flujo de anuncios coincidente para la velocidad de bits actual del contenido. </p> <p>  </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270005  </span> </td> 
   <td colname="2"><span class="codeph"> AVASSET_FAILED_TO_CREATE  </span> </td> 
   <td colname="3"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="4"> <p>Ninguna </p> </td> 
   <td colname="5"> <p>Error al crear el AVAset. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270006  </span> </td> 
   <td colname="2"><span class="codeph"> SiteCatalyst_WARNING  </span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="5"> <p>Advertencia: Consulte la descripción de la advertencia de sitecatalyst. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270007  </span> </td> 
   <td colname="2"><span class="codeph"> NETWORK_ERROR  </span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> <p>Error al obtener datos de la red. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002</span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING</span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>El audio de este anuncio no se puede escuchar porque falta </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003</span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING</span> </td> 
   <td colname="3"> <p>Ninguna </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>Falta la velocidad de bits coincidente. </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID y el origen (URL) se pueden recuperar mediante PTAdAsset en los metadatos de notificación con la clave `AD_ASSET`.
