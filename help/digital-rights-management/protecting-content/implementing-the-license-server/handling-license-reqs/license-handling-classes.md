---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Información general {#overview}

Para obtener una licencia, los clientes solicitan los metadatos incrustados en el contenido empaquetado y luego envían la solicitud al servidor de licencias. El servidor de licencias utiliza información extraída de los metadatos de contenido para generar una licencia.

Si el cliente y el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Si la versión de protocolo 3 es la máxima admitida por el cliente o el servidor, los clientes de DRM de Primetime envían las solicitudes de autenticación a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Un dispositivo puede tener varias licencias para el mismo contenido (el mismo ID de licencia), pero solo puede tener una licencia para un ID de licencia y un ID de política de DRM en particular. Si recibe una licencia con un ID de licencia/ID de política duplicado, la nueva licencia reemplazará a la antigua solo si la fecha de emisión de la nueva licencia es posterior a la fecha de emisión de la licencia existente. Esta lógica se utiliza para procesar las licencias incrustadas en el contenido. Por lo tanto, no se recomienda incrustar más de una licencia con el mismo ID de directiva DRM en un fragmento de contenido. La misma lógica se aplica a las licencias pasadas al cliente a través de la API `DRMManager.storeVoucher()` ActionScript3; si el cliente ya posee una licencia con una fecha de emisión posterior, se puede ignorar la licencia proporcionada.

## Clases de administración de solicitudes de licencia {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Esta es la clase del controlador de solicitud de licencia. Lee y analiza las solicitudes de licencia. Su método `getRequests()` devuelve una lista de objetos `LicenseRequestMessage`.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Esta es la clase de mensaje de solicitud. El llamador debe iterar a través de la lista `LicenseRequestMessage` devuelta por `getRequests()` y, para cada solicitud, generar una licencia o establecer un código de error. Llame a `LicenseRequestMessage.getContentInfo()` para obtener información extraída de los metadatos de contenido, incluido el ID de contenido, el ID de licencia y las políticas de DRM.

Las licencias y los errores se envían al mismo tiempo en que se llama al método `LicenseHandler.close()` .

Consulte la [documentación de referencia de la API del servidor DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) para obtener más información.
