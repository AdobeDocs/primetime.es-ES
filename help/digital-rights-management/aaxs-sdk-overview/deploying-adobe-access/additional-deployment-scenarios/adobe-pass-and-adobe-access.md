---
seo-title: Adobe Pass y Adobe Access
title: Adobe Pass y Adobe Access
uuid: 09e75cd7-00b3-4f0f-869e-43dc4d5c3bf7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Adobe Pass y Adobe Access {#adobe-pass-and-adobe-access}

Adobe Pass ( [](https://www.adobe.com/products/adobepass/)) proporciona autenticación y autorización de usuarios y dispositivos en varios proveedores de contenido. El usuario debe tener una suscripción válida a TV por cable o por satélite.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass se puede utilizar junto con Adobe Access para proteger el contenido multimedia. En este escenario, el reproductor de vídeo (SWF) puede cargar otro SWF denominado *Access Enabler*, alojado por Adobe Systems. El *Access Enabler* se utiliza para conectarse al servicio Adobe Pass y facilitar la integración de SAML SSO con los sistemas de proveedores de identidad de MVPD (Distribuidor de programación de vídeo multicanal). Esto implica redirigir brevemente el explorador del usuario a la página de inicio de sesión de MVPD, luego mantener un autentificador AuthN y finalmente volver al sitio web de contenido con una sesión de AuthN en caché.

A continuación, *Access Enabler* puede facilitar las autorizaciones back-end entre el servicio Adobe Pass y el MVPD. El MVPD mantiene la lógica empresarial y determina a qué contenido tiene derecho el usuario. La asignación de derechos persiste en un autentificador AuthZ adicional para ese recurso de contenido y se devuelve al cliente.

Los autentificadores y los autentificadores de autorización se firman con el ID exclusivo y la clave privada del cliente de Adobe Access para evitar alteraciones o falsificaciones. Solo se puede acceder a este token a través de *Access Enabler*.

El reproductor de vídeo puede activar el proceso llamando `getAuthorization` al activador de *Access*. Cuando hay tokens AuthN/AuthZ válidos, *AccessEnabler* envía una llamada de retorno al reproductor de vídeo que incluirá un token de medios de corta duración para reproducir el contenido del vídeo.

Adobe Pass proporciona un validador de tokens de medios o una biblioteca Java que se puede implementar en un servidor. Al utilizar el servidor de Flash Access para la protección de contenido, puede integrar el validador de autentificadores de medios con un complemento del servidor de Adobe Access para emitir automáticamente una licencia genérica después de validar correctamente el autentificador de medios. A continuación, el contenido se transmite desde los servidores CDN al cliente. Para adquirir una licencia de contenido, el token de medios de corta duración se puede enviar al servidor de Adobe Access, donde se verifica la validez del token y se puede emitir una licencia.

El *Access Enabler* utiliza generalmente el autentificador AuthN de larga duración en todos los desarrolladores de contenido para representar el AuthN para ese suscriptor MVPD. Además, el servidor de Adobe Access y el verificador de autentificadores de autentificadores pueden ser gestionados por el CDN o un proveedor de servicios en nombre del proveedor de contenido.
