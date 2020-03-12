---
seo-title: Administrar solicitudes de Obtención de versión del servidor
title: Administrar solicitudes de Obtención de versión del servidor
uuid: 6e287f58-2ad2-428a-a76a-6847d06b0fd8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Administrar solicitudes de Obtención de versión del servidor {#handle-get-server-version-requests}

El cliente DRM de Adobe Primetime 3.0 o posterior envía una solicitud Get Server Version para determinar las capacidades del servidor. Todos los servidores que utilizan Primetime DRM SDK 3.0 o posterior deben implementar la compatibilidad con las solicitudes Get Server Version.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* La dirección URL de la solicitud debe ser &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Para Primetime DRM SDK 4.0 o posterior, la respuesta a una solicitud Get Server Version indica a los clientes que el servidor admite las versiones 3 y 4 del protocolo Primetime DRM.
