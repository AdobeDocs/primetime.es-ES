---
description: Puede habilitar FairPlay para Safari cuando trabaje con Primetime DRM Cloud, con tecnología ExpressPlay.
title: Habilitar FairPlay para Safari HLS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Habilitar FairPlay para Safari HLS {#enable-fairplay-for-safari-hls}

Puede habilitar FairPlay para Safari cuando trabaje con Primetime DRM Cloud, con tecnología ExpressPlay.

Asegúrese de que dispone de lo siguiente:

* Una aplicación de ejemplo que funciona y que puede reproducir vídeo HLS.

   La aplicación de ejemplo debe ser capaz de reproducir contenido protegido por FairPlay con la licencia gestionada a través de Primetime DRM con tecnología ExpressPlay.
* Contenido HLS de muestra (manifiesto M3U8) empaquetado con protección FairPlay.

Para aprovechar al máximo la información aquí, obtenga información sobre los flujos de trabajo Multi-DRM que empiezan por la subsección [Servidor de referencia: Ejemplo de ExpressPlay Entitlement Server (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) en la guía Flujos de trabajo Multi-DRM. Primero lea esa documentación sobre cómo configurar su derecho y el servidor clave, y la siguiente información será mucho más útil.
Necesita los siguientes elementos:

* Su ** autenticador del cliente de ExpressPlay
* La misma clave de contenido y `iv` con los que se empaquetó el contenido.
* La ubicación del certificado de clave pública de FairPlay.

Para modificar la aplicación FairPlay/Safari:

1. Establezca la ubicación del certificado de clave pública de FairPlay que se utilizó en la solicitud del servidor de licencias de FairPlay.

   Por ejemplo:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Realice una solicitud manual de licencia de FairPlay *token* a ExpressPlay para obtener una URL de token de licencia.

       Puede completar este paso de una de las siguientes maneras:
   
   * Utilice su propio autenticador de cliente de producción de ExpressPlay.
   * Utilice la misma clave de contenido y `iv` en esta solicitud que se utilizó para empaquetar el contenido que desea reproducir.

      Ejecute el siguiente comando desde el shell y sustituya el autenticador de cliente de ExpressPlay para obtener la URL del token de licencia para el contenido de ejemplo:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      La respuesta con la URL del token de licencia tendrá este aspecto:

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. Establezca una variable con la URL del token de licencia de ExpressPlay.

   Por ejemplo:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Para que la aplicación pueda reproducir contenido protegido, cambie el esquema de URL del contenido de `skd://` a `https://`.

   Debe añadir este cambio en el esquema de URL en la aplicación antes de la llamada al servidor de licencias que permite la reproducción.

   Los protocolos deben cambiarse porque el ID de contenido, que proporciona acceso a la clave de contenido en el sistema de administración de claves, está empaquetado en el manifiesto M3U8 con el protocolo `skd://`. Cuando el reproductor está listo para obtener la licencia para reproducir el contenido protegido, primero debe cambiar de protocolo para comunicarse con el servidor de licencias ExpressPlay. En el ejemplo siguiente, el `myServerProcessSPCPath` se modifica para contener el esquema de URL correcto para la solicitud del servidor de licencias:

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```

