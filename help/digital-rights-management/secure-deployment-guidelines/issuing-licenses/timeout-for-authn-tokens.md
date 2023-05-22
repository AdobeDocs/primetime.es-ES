---
description: Todos los tokens de autenticación generados por el SDK de DRM de Adobe Primetime tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.
title: Tiempo de espera para tokens de autenticación
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Tiempo de espera para tokens de autenticación{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de DRM de Adobe Primetime tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.

La caducidad del token de autenticación se especifica al utilizar el SDK de DRM de Primetime al gestionar una solicitud de autenticación. Una vez caducado, el token deja de ser válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
