---
seo-title: Información general
title: Información general
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Información general{#overview}

El método general para gestionar solicitudes es crear un controlador, analizar la solicitud, establecer los datos de respuesta o el código de error y cerrar el controlador.

La clase base utilizada para administrar la interacción de una sola solicitud/respuesta es `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Se utiliza una instancia de la clase `HandlerConfiguration` para inicializar el controlador. `HandlerConfiguration` almacena información de configuración del servidor, incluidas las credenciales de transporte, la tolerancia de marca de hora, las listas de actualización de directiva y las listas de revocación. El controlador lee los datos de la solicitud y los analiza en una instancia de  `RequestMessageBase`. El llamante puede examinar la información de la solicitud y decidir si devuelve un error o una respuesta correcta (las subclases de `RequestMessageBase` proporcionan un método para configurar los datos de respuesta).

Si la solicitud se realiza correctamente, configure los datos de respuesta; de lo contrario, invoque `RequestMessageBase.setErrorData()` si se produce un error. Siempre finalice la implementación invocando el método `close()` (se recomienda llamar a `close()` en el bloque `finally` de una sentencia `try`). Consulte la documentación de referencia de la API `MessageHandlerBase` para ver un ejemplo de cómo invocar el controlador.

>[!NOTE]
>
>El código de estado HTTP 200 (OK) debe enviarse en respuesta a todas las solicitudes procesadas por el controlador. Si no se pudo crear el controlador debido a un error de servidor, el servidor puede responder con otro código de estado, como 500 (error interno del servidor).

El cliente utiliza la dirección URL del servidor de licencias especificada en el momento del empaquetado como dirección URL base para todas las solicitudes enviadas al servidor de licencias. Por ejemplo, si la dirección URL del servidor se especifica como &quot;ht<span></span>tps://licenseserver.com/path&quot;, el cliente enviará solicitudes a &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/...&quot;. Consulte las secciones siguientes para obtener detalles sobre la ruta específica utilizada para cada tipo de solicitud. Al implementar el servidor de licencias, asegúrese de que el servidor responde a las rutas requeridas para cada tipo de solicitud.

Una solicitud de licencia puede contener un token de autenticación. Si se utilizó la autenticación de nombre de usuario y contraseña, la solicitud puede contener un `AuthenticationToken` generado por `AuthenticationHandler` y el SDK se asegurará de que el token sea válido antes de emitir una licencia.
