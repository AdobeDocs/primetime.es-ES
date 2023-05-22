---
title: Información general
description: Información general
copied-description: true
exl-id: d284b279-d261-4573-825d-919a551b3194
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Información general{#overview}

El enfoque general para administrar solicitudes es crear un controlador, analizarlo, establecer los datos de respuesta o el código de error y cerrar el controlador.

La clase base utilizada para controlar la interacción de solicitud/respuesta única es `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Una instancia de `HandlerConfiguration` se utiliza para inicializar el controlador. `HandlerConfiguration` almacena información de configuración del servidor, incluidas credenciales de transporte, tolerancia de marca de tiempo, listas de actualización de directivas y listas de revocación. El controlador lee los datos de solicitud y analiza la solicitud en una instancia de `RequestMessageBase`. El llamador puede examinar la información de la solicitud y decidir si devuelve un error o una respuesta correcta (subclases de `RequestMessageBase` proporciona un método para configurar los datos de respuesta).

Si la solicitud se realiza correctamente, establezca los datos de respuesta; de lo contrario, invoque `RequestMessageBase.setErrorData()` en caso de fallo. Finalice siempre la implementación invocando el `close()` método (se recomienda que `close()` se llamará en el `finally` bloque de a `try` ; instrucción). Consulte la `MessageHandlerBase` Documentación de referencia de la API para ver un ejemplo de cómo invocar el controlador.

>[!NOTE]
>
>El código de estado HTTP 200 (OK) debe enviarse en respuesta a todas las solicitudes procesadas por el controlador. Si no se pudo crear el controlador debido a un error del servidor, éste puede responder con otro código de estado, como 500 (Error interno del servidor).

El cliente utiliza la URL del servidor de licencias especificada en el momento del empaquetado como URL base para todas las solicitudes enviadas al servidor de licencias. Por ejemplo, si la dirección URL del servidor se especifica como &quot;visita<span></span>tps://licenseserver.com/path&quot;, el cliente enviará solicitudes a &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/...&quot;. Consulte las secciones siguientes para obtener más información sobre la ruta específica utilizada para cada tipo de solicitud. Al implementar el servidor de licencias, asegúrese de que este responda a las rutas necesarias para cada tipo de solicitud.

Una solicitud de licencia puede contener un token de autenticación. Si se ha utilizado la autenticación de nombre de usuario y contraseña, la solicitud puede contener un `AuthenticationToken` generado por el `AuthenticationHandler`, y el SDK se asegurará de que el token sea válido antes de emitir una licencia.
