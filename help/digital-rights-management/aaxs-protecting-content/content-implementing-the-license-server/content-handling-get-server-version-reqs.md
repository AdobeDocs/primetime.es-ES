---
title: Gestión de solicitudes Get Server Version
description: Gestión de solicitudes Get Server Version
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Gestión de solicitudes Get Server Version{#handling-get-server-version-requests}

El cliente de acceso a Adobe 3.0 y versiones posteriores envían una solicitud de Obtención de versión del servidor para determinar las funcionalidades del servidor. Todos los servidores que utilicen el SDK 3.0 de acceso a Adobe y versiones posteriores deben implementar la compatibilidad con las solicitudes Get Server Version.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* La dirección URL de solicitud debe ser &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Para el SDK de acceso a Adobe 4.0 y posteriores, la respuesta a una solicitud de Obtención de versión del servidor indica a los clientes que el servidor admite las versiones 3 y 4 del protocolo de acceso a Adobe.
