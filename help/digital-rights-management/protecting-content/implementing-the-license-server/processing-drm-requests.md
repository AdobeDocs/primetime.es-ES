---
title: Procesamiento de solicitudes de Adobe Primetime DRM
description: Procesamiento de solicitudes de Adobe Primetime DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# Procesar solicitudes de Adobe Primetime DRM {#process-adobe-primetime-drm-requests}

El método general para administrar solicitudes es crear un controlador, analizar la solicitud, configurar los datos de respuesta o el código de error y cerrar el controlador.

La clase base utilizada para gestionar la interacción de solicitud/respuesta única es `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Se utiliza una instancia de la clase `HandlerConfiguration` para inicializar el controlador. `HandlerConfiguration` almacena información de configuración del servidor, incluidas las credenciales de transporte, la tolerancia de marca de tiempo, las listas de actualización de directivas y las listas de revocación. El controlador lee los datos de solicitud y analiza la solicitud en una instancia de  `RequestMessageBase`. El llamador puede examinar la información de la solicitud y decidir si devuelve un error o una respuesta correcta (las subclases de `RequestMessageBase` proporcionan un método para configurar los datos de respuesta).

Si la solicitud se realiza correctamente, establezca los datos de respuesta; de lo contrario, invoque `RequestMessageBase.setErrorData()` en caso de error. Para finalizar siempre la implementación, invoque el método `close()` (se recomienda llamar a `close()` en el bloque `finally` de una sentencia `try`). Consulte la documentación de referencia de la API `MessageHandlerBase` para ver un ejemplo de cómo invocar el controlador.

>[!NOTE]
>
>El código de estado HTTP 200 (OK) debe enviarse en respuesta a todas las solicitudes procesadas por el controlador. Si no se pudo crear el controlador debido a un error del servidor, el servidor puede responder con otro código de estado, como 500 (error interno del servidor).

El cliente utiliza la URL del servidor de licencias especificada en el momento del empaquetado como URL base para todas las solicitudes enviadas al servidor de licencias. Por ejemplo, si la dirección URL del servidor se especifica como &lt;[!DNL ht<span></span>tps://licenseserver.com/path], el cliente envía solicitudes a &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...] Consulte las siguientes secciones para obtener detalles sobre la ruta específica utilizada para cada tipo de solicitud. Al implementar el servidor de licencias, asegúrese de que el servidor responda a las rutas requeridas para cada tipo de solicitud.

Una solicitud de licencia puede contener un token de autenticación. Si se utilizó la autenticación de nombre de usuario/contraseña, la solicitud puede contener un `AuthenticationToken` generado por el `AuthenticationHandler` y el SDK se asegurará de que el token sea válido antes de emitir una licencia.

## Usar identificadores de máquina {#use-machine-identifiers}

Todas las solicitudes de Adobe Primetime DRM (excepto las solicitudes que admiten la compatibilidad con FMRMS) incluyen información sobre el token de equipo que se ha emitido al cliente durante la personalización. El token de equipo incluye un ID de equipo, que es un identificador que se ha asignado durante la individualización. Puede utilizar este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Puede utilizar un identificador como se indica a continuación:

* El método `getUniqueId()` devuelve una cadena que se ha asignado a un dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambia si el usuario vuelve a dar formato al disco duro y se vuelve a individualizar. Este identificador también tiene un valor diferente entre Adobe AIR y el Flash Player de Adobe en distintos navegadores del mismo equipo.
* Si desea contar los equipos con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si el equipo se ha visto antes, obtenga todos los identificadores de un nombre de usuario e invoque `matches()` para comprobar si hay alguna coincidencia. Dado que el método `matches()` debe usarse para comparar los valores devueltos por `MachineId.getBytes`, esta opción solo es práctica cuando hay un pequeño número de valores para comparar; por ejemplo, las máquinas asociadas a un usuario en particular.

## Autenticación de usuario {#user-authentication}

Una solicitud de Adobe Primetime DRM puede contener un token de autenticación.

Si se utilizó la autenticación de nombre de usuario/contraseña, la solicitud puede incluir un `AuthenticationToken` generado por el `AuthenticationHandler`. Si desea acceder y verificar el token, debe utilizar `RequestMessageBase.getAuthenticationToken()`. Para iniciar una solicitud de nombre de usuario y contraseña en el cliente, utilice el ActionScript `DRMManager.authenticate()` o la API de iOS.

Si el cliente y el servidor utilizan un mecanismo de autenticación personalizado, el cliente obtiene un token de autenticación a través de otro canal y establece el token de autenticación personalizado mediante la API `DRMManager.setAuthenticationToken` ActionScript 3.0. Utilice `RequestMessageBase.getRawAuthenticationToken()` para obtener el token de autenticación personalizado. La implementación del servidor determina si el token de autenticación personalizado es válido.

## Protección contra repetición {#replay-protection}

Para la protección de repetición, es posible que desee comprobar si el identificador de mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante podría estar intentando reproducir la solicitud, lo que debería ser denegado. Para detectar los intentos de reproducción, el servidor puede almacenar una lista de id de mensajes vistos recientemente y comprobar cada solicitud entrante con la lista en caché. Para limitar la cantidad de tiempo que se deben almacenar los identificadores de mensaje, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK deniega cualquier solicitud que lleve una marca de tiempo durante más de la cantidad especificada de segundos desde la hora del servidor.

## Detección de reversión {#rollback-detection}

Para la detección de reversión, algunas reglas de uso requieren que el cliente mantenga la información de estado para la aplicación de los derechos. Por ejemplo, para aplicar la regla de uso de la ventana de reproducción, el cliente almacena la fecha y la hora en que el usuario empezó a ver el contenido por primera vez. Este evento déclencheur el inicio de la ventana de reproducción. Para aplicar de forma segura la ventana de reproducción, el servidor debe asegurarse de que el usuario no realiza una copia de seguridad y restaurar el estado del cliente para eliminar la hora de inicio de la ventana de reproducción almacenada en el cliente. El servidor hace esto rastreando el valor del contador de reversión del cliente.

Para cada solicitud, el servidor obtiene el valor del contador llamando a `RequestMessageBase.getClientState()` para obtener el objeto `ClientState` y luego llamando a `ClientState.getCounter()` para obtener el valor actual del contador de estado del cliente. El servidor debe almacenar este valor para cada cliente (utilice `MachineId.getUniqueId()` para identificar el cliente asociado con el valor del contador de reversión) y luego llamar a `ClientState.incrementCounter()` para aumentar el valor del contador en uno. Si el servidor detecta que el valor de contador es menor que el último valor visto por el servidor, es posible que el estado del cliente se haya revertido.

Consulte la documentación de referencia de la API `ClientState` para obtener más información sobre la detección de manipulaciones en el estado del cliente.

## Datos de configuración del servidor global{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se hace creando una clase `ServerConfigData` y llamando a `HandlerConfiguration.setServerConfigData()`. Esta configuración solo se aplica a las licencias emitidas por este servidor de licencias.

La tolerancia a la ventana del reloj es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar el reloj del equipo 4 horas sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede configurar en la clase `ServerConfigData`. Cuando cambie el valor de cualquiera de estas configuraciones, asegúrese de aumentar el número de versión llamando a `setVersion()`. Los nuevos valores solo se envían al cliente si la versión del cliente es anterior a la versión actual `ServerConfigData`.

## Archivo de directiva DRM de dominio cruzado {#crossdomain-drm-policy-file}

Si el servidor de licencias está alojado en un dominio diferente al SWF de reproducción de vídeo, se necesita un archivo de directiva DRM entre dominios ( [!DNL crossdomain.xml]) para permitir que el SWF solicite licencias a un servidor de licencias. Un archivo de directiva DRM entre dominios está representado por un archivo XML que permite al servidor indicar que sus datos y documentos están disponibles para archivos SWF servidos desde otros dominios. Cualquier archivo SWF servido desde un dominio especificado en el archivo de directiva DRM entre dominios del servidor de licencias puede acceder a los datos o recursos desde ese servidor de licencias.

Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de directivas entre dominios permitiendo que los dominios de confianza accedan al servidor de licencias y limitando el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de directiva DRM entre dominios, consulte las siguientes ubicaciones:

* Controles de sitios web (archivos de directivas DRM)
* Especificación de archivo de directiva DRM entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)