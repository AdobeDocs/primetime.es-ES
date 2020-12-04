---
seo-title: Información general
title: Información general
uuid: 2bbf0aa1-df35-429d-84df-db357fa53e47
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Información general {#overview}

Para obtener una licencia, los clientes solicitan los metadatos incrustados en el contenido empaquetado y luego envían esa solicitud al servidor de licencias. El servidor de licencias utiliza información extraída de los metadatos de contenido para generar una licencia.

Si tanto el cliente como el servidor admiten la versión 5 del protocolo, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Si la versión 3 del protocolo es la máxima admitida por el cliente o el servidor, los clientes de DRM de Primetime enviarán las solicitudes de autenticación a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Un dispositivo puede tener varias licencias para el mismo contenido (el mismo ID de licencia), pero solo puede tener una licencia para un ID de licencia y un ID de directiva de DRM concretos. Si recibe una licencia con un LicenseID/PolicyID de duplicado, la nueva licencia reemplazará a la anterior sólo si la fecha de emisión de la nueva licencia es posterior a la fecha de emisión de la licencia existente. Esta lógica se utiliza para procesar las licencias incrustadas en el contenido. Por lo tanto, no se recomienda incrustar más de una licencia con el mismo ID de directiva DRM en un fragmento de contenido. La misma lógica se aplica a las licencias pasadas al cliente a través de la API de `DRMManager.storeVoucher()` ActionScript3; si el cliente ya posee una licencia con una fecha de emisión posterior, la licencia proporcionada puede ignorarse.

## Clases de gestión de solicitudes de licencia {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Esta es la clase del controlador de solicitudes de licencia. Lee y analiza las solicitudes de licencia. Su método `getRequests()` devuelve una lista de objetos `LicenseRequestMessage`.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Esta es la clase de mensaje de solicitud. El llamante debe iterar a través de la lista `LicenseRequestMessage` devuelta por `getRequests()` y, para cada solicitud, generar una licencia o establecer un código de error. Llame a `LicenseRequestMessage.getContentInfo()` para obtener información extraída de los metadatos del contenido, incluyendo el ID de contenido, el ID de licencia y las políticas de DRM.

Las licencias y los errores se envían al mismo tiempo que se llama al método `LicenseHandler.close()`.

Consulte la [documentación de referencia de la API del servidor DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) para obtener más información.
