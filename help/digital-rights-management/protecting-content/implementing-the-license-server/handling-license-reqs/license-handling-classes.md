---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Información general {#overview}

Para obtener una licencia, los clientes forman una solicitud a partir de los metadatos incrustados en el contenido empaquetado y luego la envían al servidor de licencias. El servidor de licencias utiliza información extraída de los metadatos de contenido para generar una licencia.

Si el cliente y el servidor admiten la versión 5 del protocolo, la URL de solicitud es &quot;URL del servidor de licencias en los metadatos&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Si la versión de protocolo 3 es la máxima admitida por el cliente o el servidor, los clientes de DRM de Primetime envían solicitudes de autenticación a &quot;URL del servidor de licencias en los metadatos&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en los metadatos&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Un dispositivo puede tener varias licencias para el mismo contenido (el mismo ID de licencia), pero solo puede tener una licencia para un ID de licencia en particular y un ID de política de DRM. Si recibe una licencia con un ID de licencia/ID de política duplicado, la nueva licencia reemplazará a la anterior solo si la fecha de emisión de la nueva licencia es posterior a la fecha de emisión de la licencia existente. Esta lógica se utiliza para procesar licencias incrustadas en el contenido. Por lo tanto, no se recomienda incrustar más de una licencia con el mismo ID de política de DRM en un fragmento de contenido. La misma lógica se aplica a las licencias que se pasan al cliente a través de `DRMManager.storeVoucher()` API de ActionScript 3; si el cliente ya posee una licencia con una fecha de emisión posterior, la licencia proporcionada puede ignorarse.

## Clases de administración de solicitudes de licencia {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` : es la clase de controlador de solicitud de licencia. Lee y analiza solicitudes de licencia. Su `getRequests()` El método devuelve una lista de `LicenseRequestMessage` objetos.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` : esta es la clase de mensaje de solicitud. El autor de la llamada debe iterar a través de `LicenseRequestMessage` lista devuelta por `getRequests()`y para cada solicitud, genere una licencia o establezca un código de error. Llamada `LicenseRequestMessage.getContentInfo()` para obtener información extraída de los metadatos de contenido, incluido el ID de contenido, el ID de licencia y las políticas de DRM.

Las licencias y los errores se envían al mismo tiempo cuando la variable `LicenseHandler.close()` método se llama.

Consulte la [Documentación de referencia de la API del servidor DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) para obtener más información.
