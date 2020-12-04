---
description: Todos los tokens de autenticación generados por el SDK de Adobe Primetime DRM tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.
seo-description: Todos los tokens de autenticación generados por el SDK de Adobe Primetime DRM tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.
seo-title: Tiempo de espera para los tokens de autenticación
title: Tiempo de espera para los tokens de autenticación
uuid: 2c2b0dad-0979-4d49-b109-2700ceb4d722
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Tiempo de espera para autentificadores{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de Adobe Primetime DRM tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.

La caducidad del autentificador se especifica mediante el uso del SDK de Primetime DRM al gestionar una solicitud de autenticación. Una vez caducado, el token ya no es válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
