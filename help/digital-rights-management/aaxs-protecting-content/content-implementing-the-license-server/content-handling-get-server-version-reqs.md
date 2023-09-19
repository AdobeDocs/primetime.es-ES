---
title: Administrar solicitudes de obtención de versión del servidor
description: Administrar solicitudes de obtención de versión del servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Administrar solicitudes de obtención de versión del servidor{#handling-get-server-version-requests}

El cliente de acceso a Adobe 3.0 y versiones posteriores envían una solicitud de obtención de versión del servidor para determinar las capacidades del servidor. Todos los servidores que utilicen el SDK 3.0 de acceso a Adobe y versiones posteriores deben implementar la compatibilidad con las solicitudes Obtener versión del servidor.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* La URL de solicitud debe ser &quot;URL del servidor de licencias en los metadatos&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Para el SDK 4.0 de acceso a Adobe y versiones posteriores, la respuesta a una solicitud de obtención de versión del servidor indica a los clientes que el servidor admite las versiones 3 y 4 del protocolo de acceso a Adobe.
