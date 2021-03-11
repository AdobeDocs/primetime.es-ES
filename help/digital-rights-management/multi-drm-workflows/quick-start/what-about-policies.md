---
description: La configuración de políticas es el proceso de especificar condiciones para cuándo y cómo se permite al usuario reproducir contenido de vídeo protegido.
title: Configuración de políticas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Configuración de directivas{#setting-policies}

La configuración de políticas es el proceso de especificar condiciones para cuándo y cómo se permite al usuario reproducir contenido de vídeo protegido.

La creación de directivas se produce como parte de la solicitud de token de licencia. (Consulte [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) para ver un ejemplo con Widevine).

Una vez que el código del lado del servidor de un cliente ha determinado que emitirá una licencia (en función de las comprobaciones de autorizaciones, la geolocalización o cualquier otra información necesaria), solicita un token y *en el token* especifica los `securityLevel`, `hdcpOutputControl` y `licenseDuration` requeridos. Estas son las opciones del lado del cliente para una directiva Widevine. Otras soluciones DRM ofrecen enfoques similares, pero los detalles son diferentes en cada caso y se detallan en los flujos de trabajo individuales.

>[!NOTE]
>
>Adobe proporciona un servidor de referencia de muestra que muestra cómo implementar su propio servidor de autorizaciones/tienda: [Servidor de referencia: Servidor de derechos ExpressPlay de muestra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

