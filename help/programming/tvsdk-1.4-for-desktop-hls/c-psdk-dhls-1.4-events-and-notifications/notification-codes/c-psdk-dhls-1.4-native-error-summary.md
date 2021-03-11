---
title: Detalles de la notificación NATIVE_ERROR
description: Detalles de la notificación NATIVE_ERROR
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Detalles de la notificación NATIVE_ERROR {#details-for-the-native-error-notification}

Cuando TVSDK gestiona un error nativo, establece algunos o todos los valores de clave de metadatos siguientes.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nombre de clave de metadatos </th> 
   <th colname="col2" class="entry"> Valor de metadatos </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_CODE  </span> </td> 
   <td colname="col2"> 
    <pre>
      Código de error nativo del Flash Player. 
    </pre> Estos códigos representan lo siguiente: 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">Errores de DRM (códigos 3300 a 3367). Son los mismos que los códigos de error de Flash Player equivalentes. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">Errores de reproducción de vídeo (-1 a 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">Errores de criptografía (300 a 307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_CODE_MESSAGE  </span> </td> 
   <td colname="col2"> Una cadena que contiene el nombre del error; por ejemplo, <span class="codeph"> AAXS_InvalidVoucher </span> o <span class="codeph"> DECODER_FAILED </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_SUBERROR_CODE  </span> </td> 
   <td colname="col2"> Para los errores de DRM, también se devuelven códigos de suberror. Estos códigos corresponden al código de suberror <span class="codeph"> DRMErrorEvents </span> que devuelve el Flash Player. Cuando informe de errores a Adobe, incluya este valor numérico para obtener ayuda sobre la resolución de problemas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING  </span> </td> 
   <td colname="col2"> Para DRM, esta es su cadena de error personalizada de la implementación del servidor DRM, si la ha definido. Incluya esto también cuando informe de errores a Adobes. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="col2"> Descripción de cadena del error. Normalmente es la URL de los medios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_URL  </span> </td> 
   <td colname="col2"> URL del medio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_TYPE  </span> </td> 
   <td colname="col2"> Tipo de medio (HLS). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_ID  </span> </td> 
   <td colname="col2"> ID del medio. </td> 
  </tr> 
 </tbody> 
</table>

TVSDK recibe estos códigos de error y cadenas del motor de vídeo.

>[!IMPORTANT]
>
>Para obtener una lista completa de los códigos de error de cliente DRM de Adobe Primetime, consulte [DRM Client Error Message Reference](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).