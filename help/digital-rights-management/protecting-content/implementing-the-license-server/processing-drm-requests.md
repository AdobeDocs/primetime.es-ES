---
seo-title: Procesar solicitudes DRM de Adobe Primetime
title: Procesar solicitudes DRM de Adobe Primetime
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# Procesar solicitudes DRM de Adobe Primetime {#process-adobe-primetime-drm-requests}

El método general para administrar solicitudes es crear un controlador, analizar la solicitud, establecer los datos de respuesta o el código de error y cerrar el controlador.

La clase base utilizada para controlar la interacción de una solicitud o respuesta es `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Se utiliza una instancia de la `HandlerConfiguration` clase para inicializar el controlador. `HandlerConfiguration` almacena información de configuración del servidor, incluidas las credenciales de transporte, la tolerancia de marca de hora, las listas de actualización de directiva y las listas de revocación. El controlador lee los datos de la solicitud y los analiza en una instancia de `RequestMessageBase`. El llamante puede examinar la información de la solicitud y decidir si devuelve un error o una respuesta correcta (las subclases de `RequestMessageBase` proporcionan un método para configurar los datos de respuesta).

Si la solicitud es correcta, configure los datos de respuesta; de lo contrario, invoque `RequestMessageBase.setErrorData()` si se produce un error. Siempre finalice la implementación invocando el `close()` método (se recomienda que `close()` se llame en el `finally` bloque de una `try` instrucción). Consulte la documentación de referencia de la `MessageHandlerBase` API para ver un ejemplo de cómo invocar el controlador.

>[!NOTE]
>
>El código de estado HTTP 200 (OK) debe enviarse en respuesta a todas las solicitudes procesadas por el controlador. Si no se pudo crear el controlador debido a un error de servidor, el servidor puede responder con otro código de estado, como 500 (error interno del servidor).

El cliente utiliza la dirección URL del servidor de licencias especificada en el momento del empaquetado como dirección URL base para todas las solicitudes enviadas al servidor de licencias. Por ejemplo, si la dirección URL del servidor se especifica como &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, el cliente envía solicitudes a &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]> Vea las siguientes secciones para obtener detalles sobre la ruta específica utilizada para cada tipo de solicitud. Al implementar el servidor de licencias, asegúrese de que el servidor responde a las rutas requeridas para cada tipo de solicitud.

Una solicitud de licencia puede contener un token de autenticación. Si se utilizó la autenticación de nombre de usuario y contraseña, la solicitud puede contener un `AuthenticationToken` generado por el `AuthenticationHandler`, y el SDK se asegurará de que el token sea válido antes de emitir una licencia.

## Usar identificadores de máquina {#use-machine-identifiers}

Todas las solicitudes DRM de Adobe Primetime (excepto las solicitudes que admiten compatibilidad con FMRMS) incluyen información sobre el autentificador del equipo que se ha emitido al cliente durante la individualización. El autentificador del equipo incluye un identificador de equipo, que se ha asignado durante la individualización. Puede utilizar este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Puede utilizar un identificador como se indica a continuación:

* El `getUniqueId()` método devuelve una cadena que se ha asignado a un dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambia si el usuario cambia el formato del disco duro y vuelve a individualizarse. Este identificador también tiene un valor diferente entre Adobe AIR y el Flash Player de Adobe en distintos exploradores del mismo equipo.
* Si desea contar los equipos con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si la máquina ya se ha visto antes, obtenga todos los identificadores de un nombre de usuario y llame `matches()` para comprobar si hay alguna coincidencia. Dado que el `matches()` método debe utilizarse para comparar los valores devueltos por `MachineId.getBytes`, esta opción sólo es práctica cuando hay un pequeño número de valores que comparar; por ejemplo, los equipos asociados a un usuario en particular.

## Autenticación de usuarios {#user-authentication}

Una solicitud de Adobe Primetime DRM puede contener un autentificador.

Si se utilizó la autenticación de nombre de usuario y contraseña, la solicitud puede incluir un `AuthenticationToken` generado por el `AuthenticationHandler`. Si desea acceder y verificar el token, debe utilizarlo `RequestMessageBase.getAuthenticationToken()`. Para iniciar una solicitud de nombre de usuario y contraseña en el cliente, utilice el `DRMManager.authenticate()` ActionScript o la API de iOS.

Si el cliente y el servidor utilizan un mecanismo de autenticación personalizado, el cliente obtiene un autentificador de autenticación mediante otro canal y establece el autentificador de autenticación personalizado mediante la API de `DRMManager.setAuthenticationToken` ActionScript 3.0. Se utiliza `RequestMessageBase.getRawAuthenticationToken()` para obtener el token de autenticación personalizado. La implementación del servidor determina si el autentificador personalizado es válido.

## Protección contra repetición {#replay-protection}

Para proteger la reproducción, es posible que desee comprobar si el identificador de mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante podría estar tratando de reproducir la solicitud, lo cual debería ser denegado. Para detectar los intentos de reproducción, el servidor puede almacenar una lista de los identificadores de mensaje vistos recientemente y comprobar cada solicitud entrante con la lista en caché. Para limitar la cantidad de tiempo que deben almacenarse los identificadores de mensaje, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK deniega toda solicitud que lleve una marca de tiempo durante más de los segundos especificados de la hora del servidor.

## Detección de retroceso {#rollback-detection}

Para la detección de rollback, algunas reglas de uso requieren que el cliente mantenga la información de estado para la aplicación de los derechos. Por ejemplo, para aplicar la regla de uso de la ventana de reproducción, el cliente almacena la fecha y la hora en que el usuario comenzó a ver el contenido por primera vez. Este evento desencadena el inicio de la ventana de reproducción. Para aplicar de forma segura la ventana de reproducción, el servidor debe asegurarse de que el usuario no realiza copias de seguridad y restaura el estado del cliente para eliminar el tiempo de inicio de la ventana de reproducción almacenado en el cliente. El servidor hace esto rastreando el valor del contador de rollback del cliente.

Para cada solicitud, el servidor obtiene el valor del contador llamando `RequestMessageBase.getClientState()` para obtener el `ClientState` objeto y luego `ClientState.getCounter()` para obtener el valor actual del contador de estado del cliente. El servidor debe almacenar este valor para cada cliente (utilizar `MachineId.getUniqueId()` para identificar el cliente asociado con el valor del contador de rollback) y, a continuación, llamar `ClientState.incrementCounter()` para aumentar el valor del contador en uno. Si el servidor detecta que el valor del contador es menor que el último valor visto por el servidor, es posible que el estado del cliente se haya revertido.

Consulte la documentación de referencia de la `ClientState` API para obtener más información sobre la detección de manipulaciones en el estado del cliente.

## Datos de configuración del servidor global{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se realiza creando una `ServerConfigData` clase y llamando `HandlerConfiguration.setServerConfigData()`. Esta configuración solo se aplica a las licencias emitidas por este servidor de licencias.

La tolerancia a la parabrisas del reloj es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar 4 horas el reloj del equipo sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede establecer en la `ServerConfigData` clase. Cuando cambie el valor de cualquiera de estas opciones de configuración, asegúrese de incrementar el número de versión llamando a `setVersion()`. Los nuevos valores solo se envían al cliente si la versión del cliente es anterior a la `ServerConfigData` versión actual.

## Archivo de política DRM de dominio cruzado {#crossdomain-drm-policy-file}

Si el servidor de licencias está alojado en un dominio distinto del SWF de reproducción de vídeo, se necesita un archivo de política DRM entre dominios ( [!DNL crossdomain.xml]) para permitir que el SWF solicite licencias desde un servidor de licencias. Un archivo de política DRM entre dominios está representado por un archivo XML que permite al servidor indicar que sus datos y documentos están disponibles para los archivos SWF que se ofrecen desde otros dominios. Cualquier archivo SWF servido desde un dominio especificado en el archivo de política DRM entre dominios del servidor de licencias puede acceder a los datos o recursos de dicho servidor de licencias.

Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de directivas entre dominios, permitiendo únicamente que los dominios de confianza tengan acceso al servidor de licencias y limitando el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de política DRM entre dominios, consulte las siguientes ubicaciones:

* Controles del sitio web (archivos de política DRM)
* Especificación de archivo de directiva DRM entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)