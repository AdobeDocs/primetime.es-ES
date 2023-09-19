---
title: Detalles de la notificación NATIVE_ERROR
description: Detalles de la notificación NATIVE_ERROR
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Detalles de la notificación NATIVE_ERROR {#details-for-the-native-error-notification}

Cuando TVSDK administra un error nativo, establece algunos o todos los valores de clave de metadatos siguientes.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nombre de clave de metadatos </th> 
   <th colname="col2" class="entry"> Valor de metadatos </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="col2"> 
    <pre>
      Código de error nativo del AVE. 
    </pre> Estos códigos representan lo siguiente: 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">Errores de DRM (códigos 3300 a 3367). Son los mismos que los códigos de error de Flash Player equivalentes. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">Errores de reproducción de vídeo (-1 a 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">Errores de criptografía (300 a 307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME </span> </td> 
   <td colname="col2"> Una cadena que contiene el nombre del error; por ejemplo, <span class="codeph"> Cupón AXS_Invalid </span> o <span class="codeph"> DECODER_FAILED </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE </span> </td> 
   <td colname="col2"> Para los errores de DRM, también se devuelven códigos de suberror. Estos códigos corresponden a la variable <span class="codeph"> DRMErrorEvents </span> código de suberror devuelto por el Flash Player. Cuando comunique errores al Adobe, incluya este valor numérico para obtener asistencia en la resolución de problemas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> Para DRM, esta es la cadena de error personalizada de la implementación del servidor DRM, si ha definido alguna. Incluya esto también al informar de errores al Adobe. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DESCRIPCIÓN </span> </td> 
   <td colname="col2"> Descripción en cadena del error. Normalmente, la dirección URL del contenido. </td> 
  </tr> 
 </tbody> 
</table>

TVSDK recibe estos códigos de error y cadenas del motor de vídeo.

>[!IMPORTANT]
>
>Para obtener una lista completa de los códigos de error del cliente DRM de Adobe Primetime, consulte [Referencia de mensaje de error del cliente DRM](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).
