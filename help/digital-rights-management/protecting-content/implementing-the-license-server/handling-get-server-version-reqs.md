---
title: Gestionar las solicitudes Get Server Version
description: Gestionar las solicitudes Get Server Version
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Gestionar peticiones de versión del servidor de obtención {#handle-get-server-version-requests}

El cliente Adobe Primetime DRM 3.0 o posterior envía una solicitud Get Server Version para determinar las capacidades del servidor. Todos los servidores que utilizan Primetime DRM SDK 3.0 o posterior deben implementar la compatibilidad con las solicitudes Get Server Version.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* La dirección URL de solicitud debe ser &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Para Primetime DRM SDK 4.0 o posterior, la respuesta a una solicitud Get Server Version indica a los clientes que el servidor admite las versiones 3 y 4 del protocolo Primetime DRM.
