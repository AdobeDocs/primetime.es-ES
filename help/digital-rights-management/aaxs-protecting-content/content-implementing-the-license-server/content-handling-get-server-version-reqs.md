---
seo-title: Gestión de solicitudes Get Server Version
title: Gestión de solicitudes Get Server Version
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestión de solicitudes Get Server Version{#handling-get-server-version-requests}

El cliente de Adobe Access 3.0 y versiones posteriores envían una solicitud de Get Server Version para determinar las capacidades del servidor. Todos los servidores que utilizan el SDK 3.0 de Adobe Access y versiones posteriores deben implementar la compatibilidad con las solicitudes Get Server Version.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* La dirección URL de la solicitud debe ser &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Para el SDK 4.0 de Adobe Access y versiones posteriores, la respuesta a una solicitud de Get Server Version indica a los clientes que el servidor admite las versiones 3 y 4 del protocolo Adobe Access.
