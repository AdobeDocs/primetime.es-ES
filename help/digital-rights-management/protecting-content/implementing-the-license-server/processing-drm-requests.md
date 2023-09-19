---
title: Procesamiento de solicitudes de DRM de Adobe Primetime
description: Procesamiento de solicitudes de DRM de Adobe Primetime
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# Procesamiento de solicitudes de DRM de Adobe Primetime {#process-adobe-primetime-drm-requests}

El enfoque general para administrar solicitudes es crear un controlador, analizarlo, establecer los datos de respuesta o el código de error y cerrar el controlador.

La clase base utilizada para controlar la interacción de solicitud/respuesta única es `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Una instancia de `HandlerConfiguration` se utiliza para inicializar el controlador. `HandlerConfiguration` almacena información de configuración del servidor, incluidas credenciales de transporte, tolerancia de marca de tiempo, listas de actualización de directivas y listas de revocación. El controlador lee los datos de solicitud y analiza la solicitud en una instancia de `RequestMessageBase`. El llamador puede examinar la información de la solicitud y decidir si devuelve un error o una respuesta correcta (subclases de `RequestMessageBase` proporciona un método para configurar los datos de respuesta).

Si la solicitud se realiza correctamente, establezca los datos de respuesta; de lo contrario, invoque `RequestMessageBase.setErrorData()` en caso de fallo. Finalice siempre la implementación invocando el `close()` método (se recomienda que `close()` se llamará en el `finally` bloque de a `try` ; instrucción). Consulte la `MessageHandlerBase` Documentación de referencia de la API para ver un ejemplo de cómo invocar el controlador.

>[!NOTE]
>
>El código de estado HTTP 200 (OK) debe enviarse en respuesta a todas las solicitudes procesadas por el controlador. Si no se pudo crear el controlador debido a un error del servidor, éste puede responder con otro código de estado, como 500 (Error interno del servidor).

El cliente utiliza la URL del servidor de licencias especificada en el momento del empaquetado como URL base para todas las solicitudes enviadas al servidor de licencias. Por ejemplo, si la dirección URL del servidor se especifica como &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, el cliente envía solicitudes a &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]> Consulte las secciones siguientes para obtener más información sobre la ruta específica utilizada para cada tipo de solicitud. Al implementar el servidor de licencias, asegúrese de que este responda a las rutas necesarias para cada tipo de solicitud.

Una solicitud de licencia puede contener un token de autenticación. Si se ha utilizado la autenticación de nombre de usuario y contraseña, la solicitud puede contener un `AuthenticationToken` generado por el `AuthenticationHandler`, y el SDK se asegurará de que el token sea válido antes de emitir una licencia.

## Usar identificadores de equipo {#use-machine-identifiers}

Todas las solicitudes de DRM de Adobe Primetime (excepto las solicitudes que admiten la compatibilidad con FRMS) incluyen información sobre el token de equipo que se ha emitido al cliente durante la individualización. El token de equipo incluye un ID de equipo, que es un identificador que se ha asignado durante la individualización. Puede utilizar este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Puede utilizar un identificador de la siguiente manera:

* El `getUniqueId()` El método devuelve una cadena que se ha asignado a un dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambia si el usuario vuelve a dar formato al disco duro y vuelve a individualizar. Este identificador también tiene un valor diferente entre Adobe AIR y el Flash Player de Adobe en distintos navegadores del mismo equipo.
* Si desea contar los equipos con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si el equipo ya se ha visto antes, obtenga todos los identificadores para un nombre de usuario y llame a `matches()` para comprobar si hay alguna coincidencia. Debido a que el `matches()` debe utilizarse para comparar los valores devueltos por `MachineId.getBytes`Sin embargo, esta opción solo es práctica cuando hay un pequeño número de valores que comparar; por ejemplo, los equipos asociados con un usuario en particular.

## Autenticación de usuario {#user-authentication}

Una solicitud de DRM de Adobe Primetime puede contener un token de autenticación.

Si se ha utilizado la autenticación de nombre de usuario y contraseña, la solicitud puede incluir un `AuthenticationToken` generado por el `AuthenticationHandler`. Si desea acceder y verificar el token, debe utilizar `RequestMessageBase.getAuthenticationToken()`. Para iniciar una solicitud de nombre de usuario y contraseña en el cliente, utilice el `DRMManager.authenticate()` ActionScript o API de iOS.

Si el cliente y el servidor utilizan un mecanismo de autenticación personalizado, el cliente obtiene un token de autenticación a través de algún otro canal y establece el token de autenticación personalizado utilizando `DRMManager.setAuthenticationToken` API de ActionScript 3.0. Uso `RequestMessageBase.getRawAuthenticationToken()` para obtener el token de autenticación personalizado. La implementación del servidor determina si el token de autenticación personalizado es válido.

## Protección de repetición {#replay-protection}

Para la protección de reproducción, es posible que desee comprobar si el identificador del mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante puede estar intentando reproducir la solicitud, lo que debería denegarse. Para detectar intentos de reproducción, el servidor puede almacenar una lista de ID de mensajes vistos recientemente y comprobar cada solicitud entrante en la lista en caché. Para limitar la cantidad de tiempo que se deben almacenar los identificadores de mensajes, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK deniega cualquier solicitud que lleve una marca de tiempo durante más del número especificado de segundos fuera del tiempo del servidor.

## Detección de reversión {#rollback-detection}

Para la detección de reversiones, algunas reglas de uso requieren que el cliente mantenga la información de estado para la aplicación de los derechos. Por ejemplo, para aplicar la regla de uso de la ventana de reproducción, el cliente almacena la fecha y la hora en que el usuario empezó a ver el contenido por primera vez. Este evento déclencheur el inicio de la ventana de reproducción. Para aplicar de forma segura la ventana de reproducción, el servidor debe asegurarse de que el usuario no realiza una copia de seguridad ni restaura el estado del cliente para eliminar la hora de inicio de la ventana de reproducción almacenada en el cliente. Para ello, el servidor realiza un seguimiento del valor del contador de reversión del cliente.

Para cada solicitud, el servidor obtiene el valor del contador llamando a `RequestMessageBase.getClientState()` para obtener la `ClientState` objeto, luego llamar a `ClientState.getCounter()` para obtener el valor actual del contador de estado del cliente. El servidor debe almacenar este valor para cada cliente (utilice `MachineId.getUniqueId()` para identificar al cliente asociado con el valor del contador de reversión y, a continuación, llame a `ClientState.incrementCounter()` para aumentar el valor del contador en uno. Si el servidor detecta que el valor del contador es menor que el último valor que vio el servidor, es posible que se haya revertido el estado del cliente.

Consulte la `ClientState` Documentación de referencia de la API para obtener más información sobre la detección de alteraciones del estado del cliente.

## Datos de configuración global del servidor{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se hace creando un `ServerConfigData` clase y llamada `HandlerConfiguration.setServerConfigData()`. Esta configuración sólo se aplica a las licencias emitidas por este servidor de licencias.

La tolerancia del reloj contra devoluciones es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar el reloj del equipo 4 horas sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede establecer en la variable `ServerConfigData` clase. Cuando cambie el valor de cualquiera de estas configuraciones, asegúrese de incrementar el número de versión llamando a `setVersion()`. Los nuevos valores solo se envían al cliente si la versión del cliente es anterior a la actual `ServerConfigData` versión.

## Archivo de directiva DRM entre dominios {#crossdomain-drm-policy-file}

Si el servidor de licencias está alojado en un dominio diferente al del SWF de reproducción de vídeo, cree un archivo de directiva DRM entre dominios ( [!DNL crossdomain.xml]) es necesario para permitir que el SWF solicite licencias de un servidor de licencias. Un archivo de directiva DRM entre dominios se representa mediante un archivo XML que permite al servidor indicar que sus datos y documentos están disponibles para archivos de SWF proporcionados por otros dominios. Cualquier archivo de SWF servido desde un dominio especificado en el archivo de directiva DRM entre dominios del servidor de licencias puede acceder a los datos o recursos de ese servidor de licencias.

El Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de directivas entre dominios, ya que solo permite a los dominios de confianza acceder al servidor de licencias y limita el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de política DRM entre dominios, consulte las siguientes ubicaciones:

* Controles de sitio Web (archivos de directiva DRM)
* Especificación del archivo de política DRM entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
