---
description: La configuración de directivas es el proceso de especificar condiciones sobre cuándo y cómo se permite a un usuario reproducir contenido de vídeo protegido.
title: Estableciendo directivas
exl-id: ab7295c8-88f2-4d4a-a7f1-3332df7bb735
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Estableciendo directivas{#setting-policies}

La configuración de directivas es el proceso de especificar condiciones sobre cuándo y cómo se permite a un usuario reproducir contenido de vídeo protegido.

La creación de directivas se produce como parte de la solicitud de token de licencia. (Consulte [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) por ejemplo, con Widevine).

Una vez que el código del lado del servidor de un cliente ha determinado que emitirá una licencia (basada en las comprobaciones de autorizaciones, la geolocalización o cualquier otra información necesaria), solicita un token y *en el token* especifica el requerido `securityLevel`, `hdcpOutputControl`, y `licenseDuration`. Estas son las opciones del lado del cliente para una política de Widevine. Otras soluciones de DRM ofrecen enfoques similares, pero los detalles son diferentes en cada caso y se explican en los flujos de trabajo individuales.

>[!NOTE]
>
>Adobe proporciona un servidor de referencia de ejemplo que muestra cómo implementar su propio servidor de derechos/tienda: [Servidor de referencia: Servidor de derechos de ExpressPlay de muestra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
