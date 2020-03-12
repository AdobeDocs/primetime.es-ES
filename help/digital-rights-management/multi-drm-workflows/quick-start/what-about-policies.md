---
description: La configuración de políticas es el proceso de especificar las condiciones para cuándo y cómo se permite al usuario reproducir contenido de vídeo protegido.
seo-description: La configuración de políticas es el proceso de especificar las condiciones para cuándo y cómo se permite al usuario reproducir contenido de vídeo protegido.
seo-title: Configuración de políticas
title: Configuración de políticas
uuid: 2d2672ce-5ed4-4868-aa5e-0a9e21a809b3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configuración de políticas{#setting-policies}

La configuración de políticas es el proceso de especificar las condiciones para cuándo y cómo se permite al usuario reproducir contenido de vídeo protegido.

La creación de directivas se produce como parte de la solicitud de token de licencia. (Consulte [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) para ver un ejemplo de uso de Widevine).

Una vez que el código de servidor de un cliente ha determinado que emitirá una licencia (basada en comprobaciones de derechos, geolocalización o cualquier otra información necesaria), solicita un token y, *en el token* , especifica los requisitos `securityLevel`, `hdcpOutputControl`y `licenseDuration`. Estas son las opciones del lado del cliente para una política Widevine. Otras soluciones DRM ofrecen enfoques similares, pero los detalles son diferentes en cada caso y se explican en los flujos de trabajo individuales.

>[!NOTE]
>
>Adobe proporciona un servidor de referencia de muestra que muestra cómo implementar su propio servidor o tienda de asignación de derechos: Servidor [de referencia: Servidor de asignación de derechos ExpressPlay de muestra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

