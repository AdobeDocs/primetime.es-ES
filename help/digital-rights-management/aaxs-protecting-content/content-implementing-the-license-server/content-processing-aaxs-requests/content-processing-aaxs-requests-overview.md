---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Información general{#overview}

El método general para gestionar solicitudes es crear un controlador, analizar la solicitud, establecer los datos de respuesta o el código de error y cerrar el controlador.

La clase base utilizada para gestionar la interacción de solicitud/respuesta única es `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Se utiliza una instancia de la clase `HandlerConfiguration` para inicializar el controlador. `HandlerConfiguration` almacena información de configuración del servidor, incluidas las credenciales de transporte, la tolerancia de marca de tiempo, las listas de actualización de directivas y las listas de revocación. El controlador lee los datos de solicitud y analiza la solicitud en una instancia de  `RequestMessageBase`. El llamador puede examinar la información de la solicitud y decidir si devuelve un error o una respuesta correcta (las subclases de `RequestMessageBase` proporcionan un método para configurar los datos de respuesta).

Si la solicitud se realiza correctamente, establezca los datos de respuesta; de lo contrario, invoque `RequestMessageBase.setErrorData()` en caso de error. Para finalizar siempre la implementación, invoque el método `close()` (se recomienda llamar a `close()` en el bloque `finally` de una sentencia `try`). Consulte la documentación de referencia de la API `MessageHandlerBase` para ver un ejemplo de cómo invocar el controlador.

>[!NOTE]
>
>El código de estado HTTP 200 (OK) debe enviarse en respuesta a todas las solicitudes procesadas por el controlador. Si no se pudo crear el controlador debido a un error del servidor, el servidor puede responder con otro código de estado, como 500 (error interno del servidor).

El cliente utiliza la URL del servidor de licencias especificada en el momento del empaquetado como URL base para todas las solicitudes enviadas al servidor de licencias. Por ejemplo, si la URL del servidor se especifica como &quot;ht<span></span>tps://licenseserver.com/path&quot;, el cliente enviará solicitudes a &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/...&quot;. Consulte las secciones siguientes para obtener detalles sobre la ruta específica utilizada para cada tipo de solicitud. Al implementar el servidor de licencias, asegúrese de que el servidor responda a las rutas requeridas para cada tipo de solicitud.

Una solicitud de licencia puede contener un token de autenticación. Si se utilizó la autenticación de nombre de usuario/contraseña, la solicitud puede contener un `AuthenticationToken` generado por el `AuthenticationHandler` y el SDK se asegurará de que el token sea válido antes de emitir una licencia.
