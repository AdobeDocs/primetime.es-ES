---
title: Administrar solicitudes de autenticación
description: Administrar solicitudes de autenticación
copied-description: true
exl-id: 64d23db0-254d-46b1-8317-ba0381509b44
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Administrar solicitudes de autenticación {#handle-authentication-requests}

El `AuthenticationHandler` se utiliza para procesar solicitudes de autenticación. Solo se utiliza para la autenticación de nombre de usuario y contraseña.

Al generar el token de autenticación, se debe especificar la fecha de caducidad del token. También se pueden incluir propiedades personalizadas en el token. Si se establece, el servidor podrá ver esas propiedades cuando se envíe el token de autenticación en solicitudes posteriores. Consulte [Administrar solicitudes de licencia](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) para obtener información sobre la administración de tokens de autenticación personalizados.

El controlador lee una solicitud de autenticación y analiza el mensaje de solicitud cuando `parseRequest()` se llama. La implementación del servidor examina las credenciales del usuario en la solicitud y, si las credenciales son válidas, genera un `AuthenticationToken` objeto llamando a `getRequest().generateAuthToken()`. If `AuthenticationRequestMessage.generateAuthToken()` no se llama antes de `close()`, se envía un código de error de error de autenticación.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de solicitud es &quot;URL del servidor de licencias en los metadatos: +&quot; [!DNL /flashaccess/authn/v4]&quot;. Si la versión 3 del protocolo es la máxima admitida por el cliente o el servidor, los clientes de Adobe Primetime DRM envían luego solicitudes de autenticación a &quot;URL del servidor de licencias en los metadatos&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en los metadatos&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;
