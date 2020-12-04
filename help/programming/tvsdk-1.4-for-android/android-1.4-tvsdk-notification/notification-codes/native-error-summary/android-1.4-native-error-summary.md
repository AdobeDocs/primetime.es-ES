---
seo-title: Detalles de la notificación NATIVE_ERROR
title: Detalles de la notificación NATIVE_ERROR
uuid: 18c4da57-59de-41a8-a2ea-fef800565207
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Detalles de la notificación NATIVE_ERROR {#details-for-the-native-error-notification}

Cuando TVSDK gestiona un error nativo, establece algunos o todos los siguientes valores de clave de metadatos.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nombre de clave de metadatos </th> 
   <th colname="col2" class="entry"> Valor de metadatos </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
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
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME  </span> </td> 
   <td colname="col2"> Una cadena que contiene el nombre del error; por ejemplo, <span class="codeph"> AAXS_InvalidVoucher </span> o <span class="codeph"> DECODER_FAILED </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE  </span> </td> 
   <td colname="col2"> Para los errores de DRM, también se devuelven códigos de suberror. Estos códigos corresponden al código de suberror <span class="codeph"> DRMErrorEvents </span> que devuelve el Flash Player. Cuando se produzcan errores de sistema de informes en el Adobe, incluya este valor numérico para obtener ayuda en la resolución de problemas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING  </span> </td> 
   <td colname="col2"> Para DRM, esta es la cadena de error personalizada de la implementación del servidor DRM, si ha definido alguna. También incluya esto cuando se produzcan errores de sistema de informes en el Adobe. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DESCRIPCIÓN  </span> </td> 
   <td colname="col2"> Descripción de cadena del error. Normalmente, la dirección URL del medio. </td> 
  </tr> 
 </tbody> 
</table>

TVSDK recibe estos códigos de error y cadenas del motor de vídeo.

>[!IMPORTANT]
>
>Para obtener una lista completa de los códigos de error de cliente DRM de Adobe Primetime, consulte [Referencia de mensaje de error de cliente DRM](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).