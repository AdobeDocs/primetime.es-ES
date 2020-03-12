---
seo-title: Autenticación Adobe Primetime y Adobe Primetime DRM
title: Autenticación Adobe Primetime y Adobe Primetime DRM
uuid: 44fe3956-efb5-4fc5-97e2-37abb6554322
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Autenticación Adobe Primetime y Adobe Primetime DRM {#adobe-primetime-authentication-and-adobe-primetime-drm}

La autenticación Adobe Primetime ( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/)) proporciona autenticación y autorización de usuario/dispositivo en varios proveedores de contenido. El usuario debe tener una suscripción válida a TV por cable o por satélite.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

La autenticación Adobe Primetime se puede utilizar junto con Adobe Primeitme DRM para proteger el contenido multimedia. En este escenario, el reproductor de vídeo (SWF) puede cargar otro SWF denominado *Access Enabler*, alojado por Adobe Systems. El *Access Enabler* se utiliza para conectarse al servicio de autenticación Adobe Primetime y facilitar la integración de SAML SSO con los sistemas de proveedores de identidad de MVPD (Distribuidor de programación de vídeo multicanal). Esto implica redirigir brevemente el explorador del usuario a la página de inicio de sesión de MVPD, luego mantener un autentificador AuthN y finalmente volver al sitio web de contenido con una sesión de AuthN en caché.

A continuación, *Access Enabler* puede facilitar las autorizaciones back-end entre el servicio de autenticación Adobe Primetime y el MVPD. El MVPD mantiene la lógica empresarial y determina a qué contenido tiene derecho el usuario. La asignación de derechos persiste en un autentificador AuthZ adicional para ese recurso de contenido y se devuelve al cliente.

Los tokens de autenticación y autorización se firman con el ID exclusivo y la clave privada del cliente DRM de Primetime para evitar la manipulación o la falsificación. Solo se puede acceder a este token a través de *Access Enabler*.

El reproductor de vídeo puede activar el proceso llamando `getAuthorization` al activador de *Access*. Cuando hay tokens AuthN/AuthZ válidos, *AccessEnabler* envía una llamada de retorno al reproductor de vídeo que incluirá un token de medios de corta duración para reproducir el contenido del vídeo.

La autenticación Adobe Primetime proporciona un validador de tokens de medios o una biblioteca Java que se puede implementar en un servidor. Al utilizar el servidor Primetime DRM para la protección de contenido, puede integrar el validador de autentificadores de medios con un complemento Primetime DRM del lado del servidor para emitir automáticamente una licencia genérica después de validar correctamente el autentificador de medios. A continuación, el contenido se transmite desde los servidores CDN al cliente. Para adquirir una licencia de contenido, el token de medios de corta duración se puede enviar al servidor Primetime DRM, donde se verifica la validez del token y se puede emitir una licencia.

El *Access Enabler* utiliza generalmente el autentificador AuthN de larga duración en todos los desarrolladores de contenido para representar el AuthN para ese suscriptor MVPD. Además, el servidor Primetime DRM y el verificador de autentificadores pueden ser operados por el CDN o un proveedor de servicios en nombre del proveedor de contenido.