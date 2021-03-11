---
title: Acceso a Adobe Pass y Adobe
description: Acceso a Adobe Pass y Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Acceso a Adobe Pass y Adobe {#adobe-pass-and-adobe-access}

Adobe Pass ( [](https://www.adobe.com/products/adobepass/)) proporciona autenticación y autorización de usuarios/dispositivos en varios proveedores de contenido. El usuario debe tener una suscripción válida a TV por cable o por satélite.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass se puede utilizar junto con Acceso a Adobe para proteger el contenido multimedia. En esta situación, el reproductor de vídeo (SWF) puede cargar otro SWF denominado *Access Enabler*, que está alojado por Adobe Systems. El *Access Enabler* se utiliza para conectarse al servicio de Adobe Pass y facilitar la integración de SAML SSO con los sistemas proveedores de identidad de MVPD (Distribuidor de Programación de Vídeo Multicanal). Esto implica redirigir brevemente el navegador del usuario a la página de inicio de sesión de MVPD, luego mantener un token AuthN y finalmente volver al sitio web de contenido con una sesión de AuthN en caché.

El *Access Enabler* puede facilitar las autorizaciones back-end entre el servicio de Adobe Pass y el MVPD. El MVPD mantiene la lógica empresarial y determina a qué contenido tiene derecho el usuario. La asignación de derechos se mantiene en un token AuthZ adicional para ese recurso de contenido y se devuelve al cliente.

Los tokens de autenticación y autorización se firman con el ID exclusivo y la clave privada del cliente de acceso de Adobe para evitar la manipulación o la suplantación. Solo se puede acceder a este token a través de *Access Enabler*.

El reproductor de vídeo puede almacenar en déclencheur el proceso llamando a `getAuthorization` en el *Activador de acceso*. Cuando hay tokens válidos de AuthN/AuthZ, *AccessEnabler* envía una llamada de retorno al reproductor de vídeo que incluirá un token multimedia de corta duración para reproducir el contenido de vídeo.

Adobe Pass proporciona una biblioteca Java del validador de tokens de medios que se puede implementar en un servidor. Al utilizar el servidor de acceso de Adobe para la protección de contenido, puede integrar el validador de tokens de medios con un complemento del lado del servidor de acceso de medios para emitir automáticamente una licencia genérica después de validar correctamente el token de medios. A continuación, el contenido se transmite desde los servidores de CDN al cliente. Para adquirir una licencia de contenido, el token de contenido de corta duración se puede enviar al servidor de acceso a Adobe, donde se verifica la validez del token y se puede emitir una licencia.

El token de AuthN de larga duración lo utiliza generalmente *Access Enabler* en todos los desarrolladores de contenido para representar el AuthN para ese suscriptor de MVPD. Además, Adobe Access Server y el verificador de tokens pueden ser operados por la CDN o un proveedor de servicios en nombre del proveedor de contenido.
