---
title: Administrar solicitudes de obtención de versión del servidor
description: Administrar solicitudes de obtención de versión del servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Administrar solicitudes de obtención de versión del servidor {#handle-get-server-version-requests}

El cliente DRM de Adobe Primetime 3.0 o posterior envía una solicitud de obtención de versión del servidor para determinar las capacidades del servidor. Todos los servidores que utilicen Primetime DRM SDK 3.0 o posterior deben implementar la compatibilidad con las solicitudes Obtener versión del servidor.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* La URL de solicitud debe ser &quot;URL del servidor de licencias en los metadatos&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Para el SDK 4.0 de Primetime DRM o posterior, la respuesta a una solicitud de Obtener versión del servidor indica a los clientes que el servidor admite las versiones 3 y 4 del protocolo DRM de Primetime.
