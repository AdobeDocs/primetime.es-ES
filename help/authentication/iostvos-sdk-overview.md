---
title: Información general sobre el SDK de iOS/tvOS
description: Información general sobre el SDK de iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '3691'
ht-degree: 0%

---


# Información general sobre el SDK de iOS/tvOS {#iostvos-sdk-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


</br>


## Introducción {#intro}

iOS AccessEnabler es una biblioteca iOS/tvOS Objective-C que permite que las aplicaciones móviles utilicen la autenticación Adobe Primetime para los servicios de asignación de derechos de TV en todas partes. La implementación consiste en la variable *AccessEnabler* interfaz que define la API de asignación de derechos y la *EntitlementDelegate* y *[EntitlementStatus](#ios%20entitlement%20status)* protocolos que describen las llamadas de retorno que déclencheur la biblioteca . La interfaz, junto con el protocolo, se menciona con un nombre común: la biblioteca AccessEnabler.

## Requisitos de iOS y tvOS {#reqs}

Para conocer los requisitos técnicos actuales relacionados con la plataforma iOS y tvOS y la autenticación Primetime, consulte [Requisitos de plataforma/dispositivo/herramienta](#ios)y consulte las notas de la versión incluidas en la descarga del SDK. Durante el resto de esta página, verá secciones que señalan cambios que se aplican a versiones específicas del SDK y posteriores. Por ejemplo, la siguiente es una nota legítima sobre el SDK 1.7.5:

## Explicación de los flujos de trabajo de cliente nativos {#flows}

Los flujos de trabajo de cliente nativos suelen ser los mismos o muy similares a los de los clientes de autenticación Primetime basados en explorador. Sin embargo, hay algunas excepciones, como se describe a continuación.

- [Flujo de trabajo posterior a la inicialización](#post-init)
- [Flujo de trabajo de autenticación inicial genérico](#generic)
- [Flujo de trabajo de cierre de sesión](#logout)


### Flujo de trabajo posterior a la inicialización {#post-init}

Todos los flujos de trabajo de derechos admitidos por AccessEnabler suponen que ha invocado anteriormente [`setRequestor()`](#setReq) para establecer su identidad. Esta llamada se realiza para proporcionar el ID del solicitante solo una vez, normalmente durante la fase de inicialización/configuración de la aplicación.


Con un cliente nativo de iOS, después de la llamada inicial a [`setRequestor()`](#setReq), tiene la opción de continuar:

- Puede empezar a realizar llamadas de asignación de derechos inmediatamente y permitir que se pongan en cola sin aviso, si es necesario.

- Puede recibir una confirmación del éxito/fracaso de [`setRequestor()`](#setReq) implementando [`setRequestorComplete()`](#setReqComplete) llamada de retorno.

- Puede hacer lo anterior.

Es su elección hacer que la aplicación espere a que se le notifique el éxito de [`setRequestor()`](#setReq) o hacer que dependa del mecanismo de cola de llamadas de AccessEnabler. Dado que todas las solicitudes de autorización y autenticación posteriores necesitan el ID del solicitante y la información de configuración asociada, la variable [`setRequestor()`](#setReq) bloquea de forma eficaz todas las llamadas a la API de autenticación y autorización hasta que se complete la inicialización.

 

### Flujo de trabajo de autenticación inicial genérico {#generic}

El propósito de este flujo de trabajo es iniciar sesión en un usuario con su MVPD. Después de un inicio de sesión correcto, el servidor back-end envía al usuario un token de autenticación. Aunque la autenticación suele realizarse como parte del proceso de autorización, lo siguiente describe cómo puede funcionar la autenticación de forma aislada y no incluye ningún paso de autorización.

Tenga en cuenta que aunque este flujo de trabajo difiere para los clientes nativos del flujo de trabajo típico de autenticación basada en navegador, los pasos 1-5 son los mismos para los clientes nativos y los clientes basados en navegador.

1. La aplicación inicia el flujo de trabajo de autenticación con una llamada a la función `getAuthentication() `método de API, que comprueba si hay un token de autenticación en caché válido.
1. Si el usuario está autenticado actualmente, AccessEnabler llama a su [`setAuthenticationStatus()`](#setAuthNStatus) función de llamada de retorno, pasando un estado de autenticación que indica éxito y finalizando el flujo.
1. Si el usuario no está autenticado actualmente, AccessEnabler continúa el flujo de autenticación determinando si el último intento de autenticación del usuario fue exitoso con un MVPD determinado. Si un ID de MVPD se almacena en caché y el `canAuthenticate` El indicador es verdadero O se ha seleccionado un MVPD mediante [`setSelectedProvider()`](#setSelProv), el usuario no recibe el cuadro de diálogo de selección de MVPD. El flujo de autenticación continúa utilizando el valor almacenado en caché del MVPD (es decir, el mismo MVPD que se usó durante la última autenticación correcta). Se realiza una llamada de red al servidor back-end y se redirige al usuario a la página de inicio de sesión de MVPD (paso 6 a continuación).
1. Si no se almacena en caché ningún ID de MVPD y no se seleccionó ningún MVPD usando [`setSelectedProvider()`](#setSelProv) O bien, la variable `canAuthenticate` el indicador se establece en false, la variable [`displayProviderDialog()`](#dispProvDialog) llamada de retorno. Esta llamada de retorno ordena a su aplicación que cree la interfaz de usuario que ofrezca al usuario una lista de MVPD entre los que elegir. Se proporciona una matriz de objetos MVPD que contiene la información necesaria para crear el selector de MVPD. Cada objeto MVPD describe una entidad MVPD y contiene información como el ID del MVPD (por ejemplo, XFINITY, AT\&amp;T, etc.) y la URL donde se puede encontrar el logotipo de MVPD.
1. Una vez seleccionado un MVPD concreto, su aplicación debe informar al AccessEnabler de la elección del usuario. Una vez que el usuario selecciona el MVPD deseado, informará al AccessEnabler de la selección del usuario mediante una llamada al [`setSelectedProvider()`](#setSelProv) método.
1. iOS AccessEnabler llama a su `navigateToUrl:` callback o `navigateToUrl:useSVC:` llamada de retorno para redirigir al usuario a la página de inicio de sesión de MVPD. Al activar cualquiera de los dos, AccessEnabler realiza una solicitud a la aplicación para crear un `UIWebView/WKWebView or SFSafariViewController` y para cargar la URL proporcionada en la llamada de retorno `url` parámetro. Esta es la dirección URL del extremo de autenticación en el servidor back-end. Para tvOS AccessEnabler, la variable [status()](#status_callback_implementation) la llamada de retorno se llama con una `statusDictionary` y el sondeo para la segunda autenticación de pantalla se inicia inmediatamente. La variable `statusDictionary` contiene el `registration code` que debe utilizarse para la segunda autenticación de pantalla. 
1. En el caso de iOS AccessEnabler, el usuario accede a la página de inicio de sesión de MVPD para introducir sus credenciales a través del medio de su aplicación `UIWebView/WKWebView or SFSafariViewController `controlador. Tenga en cuenta que durante esta transferencia se producen varias operaciones de redireccionamiento y que la aplicación debe controlar las direcciones URL cargadas por el controlador durante las operaciones de redireccionamiento múltiple.
1. En el caso de iOS AccessEnabler, cuando la variable `UIWebView/WKWebView or SFSafariViewController` el controlador carga una dirección URL personalizada específica y la aplicación debe cerrar el controlador e invocar AccessEnabler `handleExternalURL:url `método de API. Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue realmente. Su aplicación solo debe interpretarla como una señal de que el flujo de autenticación se ha completado y de que es seguro cerrar el `UIWebView/WKWebView or SFSafariViewController` controlador. En caso de que la aplicación deba utilizar un `SFSafariViewController `controlador la URL personalizada específica la define el `application's custom scheme` (por ejemplo: `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta URL personalizada específica la define el `ADOBEPASS_REDIRECT_URL` constante (p. ej. `adobepass://ios.app`).
1. Una vez que la aplicación cierre `UIWebView/WKWebView or SFSafariViewController` controlador y llama a la función de AccessEnabler `handleExternalURL:url `método de API, AccessEnabler recupera el token de autenticación del servidor back-end e informa a la aplicación de que el flujo de autenticación ha finalizado. AccessEnabler llama a la función [`setAuthenticationStatus()`](#setAuthNStatus) llamada de retorno con un código de estado de 1, que indica que la llamada de retorno ha sido satisfactoria. Si hay un error durante la ejecución de estos pasos, la variable [`setAuthenticationStatus()`](#setAuthNStatus) la rellamada se activa con un código de estado de 0, que indica un error de autenticación, así como un código de error correspondiente.


>[!WARNING]
>
> Durante los pasos en los que AccessEnabler cede el control a su aplicación (es decir, cuando se muestra el cuadro de diálogo de selección del proveedor, o cuando se muestra UIWebView/WKWebView o SFSafariViewController ), el usuario tiene la oportunidad de cancelar el flujo de autenticación. En estas situaciones, la aplicación es responsable de informar a AccessEnabler sobre este evento y de llamar a la función [`setSelectedProvider()`](#setSelProv) método de API, pasando null como parámetro. Esto ofrece a AccessEnabler la oportunidad de limpiar su estado interno y restablecer el flujo de autenticación. En tvOS, puede utilizar el mismo método para cancelar la encuesta de autenticación.


### Flujo de trabajo de cierre de sesión {#logout}

Para los clientes nativos, el cierre de sesión se gestiona de forma similar al proceso de autenticación descrito anteriormente.

1. La aplicación inicia el flujo de trabajo de cierre de sesión con una llamada a la función `logout() `método de API. El cierre de sesión es el resultado de una serie de operaciones de redireccionamiento HTTP debido al hecho de que el usuario necesita cerrar la sesión tanto desde los servidores de autenticación de Primetime como desde los servidores de MVPD. Debido a que este flujo no se puede completar con una solicitud HTTP simple emitida por la biblioteca AccessEnabler, una `UIWebView/WKWebView or SFSafariViewController` debe crearse una instancia del controlador para poder seguir las operaciones de redireccionamiento HTTP.

1. Se utiliza un patrón similar al flujo de autenticación. iOS AccessEnabler déclencheur el `navigateToUrl:` o `navigateToUrl:useSVC:` para crear un `UIWebView/WKWebView or SFSafariViewController` y para cargar la URL proporcionada en la llamada de retorno `url` parámetro. Esta es la dirección URL del extremo de cierre de sesión en el servidor back-end. Para el AccessEnabler de tvOS ni el `navigateToUrl:` o `navigateToUrl:useSVC:` llamada de retorno.

1. A medida que pasa por varias redirecciones, la aplicación debe monitorizar la actividad de la variable `UIWebView/WKWebView or SFSafariViewController `controle y detecte el momento en que carga una URL personalizada específica. Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue realmente. Su aplicación solo debe interpretarla como una señal de que el flujo de cierre de sesión se ha completado y de que es seguro cerrar el controlador. Cuando el controlador carga esta dirección URL personalizada específica, la aplicación debe cerrar el controlador e invocar AccessEnabler `handleExternalURL:url `método de API. En caso de que la aplicación deba utilizar un `SFSafariViewController `controlador la URL personalizada específica la define el `application's custom scheme` (p. ej.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta URL personalizada específica la define el ` ADOBEPASS_REDIRECT_URL  `constante (p. ej. `adobepass://ios.app`).

1. Al final, AccessEnabler llamará a la función [`setAuthenticationStatus()`](#setAuthNStatus) llamada de retorno con un código de estado de 0, que indica el éxito del flujo de cierre de sesión.

El flujo de cierre de sesión difiere del flujo de autenticación en que no se requiere que el usuario interactúe con la variable `UIWebView/WKWebView or SFSafariViewController`  de cualquier manera. Por lo tanto, Adobe recomienda que haga el control invisible (es decir, oculto) durante el proceso de cierre de sesión.

## Tokens {#tokens}

- [Definiciones y uso](#definitions)
- [Directrices de almacenamiento en caché](#caching)
- [Persistencia](#persistence)
- [Formato](#format)
- [Enlace de dispositivos](#device_binding)


### Definiciones y uso {#definitions}

La solución de derechos de autenticación de Primetime gira en torno a la generación de datos específicos (tokens) que la autenticación de Primetime genera al completarse correctamente los flujos de trabajo de autenticación y autorización. Estos tokens se almacenan localmente en el dispositivo iOS del cliente.

 

Los tokens tienen una vida útil limitada; una vez caducado, es necesario volver a emitir los tokens mediante el reinicio de los flujos de trabajo de autenticación y/o autorización.

 

Hay tres tipos de tokens emitidos durante los flujos de trabajo de derechos:

- **Token de autenticación:** El resultado final del flujo de trabajo de autenticación de usuario será un GUID de autenticación que AccessEnabler puede utilizar para realizar consultas de autorización en nombre del usuario. Este GUID de autenticación tendrá un valor de tiempo de vida (TTL) asociado que puede ser diferente de la propia sesión de autenticación del usuario. Se generará un token de autenticación enlazando el GUID de autenticación al dispositivo que inicia las solicitudes de autenticación.
- **Token de autorización:** Otorga acceso a un recurso protegido específico identificado por un resourceID único. Consiste en una concesión de autorización expedida por la parte autorizadora junto con el resourceID original. Esta información está enlazada al dispositivo que inicia la solicitud.
- **Token de medio de corta duración:** AccessEnabler concede acceso a la aplicación de alojamiento de un recurso determinado devolviendo un token de medios de corta duración. Este token se genera en función del token de autorización adquirido anteriormente para ese recurso específico. Además, este token no está enlazado al dispositivo y la duración de vida asociada es significativamente más corta (de forma predeterminada: 5 minutos).

Tras la autenticación y autorización correctas, la autenticación de Primetime emitirá autenticación, autorización y tokens de medios de corta duración. Estos tokens deben almacenarse en caché en el dispositivo del usuario y utilizarse durante el periodo de duración asociado.

 

### Directrices de almacenamiento en caché {#caching}

- Token de autenticación
- Token de autorización
- Token de medio de corta duración


#### Token de autenticación

- **AccessEnabler 1.7:** Este SDK introduce un nuevo método de almacenamiento de tokens, que permite la creación de varios buckets Programmer-MVPD y, por lo tanto, de varios tokens de autenticación. Ahora, se utiliza el mismo diseño de almacenamiento para el escenario &quot;Autenticación por solicitante&quot; y para el flujo de autenticación normal. La única diferencia entre ambos reside en la forma en que se realiza la autenticación: &quot;Autenticación por solicitante&quot; contiene una nueva mejora (autenticación pasiva) que permite a AccessEnabler realizar autenticación en canales de retorno, en función de la existencia de un token de autenticación en el almacenamiento (para un programador diferente). El usuario solo tiene que autenticarse una vez, y esta sesión se utilizará para obtener tokens de autenticación en aplicaciones adicionales. Este flujo de canal posterior se produce durante la [`setRequestor()`](#setReq) y es mayormente transparente para el programador. **Sin embargo, hay un requisito importante aquí: el programador DEBE llamar a setRequestor() desde el subproceso de interfaz de usuario principal.**
- **AccessEnabler 1.6 y versiones anteriores:** La forma en que se almacenan en caché los tokens de autenticación en el dispositivo depende de la variable **Autenticación por solicitante&quot;** Indicador asociado con el MVPD actual:

<!-- end list -->

1. Si la función &quot;Autenticación por solicitante&quot; está deshabilitada, se almacenará localmente un único token de autenticación en la mesa de trabajo global; este token se compartirá entre todas las aplicaciones que estén integradas con el MVPD actual.
1. Si la función &quot;Autenticación por solicitante&quot; está habilitada, se asociará explícitamente un token al programador que realizó el flujo de autenticación (el token no se almacenará en la mesa de trabajo global, sino en un archivo privado visible únicamente a la aplicación de ese programador). Más específicamente, el inicio de sesión único (SSO) entre distintas aplicaciones se desactivará; el usuario deberá realizar el flujo de autenticación explícitamente al cambiar a una aplicación nueva (siempre que el programador de la segunda aplicación esté integrado con el MVPD actual y que no exista ningún token de autenticación para ese programador en la caché local).

 

#### Token de autorización

En un momento dado, AccessEnabler solo almacena en caché un token de autorización por RECURSO. Puede haber varios tokens de autorización en la caché, pero están asociados a diferentes recursos. Cuando se emite un nuevo token de autorización y ya existe uno antiguo para *el mismo recurso*, el nuevo token sobrescribe el valor almacenado en caché existente.

 

#### Token de medio

El token de medio de corta duración NO debe almacenarse en caché en absoluto. El token multimedia debe recuperarse del servidor cada vez que se llama a una API de autorización, ya que está restringido a un uso único.

 

### Persistencia {#persistence}

Los tokens deben ser persistentes en ejecuciones consecutivas de la misma aplicación. Esto significa que una vez que se han adquirido los tokens de autenticación y autorización y el usuario cierra la aplicación, los mismos tokens están disponibles para la aplicación cuando el usuario vuelve a abrir la aplicación. Además, es deseable que estos tokens sean persistentes en varias aplicaciones. En otras palabras, después de que un usuario utilice una aplicación para iniciar sesión con un proveedor de identidad específico (obteniendo correctamente la autenticación y los tokens de autorización), se pueden utilizar los mismos tokens a través de una aplicación diferente y ya no se solicita al usuario que especifique sus credenciales al iniciar sesión mediante el mismo proveedor de identidad. Este tipo de flujo de trabajo de autenticación y autorización optimizado es lo que hace que la solución de autenticación de Primetime sea una implementación verdadera de TV en todas partes. 

 

## iOS

La biblioteca iOS AccessEnabler resuelve los problemas del uso compartido de datos entre aplicaciones al almacenar los datos de token en una estructura de datos &quot;similar al portapapeles&quot; denominada *pegar tablero*. Este recurso compartido de nivel de sistema proporciona los ingredientes clave que permiten la implementación del caso de uso de tokens persistentes deseado:

- **Soporte para almacenamiento estructurado** - La placa de pegado no es sólo una estructura de memoria simple y lineal similar a un búfer. Proporciona un mecanismo de almacenamiento parecido a un diccionario que permite la indexación de datos en función de los valores clave especificados por el usuario.
- **Compatibilidad con la persistencia de datos mediante el sistema de archivos subyacente** - El contenido de la estructura de la placa de pegado puede marcarse como persistente, en cuyo caso los datos se guardan en la memoria interna del dispositivo.

 

Una vez que un token en particular se coloca en la caché de tokens, la biblioteca AccessEnabler comprueba su validez en diferentes momentos.  Un token válido se define como:

- El TTL del token no ha caducado.
- El emisor del token se incluye en la lista de proveedores de identidad permitidos.

 

## tvOS

Dado que en tvOS la mesa de trabajo no está disponible, la biblioteca tvOS AccessEnabler utiliza NsUserDefaults como opción de almacenamiento. Esto resuelve el problema de la autenticación persistente y los tokens de autorización, pero la información almacenada no se puede compartir entre distintas aplicaciones.

 

**Cambios en el tablero de iOS 10 -** Al actualizar desde una versión anterior de iOS, se borra la mesa de trabajo. Esto significa que todas las aplicaciones deben volver a autenticarse.

 

**Cambios en el tablero de iOS 7:** Debido a los cambios en el funcionamiento de los paneles en iOS 7, habrá un SSO cruzado limitado entre las aplicaciones que se ejecuten en iOS 7. Aplicaciones que tienen la misma `<Bundle Seed ID>`(también conocido como `<Team ID>`) compartirá tokens, lo que significa que las aplicaciones A1 y A2 del mismo programador X compartirán tokens, mientras que la aplicación A1 (programador X) y la aplicación A3 (programador Y) no compartirán tokens. 

- El ID de origen del paquete/ID del equipo es el mismo entre dos aplicaciones si las genera el mismo perfil de aprovisionamiento. Para obtener más información, consulte este vínculo:
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- Esta limitación de &quot;SSO cruzado&quot; estará presente en iOS 7 independientemente del SDK de autenticación de Primetime utilizado. 

Lea esta nota técnica para obtener más información sobre la configuración de SSO en iOS 7 y superiores (la nota técnica se aplica a Access Enabler v1.8 y superiores): <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### Almacenamiento de tokens (AccessEnabler 1.7)

A partir de AccessEnabler 1.7, el almacenamiento de tokens puede admitir varias combinaciones Programador-MVPD, basadas en una estructura de mapas anidada de múltiples niveles que puede contener varios tokens de autenticación. Este nuevo almacenamiento no afecta a la API pública de AccessEnabler de ninguna manera y no requiere cambios por parte del programador. Este es un ejemplo que ilustra esta nueva funcionalidad:

1. Abra App1 (desarrollado por Programmer1).
1. Autentíquese con MVPD1 (que está integrado con Programmer1).
1. Suspender / Cerrar la aplicación actual y abrir App2 (desarrollado por Programmer2).
1. Supongamos que Programmer2 no está integrado con MVPD2; por lo tanto, el usuario NO se autenticará en App2.
1. Autentíquese con MVPD2 (que está integrado con Programmer2) en App2.
1. Vuelva a la aplicación 1; el usuario seguirá estando autenticado con el programador 1.

En versiones anteriores de AccessEnabler, el paso 6 representaba al usuario como no autenticado, ya que el almacenamiento de tokens anteriormente solo admitía un token de autenticación.

 

Al cerrar sesión desde una sesión de Programador / MVPD, se borrará todo el almacenamiento subyacente, incluidos todos los demás tokens de autenticación de Programador / MVPD del dispositivo. Por otro lado, cancelar el flujo de autenticación (invocando [`setSelectedProvider(null)`](#setSelProv)) NO borrará el almacenamiento subyacente, pero solo afectará al actual intento de autenticación Programador / MVPD (borrando el MVPD para el programador actual).

 

### Importador de tokens (AccessEnabler 1.7)

Otra función relacionada con el almacenamiento de información que se incluye en AccessEnabler 1.7 permite importar tokens de autenticación de áreas de almacenamiento antiguas. Este &quot;Importador de tokens&quot; ayuda a lograr la compatibilidad entre versiones consecutivas de AccessEnabler, manteniendo el estado SSO incluso cuando se actualiza la versión de almacenamiento. El importador se ejecuta durante el [`setRequestor()`](#setReq) y se ejecuta en los dos escenarios siguientes (suponiendo que no haya un token de autenticación válido para el programador actual en el almacenamiento actual):

- La primera instalación de una aplicación 1.7 desarrollada por un programador específico
- Ruta de actualización a un AccessEnabler futuro que utiliza un nuevo almacenamiento de información

La operación de importación es transparente para el programador y no requiere ningún cambio de código en la aplicación cliente.

 

### Token Sanitizer (AccessEnabler 1.7.5)

A partir de AccessEnabler 1.7.5, este servicio se ejecuta en [`setRequestor()`](#setReq)`. `Se desarrolló como resultado del cambio de iOS 7 de la dirección WiFi MAC al IDFA para el seguimiento. El anidador garantiza que el almacenamiento actual contenga únicamente tokens de autenticación válidos (válidos en términos del ID del dispositivo, antes calculado mediante la dirección de MAC, antes de iOS7). El autenticador de tokens elimina todos los tokens no válidos. 

 

El servicio Token Sanitizer es más útil cuando se utiliza una aplicación AccessEnabler 1.7.5 en iOS 6 y el usuario actualiza a iOS 7. Cuando esto sucede, todos los tokens de autenticación obtenidos en iOS 6 no serán válidos (debido al algoritmo de ID de dispositivo, pasa de utilizar la dirección de MAC al IDFA). El desinfectante borrará todos los tokens no válidos y el usuario no se autenticará. 

 

Sin el token Sanitizer eliminando tokens no válidos, AccessEnabler no obtendría autorizaciones debido a la presencia de tokens de autenticación no válidos. Esto resultaría difícil para el usuario final de depurar, ya que los mensajes de error de autorización pueden ser crípticos y no ser demasiado útiles para determinar qué causó el problema. 

 

### Formato {#format}

- [Token AuthN](#authn_token)
- [Token de AuthZ](#authz_token)
- [Token de medio corto](#short_token)
- [Enlace de dispositivos](#device_binding)


Tenga en cuenta que el formato de los tokens AuthN y AuthZ se incluye aquí solo para información de fondo. La estructura de estos tokens se puede cambiar mediante la autenticación de Primetime en cualquier momento. Los programadores no necesitan saber la estructura exacta de los tokens AuthN y AuthZ para implementar sus aplicaciones, ya que los tokens AuthN y AuthZ no están expuestos en el dispositivo local. Token de medios cortos *es* expuesto a la aplicación del programador.

 

#### Token de autenticación {#authn_token}

La lista siguiente presenta el formato del token de autenticación:

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthenticationToken>
      <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
      <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>   
  </simpleAuthenticationToken>
```
 

#### Token de autorización {#authz_token}

La lista siguiente presenta el formato del token de autorización:

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthorizationToken>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
      <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>
  </simpleAuthorizationToken>
```
 

#### Token de medio corto {#short_token}

El listado siguiente presenta el formato del token de medio corto. Este token está expuesto a la aplicación del programador. Se transmite a la aplicación del programador al final de un proceso exitoso de asignación de derechos:

```
  <signatureInfo>signature<signatureInfo>
  <shortAuthorizationToken>
    <sessionGUID>session_guid</sessionGUID>
    <requestorID>requestor_id</requestorID>
    <resourceID>resource_id</resourceID>
    <ttl>ttl_in_ms</ttl>
    <issueTime>issue_time</issueTime>
    <mvpdId>mvpd_id</mvpdId>
    <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
  </shortAuthorizationToken>
```
 

### Enlace de dispositivos {#device_binding}

En las listas XML anteriores, observe la etiqueta titulada `simpleTokenFingerprint`. El propósito de esta etiqueta es albergar información nativa sobre la individualización del ID del dispositivo. La biblioteca AccessEnabler puede obtener dicha información de personalización y ponerla a disposición de los servicios de autenticación de Primetime durante las llamadas de asignación de derechos. El servicio utilizará esta información e la integrará en los tokens reales, lo que vinculará efectivamente los tokens a un dispositivo específico. El objetivo final de esto es hacer que los tokens no se puedan transferir entre dispositivos.

 

Como esta es obviamente una característica relacionada con la seguridad, esta información es inherentemente &quot;sensible&quot; desde el punto de vista de la seguridad. Como resultado, esta información debe protegerse tanto de la manipulación como de la escucha. El problema de la escucha se resuelve enviando las solicitudes de autenticación/autorización a través del protocolo HTTPS. La protección de manipulación se gestiona mediante la firma digital de la información de identificación del dispositivo. La biblioteca AccessEnabler calcula un ID de dispositivo a partir de la información proporcionada por el dispositivo y, a continuación, envía el ID de dispositivo &quot;en blanco&quot; a los servidores de autenticación de Primetime como parámetro de solicitud. Los servidores de autenticación de Primetime firman digitalmente el ID del dispositivo con la clave privada de Adobe y lo añaden al token de autenticación devuelto a AccessEnabler. Por lo tanto, el ID del dispositivo está enlazado con el token de autenticación. Durante el flujo de autorización, AccessEnabler vuelve a enviar el ID del dispositivo en la etiqueta clear, junto con el token de autenticación. El fallo del proceso de validación provocará automáticamente un error en los flujos de trabajo de autenticación/autorización. Los servidores de autenticación de Primetime aplican la clave privada al ID del dispositivo y la comparan con el valor del token de autenticación. Si no coinciden, el flujo de asignación de derechos falla.

 

**Nota sobre el enlace de dispositivos en AccessEnabler 1.7.5:** A partir de AccessEnabler 1.7.5, existe un cambio en la forma en que se calcula el ID del dispositivo para proporcionar información de personalización para un dispositivo iOS. Este cambio refleja un cambio en iOS 7: A partir de iOS 7, Apple ya no proporciona la dirección WiFi MAC como opción de seguimiento, en favor de su identificador para anunciantes (IDFA). Dado que la información de personalización de una aplicación que se ejecuta en iOS 7 se basa en el IDFA y que dicha información está incrustada en los tokens de flujo de derechos, esto significa que hay una serie de posibles efectos diferentes en la experiencia del usuario que resultan de este cambio. Los diferentes efectos posibles se basan en la versión de iOS que el usuario está actualizando en combinación con la versión de AccessEnabler desde la que el programador está actualizando. Para obtener más información sobre este cambio, consulte las notas de la versión incluidas en el SDK 1.7.5 de AccessEnabler.

<!--
## Related Information {#related}


- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Primetime authentication Access
  Enabler](#)
-->
