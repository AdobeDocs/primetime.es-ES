---
title: Recuperar solicitud de perfil SSO de Platform
description: Recuperar solicitud de perfil SSO de Platform
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Recuperar solicitud de perfil SSO de Platform {#retrieve-platform-sso-profile-request}

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

Este recurso genera solicitudes de perfil para un ID de solicitante y un tuple MVPD.


| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor}/profile-request/{mvpd} | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. solicitante (parámetro de ruta)</br>2. mvpd (parámetro de ruta)</br>3. deviceType (obligatorio) | GET | La respuesta Content-Type será application/octet-stream, ya que la carga útil real es opaca para la aplicación cliente.</br></br>La aplicación debe reenviar la respuesta a la Plataforma</br></br>Motor SSO para obtener un SSO de perfil. | 200 - Éxito   </br>400 - Solicitud incorrecta |


| Parámetro de entrada | Descripción |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| mvpd | El Id. de MVPD para el que es válida esta operación. |
| deviceType | Plataforma de Apple para la que intentamos obtener una solicitud de perfil.  Cualquiera **iOS** o **tvOS**. |


