---
title: Intercambiar un token SSO de Platform por un token de Adobe
description: Intercambiar un token SSO de Platform por un token de Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---


# Intercambiar un token SSO de Platform por un token de Adobe {#exchange-a-platform-sso-token-for-an-adobe-token}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Puntos finales de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descripción {#description}

Permite &quot;intercambiar&quot; un perfil SSO de Platform por un token de Adobe.

| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. solicitante (obligatorio)</br>    </br>2.  deviceId (obligatorio)</br>    </br>3.  mvpd (obligatorio)</br>    </br>4.  deviceType (obligatorio)</br>    </br>5.  SAMLResponse (obligatorio)</br>    </br>6.  deviceUser (desaprobada)</br>    </br>7.  appId (obsoleto) | POST | La respuesta correcta será 204 Sin contenido, indicando que el token se creó correctamente y está listo para utilizarse para los flujos de autenticación. | 204 - Sin contenido   </br>400 - Solicitud incorrecta |


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| mvpd | El Id. de MVPD para el que es válida esta operación. |
| deviceType | Plataforma de Apple para la que intentamos obtener una solicitud de perfil.  Cualquiera **iOS** o **tvOS**. |
| SAMLResponse | Perfil real devuelto por Platform SSO. |
| _deviceUser_ | El identificador de usuario del dispositivo. |
| _appId_ | El id/nombre de la aplicación. |


