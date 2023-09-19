---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Información general{#overview}

Para solicitar una licencia, el cliente envía los metadatos incrustados en el contenido durante el empaquetado. El servidor de licencias utiliza la información de los metadatos de contenido para generar una licencia.

El `LicenseHandler` lee una solicitud de licencia y la analiza. `LicenseHandler`extiende `BatchHandlerBase` para admitir solicitudes de licencia por lotes, aunque esta característica no es compatible actualmente con los clientes de acceso de Adobe. El `getRequests()` El método devolverá una lista de `LicenseRequestMessage` objetos. El autor de la llamada debe iterar a través de `LicenseRequestMessages`y, para cada solicitud, genere una licencia o defina un código de error (consulte la `LicenseRequestMessage` Documentación de referencia de la API para obtener más información). Para cada solicitud de licencia, el servidor determina si emitirá una licencia. Llamada `LicenseRequestMessage.getContentInfo()` para obtener información extraída de los metadatos de contenido, incluido el ID de contenido, el ID de licencia y las directivas.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de solicitud es &quot;URL del servidor de licencias en los metadatos: + &quot;/flashaccess/license/v4&quot;. Si la versión 3 del protocolo es la máxima admitida por el cliente o el servidor, los clientes de acceso de Adobe enviarán solicitudes de autenticación a &quot;URL del servidor de licencias en los metadatos&quot; + &quot;/flashaccess/license/v3&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en los metadatos&quot; + &quot;/flashaccess/license/v1&quot;

Si se produce un error al analizar la solicitud, aparece un `HandlerParsingException` se ha lanzado. Esta excepción contiene información de error que se va a devolver al cliente. Para recuperar la información de error, llame a `HandlerParsingException.getErrorData()`. Si se produce un error durante la generación de una licencia porque no se han cumplido los requisitos de la directiva, un `PolicyEvaluationException` se ha lanzado. Esta excepción también incluye `ErrorData` para que se devuelva al cliente. Consulte la documentación de la API para `LicenseRequestMessage.generateLicense()` para obtener más información sobre cómo se evalúan las directivas durante la generación de licencias.

Las licencias y los errores se envían al mismo tiempo cuando `LicenseHandler.close()` se llama.

Un dispositivo puede tener varias licencias para el mismo contenido (el mismo ID de licencia), pero solo puede tener una licencia para un ID de licencia e ID de política en particular. Si recibe una licencia con un ID de licencia/ID de política duplicado, la nueva licencia reemplazará la antigua solo si la fecha de emisión de la nueva licencia es posterior a la fecha de emisión de la licencia existente. Esta lógica se utiliza para procesar licencias incrustadas en el contenido. Por lo tanto, no se recomienda incrustar más de una licencia con el mismo ID de política en un fragmento de contenido. La misma lógica se aplica a las licencias que se pasan al cliente a través de `DRMManager.storeVoucher()` API de ActionScript 3; si el cliente ya posee una licencia con una fecha de emisión posterior, la licencia proporcionada puede ignorarse.
