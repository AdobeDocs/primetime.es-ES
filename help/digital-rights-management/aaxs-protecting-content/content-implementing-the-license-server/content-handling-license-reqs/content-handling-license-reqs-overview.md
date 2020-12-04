---
seo-title: Información general
title: Información general
uuid: d3bfa65b-2360-4843-b59e-71451fa62a2c
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Información general{#overview}

Para solicitar una licencia, el cliente envía los metadatos incrustados en el contenido durante el empaquetado. El servidor de licencias utiliza la información de los metadatos de contenido para generar una licencia.

El `LicenseHandler` lee una solicitud de licencia y la analiza. `LicenseHandler`se amplía  `BatchHandlerBase` para dar cabida a solicitudes de licencia por lotes, aunque los clientes de Adobe Access no admiten actualmente esta función. El método `getRequests()` devolverá una Lista de objetos `LicenseRequestMessage`. El llamante debe iterar a través de `LicenseRequestMessages` y, para cada solicitud, generar una licencia o establecer un código de error (consulte la documentación de referencia de la API `LicenseRequestMessage` para obtener más información). Para cada solicitud de licencia, el servidor determina si emitirá una licencia. Llame a `LicenseRequestMessage.getContentInfo()` para obtener información extraída de los metadatos del contenido, incluyendo el ID de contenido, el ID de licencia y las políticas.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos: + &quot;/flashaccess/license/v4&quot;. Si la versión 3 del protocolo es la máxima admitida por el cliente o el servidor, los clientes de Adobe Access enviarán solicitudes de autenticación a &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/license/v3&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/license/v1&quot;

Si se produce un error al analizar la solicitud, se genera un `HandlerParsingException`. Esta excepción contiene información de error que se debe devolver al cliente. Para recuperar la información del error, llame a `HandlerParsingException.getErrorData()`. Si se produce un error al generar una licencia porque no se han cumplido los requisitos de directiva, se genera un `PolicyEvaluationException`. Esta excepción también incluye `ErrorData` que se devolverá al cliente. Consulte la documentación de API de `LicenseRequestMessage.generateLicense()` para obtener más información sobre cómo se evalúan las políticas durante la generación de licencias.

Las licencias y los errores se envían al mismo tiempo que se llama a `LicenseHandler.close()`.

Un dispositivo puede tener varias licencias para el mismo contenido (el mismo ID de licencia), pero solo puede tener una licencia para un ID de licencia y un ID de directiva concretos. Si recibe una licencia con un LicenseID/PolicyID de duplicado, la nueva licencia reemplazará a la anterior sólo si la fecha de emisión de la nueva licencia es posterior a la fecha de emisión de la licencia existente. Esta lógica se utiliza para procesar las licencias incrustadas en el contenido, por lo que no se recomienda incrustar más de una licencia con el mismo ID de directiva en un fragmento de contenido. La misma lógica se aplica a las licencias pasadas al cliente a través de la API de `DRMManager.storeVoucher()` ActionScript3; si el cliente ya posee una licencia con una fecha de emisión posterior, la licencia proporcionada puede ignorarse.
