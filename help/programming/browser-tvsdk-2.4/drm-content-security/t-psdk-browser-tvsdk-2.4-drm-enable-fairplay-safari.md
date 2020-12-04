---
description: Puede activar FairPlay para Safari cuando trabaje con Primetime DRM Cloud, con tecnología ExpressPlay.
seo-description: Puede activar FairPlay para Safari cuando trabaje con Primetime DRM Cloud, con tecnología ExpressPlay.
seo-title: Habilitar FairPlay para Safari HLS
title: Habilitar FairPlay para Safari HLS
uuid: 6a250a31-cc4b-4c4b-b1e9-893ee3ca5d78
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Habilitar FairPlay para Safari HLS {#enable-fairplay-for-safari-hls}

Puede activar FairPlay para Safari cuando trabaje con Primetime DRM Cloud, con tecnología ExpressPlay.

Asegúrese de que dispone de lo siguiente:

* Una aplicación de muestra que funciona y que puede reproducir vídeo HLS.

   La aplicación de ejemplo debe poder reproducir contenido protegido con FairPlay con las licencias gestionadas mediante Primetime DRM con ExpressPlay.
* Contenido HLS de muestra (manifiesto M3U8) empaquetado con protección FairPlay.

Para aprovechar al máximo la información aquí, conozca los Flujos de trabajo de Multi-DRM comenzando con la subsección [Servidor de referencia: Ejemplo de ExpressPlay Entitlement Server (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) en la guía de Flujos de trabajo de varios DRM. Lea primero la documentación sobre cómo configurar la asignación de derechos y el servidor clave, y la información siguiente será mucho más útil.
Necesita los siguientes elementos:

* Su *producción* autenticador del cliente de ExpressPlay
* La misma clave de contenido y `iv` con la que se empaquetó el contenido.
* Ubicación del certificado de clave pública de FairPlay.

Para modificar la aplicación FairPlay/Safari:

1. Establezca la ubicación del certificado de clave pública de FairPlay que se utilizó en la solicitud del servidor de licencias de FairPlay.

   Por ejemplo:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Realice una solicitud manual de licencia de FairPlay *token* a ExpressPlay para obtener una URL de token de licencia.

       Puede completar este paso de una de las siguientes maneras:
   
   * Utilice su propio autenticador de cliente de producción ExpressPlay.
   * Utilice la misma clave de contenido y `iv` en esta solicitud que se utilizó para empaquetar el contenido que desee reproducir.

      Ejecute el siguiente comando desde el shell y sustituya el autenticador del cliente de ExpressPlay para obtener la URL del token de licencia para el contenido de muestra:

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

1. Configure una variable con la URL del token de licencia de ExpressPlay.

   Por ejemplo:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Antes de que la aplicación pueda reproducir contenido protegido, cambie el esquema de URL del contenido de `skd://` a `https://`.

   Debe agregar este cambio de esquema de URL en la aplicación antes de la llamada al servidor de licencias que permite la reproducción.

   Es necesario cambiar los protocolos porque el ID de contenido, que proporciona acceso a la clave de contenido en el sistema de administración de claves, está empaquetado en el manifiesto M3U8 con el protocolo `skd://`. Cuando el reproductor está listo para obtener la licencia para reproducir el contenido protegido, primero debe cambiar de protocolo para comunicarse con el servidor de licencias ExpressPlay. En el ejemplo siguiente, se modifica `myServerProcessSPCPath` para que contenga el esquema de URL correcto para la solicitud del servidor de licencias:

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

