---
title: Recuperar solicitud de perfil SSO de Platform
description: Recuperar solicitud de perfil SSO de Platform
exl-id: 44fd4e26-4d9a-4607-ac2c-b85d848f5fc6
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Recuperar solicitud de perfil SSO de Platform {#retrieve-platform-sso-profile-request}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Extremos de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descripción {#description}

Este recurso produce solicitudes de perfil para un ID de solicitante y una tupla MVPD.


| Extremo | Llamado  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor}/profile-requests/{mvpd} | Aplicación de streaming</br></br>o</br></br>Servicio de programador | 1. solicitante (parámetro de ruta)</br>2. mvpd (parámetro de ruta)</br>3. deviceType (obligatorio) | GET | El Content-Type de respuesta será application/octet-stream, ya que la carga útil real es opaca para la aplicación cliente.</br></br>La aplicación debe reenviar la respuesta a la Plataforma</br></br>Motor de SSO para obtener un SSO de perfil. | 200 - Éxito   </br>400: Solicitud incorrecta |


| Parámetro de entrada | Descripción |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| solicitante | Identificador de solicitante del programador para el que es válida esta operación. |
| mvpd | Id de MVPD para el que es válida esta operación. |
| deviceType | La plataforma de Apple para la que intentamos obtener una solicitud de perfil.  Cualquiera **iOS** o **tvOS**. |
