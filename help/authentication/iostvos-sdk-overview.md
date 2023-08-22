---
title: Información general del SDK para iOS/tvOS
description: Información general del SDK para iOS/tvOS
exl-id: b02a6234-d763-46c0-bc69-9cfd65917a19
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '3691'
ht-degree: 0%

---

# Información general del SDK para iOS/tvOS {#iostvos-sdk-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.


</br>


## Introducción {#intro}

iOS AccessEnabler es una biblioteca iOS/tvOS de Objective-C que permite a las aplicaciones móviles utilizar la autenticación de Adobe Primetime para los servicios de asignación de derechos de TV Everywhere. La implementación consiste en lo siguiente *AccessEnabler* que define la API de derechos y la variable *EntitlementDelegate* y *[EntitlementStatus](#ios%20entitlement%20status)* que describe las llamadas de retorno que la biblioteca almacena en déclencheur. Se hace referencia a la interfaz junto con el protocolo con un nombre común: la biblioteca AccessEnabler.

## Requisitos de iOS y tvOS {#reqs}

Para conocer los requisitos técnicos actuales relacionados con la plataforma iOS y tvOS y la autenticación de Primetime, consulte [Requisitos de plataforma/dispositivo/herramienta](#ios)y consulte las notas de la versión incluidas con la descarga del SDK. En el resto de esta página, verá secciones que indican cambios que se aplican a versiones de SDK particulares y posteriores. Por ejemplo, la siguiente es una nota legítima sobre el SDK 1.7.5:

## Explicación de los flujos de trabajo de cliente nativos {#flows}

Los flujos de trabajo de cliente nativos suelen ser iguales o muy similares a los de los clientes de autenticación de Primetime basados en explorador. Sin embargo, hay algunas excepciones, como se describe a continuación.

- [Flujo de trabajo posterior a la inicialización](#post-init)
- [Flujo de trabajo de autenticación inicial genérica](#generic)
- [Flujo de trabajo de cierre](#logout)


### Flujo de trabajo posterior a la inicialización {#post-init}

Todos los flujos de trabajo de derechos admitidos por AccessEnabler suponen que ha llamado anteriormente a [`setRequestor()`](#setReq) para establecer su identidad. Esta llamada se realiza para proporcionar el ID de solicitante solo una vez, normalmente durante la fase de inicialización/configuración de la aplicación.


Con un cliente nativo de iOS, después de la llamada inicial a [`setRequestor()`](#setReq), tiene la opción de cómo proceder:

- Puede empezar a realizar llamadas de asignación de derechos inmediatamente y permitir que se pongan en cola silenciosamente, si es necesario.

- Puede recibir una confirmación del éxito/fracaso de [`setRequestor()`](#setReq) mediante la implementación de [`setRequestorComplete()`](#setReqComplete) devolución de llamada.

- Puede realizar las dos acciones anteriores.

Usted elige que su aplicación espere a que se notifique el éxito de [`setRequestor()`](#setReq) o haga que dependa del mecanismo de cola de llamadas de AccessEnabler. Dado que todas las solicitudes de autorización y autenticación subsiguientes necesitan el ID del solicitante y la información de configuración asociada, la variable [`setRequestor()`](#setReq) bloquea de forma efectiva todas las llamadas de API de autenticación y autorización hasta que se complete la inicialización.



### Flujo de trabajo de autenticación inicial genérica {#generic}

El propósito de este flujo de trabajo es iniciar sesión en un usuario con su MVPD. Después de un inicio de sesión correcto, el servidor back-end emite al usuario un token de autenticación. Aunque la autenticación se suele realizar como parte del proceso de autorización, a continuación se describe cómo puede funcionar la autenticación de forma aislada y no se incluye ningún paso de autorización.

Tenga en cuenta que, aunque este flujo de trabajo difiere para los clientes nativos del flujo de trabajo de autenticación basado en explorador habitual, los pasos del 1 al 5 son los mismos para los clientes nativos y los basados en explorador.

1. La aplicación inicia el flujo de trabajo de autenticación con una llamada al `getAuthentication() `Método de API, que comprueba si hay un token de autenticación en caché válido.
1. Si el usuario está autenticado actualmente, AccessEnabler llama a su [`setAuthenticationStatus()`](#setAuthNStatus) función de llamada de retorno, pasando un estado de autenticación que indica éxito y finalizando el flujo.
1. Si el usuario no está autenticado actualmente, AccessEnabler continúa el flujo de autenticación determinando si el último intento de autenticación del usuario se realizó correctamente con una MVPD determinada. Si se almacena en caché un ID de MVPD Y la variable `canAuthenticate` el indicador es verdadero O se seleccionó una MVPD usando [`setSelectedProvider()`](#setSelProv)Sin embargo, no se le pide al usuario el cuadro de diálogo de selección de MVPD. El flujo de autenticación sigue utilizando el valor almacenado en caché de la MVPD (es decir, la misma MVPD que se utilizó durante la última autenticación correcta). Se realiza una llamada de red al servidor back-end y se redirige al usuario a la página de inicio de sesión de MVPD (paso 6 a continuación).
1. Si no se almacena en caché ningún ID de MVPD Y no se seleccionó ninguna MVPD usando [`setSelectedProvider()`](#setSelProv) O el `canAuthenticate` Si el indicador se establece en false, la variable [`displayProviderDialog()`](#dispProvDialog) se llama a la devolución de llamada. Esta llamada de retorno indica a la aplicación que cree la interfaz de usuario que presenta al usuario una lista de MVPD para elegir. Se proporciona una matriz de objetos MVPD, que contiene la información necesaria para crear el selector MVPD. Cada objeto MVPD describe una entidad MVPD y contiene información como el ID de la MVPD (por ejemplo, XFINITY, AT\&amp;T, etc.) y la URL donde se puede encontrar el logotipo de MVPD.
1. Una vez que se selecciona una MVPD en particular, la aplicación debe informar al AccessEnabler de la elección del usuario. Una vez que el usuario selecciona la MVPD deseada, se informa al AccessEnabler de la selección del usuario mediante una llamada a [`setSelectedProvider()`](#setSelProv) método.
1. IOS AccessEnabler llama a su `navigateToUrl:` callback o `navigateToUrl:useSVC:` para redirigir al usuario a la página de inicio de sesión de MVPD. Al activar cualquiera de ellas, AccessEnabler realiza una solicitud a la aplicación para crear un `UIWebView/WKWebView or SFSafariViewController` y para cargar la dirección URL proporcionada en el `url` parámetro. Dirección URL del extremo de autenticación en el servidor back-end. Para tvOS AccessEnabler, la variable [status()](#status_callback_implementation) la llamada de retorno se llama con un `statusDictionary` y el sondeo para la segunda autenticación de pantalla se inicia inmediatamente. El `statusDictionary` contiene el `registration code` que debe utilizarse para la segunda autenticación de pantalla.
1. En el caso del AccessEnabler de iOS, el usuario aterriza en la página de inicio de sesión de la MVPD para introducir sus credenciales a través del medio de la aplicación `UIWebView/WKWebView or SFSafariViewController `controlador. Tenga en cuenta que durante esta transferencia se producen varias operaciones de redireccionamiento y la aplicación debe supervisar las direcciones URL que carga el controlador durante las diversas operaciones de redireccionamiento.
1. En el caso del iOS AccessEnabler, cuando la variable `UIWebView/WKWebView or SFSafariViewController` El controlador carga una dirección URL personalizada específica. La aplicación debe cerrar el controlador y llamar al servicio AccessEnabler. `handleExternalURL:url `Método de API. Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue. Su aplicación debe interpretarlo únicamente como una señal de que el flujo de autenticación se ha completado y de que es seguro cerrar el `UIWebView/WKWebView or SFSafariViewController` controlador. En caso de que la aplicación deba utilizar un `SFSafariViewController `la dirección URL personalizada específica está definida por el `application's custom scheme` (p. ej., `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta dirección URL personalizada específica se define mediante `ADOBEPASS_REDIRECT_URL` constante (es decir, `adobepass://ios.app`).
1. Una vez que la aplicación se cierre, `UIWebView/WKWebView or SFSafariViewController` controlador y llamadas a AccessEnabler `handleExternalURL:url `método de API, AccessEnabler recupera el token de autenticación del servidor back-end e informa a la aplicación de que el flujo de autenticación ha finalizado. AccessEnabler llama al método [`setAuthenticationStatus()`](#setAuthNStatus) llamada de retorno con un código de estado de 1, que indica que se ha realizado correctamente. Si se produce un error durante la ejecución de estos pasos, la variable [`setAuthenticationStatus()`](#setAuthNStatus) la llamada de retorno se activa con un código de estado de 0, que indica un error de autenticación, así como un código de error correspondiente.


>[!WARNING]
>
> Durante los pasos en los que AccessEnabler cede el control a la aplicación (es decir, cuando se muestra el cuadro de diálogo de selección del proveedor o cuando se muestra UIWebView/WKWebView o SFSafariViewController), el usuario tiene la oportunidad de cancelar el flujo de autenticación. En estas situaciones, la aplicación es responsable de informar a AccessEnabler acerca de este evento y de llamar a [`setSelectedProvider()`](#setSelProv) método de API, pasando nulo como parámetro. Esto ofrece al AccessEnabler la oportunidad de limpiar su estado interno y restablecer el flujo de autenticación. En tvOS, puede utilizar el mismo método para cancelar el sondeo de autenticación.


### Flujo de trabajo de cierre {#logout}

Para los clientes nativos, el cierre de sesión se gestiona de manera similar al proceso de autenticación descrito anteriormente.

1. La aplicación inicia el flujo de trabajo de cierre de sesión con una llamada al `logout() `Método de API. El cierre de sesión es el resultado de una serie de operaciones de redirección HTTP debido al hecho de que el usuario debe cerrar la sesión tanto desde los servidores de autenticación de Primetime como desde los servidores de MVPD. Dado que este flujo no se puede completar con una simple solicitud HTTP emitida por la biblioteca AccessEnabler, `UIWebView/WKWebView or SFSafariViewController` debe crearse una instancia del controlador para poder seguir las operaciones de redirección HTTP.

1. Se utiliza un patrón similar al flujo de autenticación. El iOS AccessEnabler almacena en déclencheur `navigateToUrl:` devolución de llamada o `navigateToUrl:useSVC:` para crear un `UIWebView/WKWebView or SFSafariViewController` y para cargar la dirección URL proporcionada en el `url` parámetro. Dirección URL del extremo de cierre de sesión en el servidor back-end. Para el AccessEnabler de tvOS, ni la variable `navigateToUrl:` devolución de llamada o `navigateToUrl:useSVC:` se llama a la devolución de llamada.

1. A medida que pasa por varias redirecciones, la aplicación debe monitorizar la actividad del `UIWebView/WKWebView or SFSafariViewController `y detectar el momento en que carga una dirección URL personalizada específica. Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue. Su aplicación debe interpretarlo únicamente como una señal de que el flujo de cierre de sesión se ha completado y de que es seguro cerrar el controlador. Cuando el controlador carga esta dirección URL personalizada específica, la aplicación debe cerrar el controlador y llamar al servicio AccessEnabler `handleExternalURL:url `Método de API. En caso de que la aplicación deba utilizar un `SFSafariViewController `la dirección URL personalizada específica está definida por el `application's custom scheme` (p. ej.,`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta dirección URL personalizada específica se define mediante ` ADOBEPASS_REDIRECT_URL  `constante (es decir, `adobepass://ios.app`).

1. Al final, AccessEnabler llama al método [`setAuthenticationStatus()`](#setAuthNStatus) llamada de retorno con un código de estado de 0, que indica que el flujo de cierre de sesión se ha realizado correctamente.

El flujo de cierre de sesión difiere del flujo de autenticación en que el usuario no tiene que interactuar con el `UIWebView/WKWebView or SFSafariViewController`  controlador de cualquier manera. Por lo tanto, Adobe recomienda hacer que el control sea invisible (es decir, oculto) durante el proceso de cierre de sesión.

## Tokens {#tokens}

- [Definiciones y uso](#definitions)
- [Directrices de almacenamiento en caché](#caching)
- [Persistencia](#persistence)
- [Formato](#format)
- [Enlace de dispositivo](#device_binding)


### Definiciones y uso {#definitions}

La solución de asignación de derechos de autenticación de Primetime gira en torno a la generación de fragmentos de datos específicos (tokens) que la autenticación de Primetime genera al finalizar correctamente los flujos de trabajo de autenticación y autorización. Estos tokens se almacenan localmente en el dispositivo iOS del cliente.



Los tokens tienen una duración limitada; tras la caducidad, los tokens deben volver a emitirse reiniciando los flujos de trabajo de autenticación o autorización.



Existen tres tipos de tokens emitidos durante los flujos de trabajo de asignación de derechos:

- **Token de autenticación:** El resultado final del flujo de trabajo de autenticación de usuarios será un GUID de autenticación que AccessEnabler puede utilizar para realizar consultas de autorización en nombre del usuario. Este GUID de autenticación tendrá asociado un valor de tiempo de vida (TTL) que puede diferir de la sesión de autenticación del usuario. Se generará un token de autenticación enlazando el GUID de autenticación al dispositivo que inicia las solicitudes de autenticación.
- **Token de autorización:** Otorga acceso a un recurso protegido específico identificado por un resourceID único. Consiste en una concesión de autorización emitida por la parte que autoriza junto con el ID de recurso original. Esta información está enlazada al dispositivo que inicia la solicitud.
- **Token de medios de corta duración:** AccessEnabler concede acceso a la aplicación de alojamiento para un recurso determinado devolviendo un token multimedia de corta duración. Este token se genera en función del token de autorización adquirido anteriormente para ese recurso en particular. Además, este token no está enlazado al dispositivo y la duración asociada es considerablemente más corta (valor predeterminado: 5 minutos).

Una vez que la autenticación y la autorización se hayan realizado correctamente, la autenticación de Primetime emitirá tokens de autenticación, autorización y medios de corta duración. Estos tokens deben almacenarse en caché en el dispositivo del usuario y utilizarse durante la duración de sus CICLOS de vida asociados.



### Directrices de almacenamiento en caché {#caching}

- Testigo de autenticación
- Token de autorización
- Token de medios de corta duración


#### Testigo de autenticación

- **AccessEnabler 1.7:** Este SDK introduce un nuevo método de almacenamiento de tokens, que permite varios contenedores de MVPD de programador y, por lo tanto, varios tokens de autenticación. Ahora se utiliza el mismo diseño de almacenamiento tanto para el escenario &quot;Autenticación por solicitante&quot; como para el flujo de autenticación normal. La única diferencia entre los dos es la forma en que se realiza la autenticación: &quot;Autenticación por solicitante&quot; contiene una nueva mejora (Autenticación pasiva) que permite que AccessEnabler realice la autenticación de canal de retorno, basada en la existencia de un token de autenticación en el almacenamiento (para un programador diferente). El usuario solo tiene que autenticarse una vez, y esta sesión se utilizará para obtener tokens de autenticación en aplicaciones adicionales. Este flujo de canal posterior tiene lugar durante el [`setRequestor()`](#setReq) llama a y es mayormente transparente para el programador. **Sin embargo, hay un requisito importante en este caso: el programador DEBE llamar a setRequestor() desde el subproceso de la interfaz de usuario principal.**
- **AccessEnabler 1.6 y versiones posteriores:** La forma en que se almacenan en caché los tokens de autenticación en el dispositivo depende de &quot;**Autenticación por solicitante&quot;** Indicador asociado con la MVPD actual:

<!-- end list -->

1. Si la función &quot;Autenticación por solicitante&quot; está deshabilitada, se almacenará un único token de autenticación localmente en la mesa de trabajo global; este token se compartirá entre todas las aplicaciones que estén integradas con la MVPD actual.
1. Si la función &quot;Autenticación por solicitante&quot; está habilitada, se asociará explícitamente un token con el programador que realizó el flujo de autenticación (el token no se almacenará en la mesa de trabajo global, sino en un archivo privado visible solo para la aplicación de ese programador). Más específicamente, se deshabilitará el inicio de sesión único (SSO) entre diferentes aplicaciones; el usuario deberá realizar el flujo de autenticación explícitamente al cambiar a una nueva aplicación (siempre que el programador de la segunda aplicación esté integrado con la MVPD actual y que no exista ningún token de autenticación para ese programador en la caché local).



#### Token de autorización

En cualquier momento dado, AccessEnabler almacena en caché solo UN token de autorización por recurso. Puede haber varios tokens de autorización en la caché, pero están asociados a diferentes recursos. Siempre que se emita un nuevo token de autorización y ya exista uno antiguo para *el mismo recurso*, el nuevo token sobrescribe el valor almacenado en caché existente.



#### Token de medios

El token de medios de corta duración NO debe almacenarse en caché. El token de medios debe recuperarse del servidor cada vez que se llama a una API de autorización, ya que está restringido a un solo uso.



### Persistencia {#persistence}

Los tokens deben ser persistentes en ejecuciones consecutivas de la misma aplicación. Esto significa que una vez que se han adquirido los tokens de autenticación y autorización y el usuario cierra la aplicación, los mismos tokens están disponibles para la aplicación cuando el usuario vuelve a abrir la aplicación. Además, es deseable que estos tokens sean persistentes en varias aplicaciones. En otras palabras, después de que un usuario utilice una aplicación para iniciar sesión con un proveedor de identidad específico (obteniendo correctamente tokens de autenticación y autorización), los mismos tokens se pueden utilizar a través de una aplicación diferente y ya no se le piden credenciales al usuario al iniciar sesión a través del mismo proveedor de identidad. Este tipo de flujo de trabajo de autenticación/autorización sin problemas es lo que hace que la solución de autenticación de Primetime sea una verdadera implementación de TV en todas partes.



## iOS

La biblioteca iOS AccessEnabler soluciona los problemas del uso compartido de datos entre aplicaciones almacenando los datos de tokens en una estructura de datos &quot;similar a un portapapeles&quot; denominada *pegar tablero*. Este recurso compartido de nivel de sistema proporciona los ingredientes clave que permiten la implementación del caso de uso de tokens persistentes deseado:

- **Compatibilidad con el almacenamiento estructurado** - La placa de pegado no es sólo una estructura de memoria simple, lineal, tipo buffer. Proporciona un mecanismo de almacenamiento similar a un diccionario que permite la indexación de datos en función de los valores de clave especificados por el usuario.
- **Compatibilidad con la persistencia de datos mediante el sistema de archivos subyacente** - El contenido de la estructura del panel de pegado puede marcarse como persistente, en cuyo caso los datos se guardan en la memoria interna del dispositivo.



Una vez que un token particular se coloca en la caché de tokens, la biblioteca AccessEnabler comprueba su validez en diferentes momentos.  Un token válido se define como:

- El TTL del token no ha caducado.
- El emisor del token se incluye en la lista de proveedores de identidad permitidos.



## tvOS

Como en tvOS la mesa de trabajo no está disponible, la biblioteca de tvOS AccessEnabler utiliza NsUserDefaults como opción de almacenamiento. Esto soluciona el problema de la autenticación persistente y los tokens de autorización, pero la información almacenada no se puede compartir entre distintas aplicaciones.



**Cambios en la mesa de trabajo de iOS 10 -** Al actualizar desde una versión anterior de iOS, la mesa de trabajo se borrará. Esto significa que todas las aplicaciones deben volver a autenticarse.



**Cambios en la mesa de trabajo de iOS 7 -** Debido a los cambios en el funcionamiento de los paneles de trabajo en iOS 7, habrá un SSO cruzado limitado entre las aplicaciones que se ejecutan en iOS 7. Aplicaciones que tienen el mismo `<Bundle Seed ID>`(también conocido como `<Team ID>`) compartirá tokens, lo que significa que las aplicaciones A1 y A2 del mismo programador X compartirán tokens, mientras que la aplicación A1 (programador X) y la aplicación A3 (programador Y) no compartirán tokens.

- El ID de raíz del paquete/ID del equipo es el mismo entre dos aplicaciones si las genera el mismo perfil de aprovisionamiento. Encontrará más información en este enlace:
  [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- Esta limitación de &quot;SSO cruzado&quot; estará presente en iOS 7 independientemente del SDK de autenticación de Primetime utilizado.

Lea esta nota técnica para obtener más información sobre la configuración de SSO en iOS 7 y versiones posteriores (la nota técnica se aplica a Access Enabler v1.8 y versiones posteriores): <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>



### Almacenamiento de tokens (AccessEnabler 1.7)

A partir de AccessEnabler 1.7, el almacenamiento de tokens puede admitir varias combinaciones de programador-MVPD, basándose en una estructura de mapas anidada de varios niveles que puede contener varios tokens de autenticación. Este nuevo almacenamiento no afecta a la API pública de AccessEnabler de ninguna manera y no requiere cambios por parte del programador. Este es un ejemplo que ilustra esta nueva funcionalidad:

1. Abra App1 (desarrollado por Programmer1).
1. Autenticar con MVPD1 (que está integrado con Programmer1).
1. Suspenda/cierre la aplicación actual y abra App2 (desarrollada por Programmer2).
1. Supongamos que Programmer2 no está integrado con MVPD2; por lo tanto, el usuario NO será autenticado en App2.
1. Autentique con MVPD2 (que está integrado con Programmer2) en App2.
1. Cambie a App1; el usuario se autenticará con Programmer1.

En versiones anteriores de AccessEnabler, el paso 6 hacía que el usuario no estuviera autenticado, ya que el almacenamiento de tokens anteriormente solo admitía un token de autenticación.



Si se cierra la sesión de un programador/MVPD, se borrará todo el almacenamiento subyacente, incluidos todos los demás tokens de autenticación de programador/MVPD del dispositivo. Por otro lado, cancelar el flujo de autenticación (invocando a [`setSelectedProvider(null)`](#setSelProv)) NO borrará el almacenamiento subyacente, pero solo afectará el intento actual de autenticación de Programador / MVPD (borrando la MVPD para el Programador actual).



### Importador de tokens (AccessEnabler 1.7)

Otra función relacionada con el almacenamiento que se incluye en AccessEnabler 1.7 permite importar tokens de autenticación de áreas de almacenamiento antiguas. Este &quot;Importador de tokens&quot; ayuda a lograr la compatibilidad entre versiones consecutivas de AccessEnabler, manteniendo el estado de SSO incluso cuando se actualiza la versión de almacenamiento. El importador se ejecuta durante el [`setRequestor()`](#setReq) y se ejecuta en los dos casos siguientes (suponiendo que no hay ningún token de autenticación válido para el programador actual en el almacenamiento actual):

- La primera instalación de una aplicación 1.7 desarrollada por un programador específico
- Ruta de actualización a un futuro AccessEnabler que utilice un nuevo almacenamiento

La operación de importación es transparente para el programador y no requiere ningún cambio de código en la aplicación cliente.



### Eliminador de tokens (AccessEnabler 1.7.5)

A partir de AccessEnabler 1.7.5, este servicio se ejecuta en [`setRequestor()`](#setReq)`. `Se desarrolló como resultado del cambio de iOS 7 de la dirección MAC de WiFi al IDFA para seguimiento. El desinfectante garantiza que el almacenamiento actual contenga únicamente tokens de autenticación válidos (válidos en términos del ID de dispositivo, anteriormente calculados mediante la dirección MAC, antes de iOS7). El eliminador de tokens elimina todos los tokens no válidos.



El servicio Token Sanitizer es más útil cuando se utiliza una aplicación AccessEnabler 1.7.5 en iOS 6 y el usuario actualiza a iOS 7. Cuando esto sucede, todos los tokens de autenticación obtenidos en iOS 6 ahora no son válidos (debido al cambio del algoritmo de ID de dispositivo de usar la dirección de MAC a IDFA). El desinfectador borrará todos los tokens no válidos y el usuario no se autenticará.



Sin el eliminador de tokens que elimine los tokens no válidos, AccessEnabler no obtendría autorizaciones debido a la presencia de tokens de autenticación no válidos. Esto resultaría difícil de depurar para el usuario final, ya que los mensajes de error de autorización pueden ser crípticos y no demasiado útiles para determinar la causa del problema.



### Formato {#format}

- [Token de AuthN](#authn_token)
- [Token de AuthZ](#authz_token)
- [Token de medios corto](#short_token)
- [Enlace de dispositivo](#device_binding)


Tenga en cuenta que el formato de los tokens AuthN y AuthZ se incluye aquí solo para obtener información general. La estructura de estos tokens se puede cambiar mediante la autenticación de Primetime en cualquier momento. Los programadores no necesitan conocer la estructura exacta de los tokens AuthN y AuthZ para implementar sus aplicaciones, ya que los tokens AuthN y AuthZ no se exponen en el dispositivo local. El token de medios cortos *es* expuesto a la aplicación del programador.



#### Testigo de autenticación {#authn_token}

La siguiente lista presenta el formato del token de autenticación:

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

La siguiente lista presenta el formato del token de autorización:

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


#### Token de medios corto {#short_token}

La siguiente lista presenta el formato del token de medios corto. Este token se expone a la aplicación del programador. Se pasa a la aplicación del programador al final de un proceso de asignación de derechos correcto:

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


### Enlace de dispositivo {#device_binding}

En los listados XML anteriores, observe la etiqueta titulada `simpleTokenFingerprint`. El propósito de esta etiqueta es contener información de individualización de ID de dispositivo nativo. La biblioteca AccessEnabler puede obtener dicha información de individualización y ponerla a disposición de los servicios de autenticación de Primetime durante las llamadas de asignación de derechos. El servicio utilizará esta información e la incrustará en los tokens reales, enlazando así de forma eficaz los tokens a un dispositivo específico. El objetivo final de esto es hacer que los tokens sean intransferibles entre dispositivos.



Dado que esta es, obviamente, una función relacionada con la seguridad, esta información es inherentemente &quot;confidencial&quot; desde el punto de vista de la seguridad. Como resultado, esta información debe protegerse contra la manipulación y la escucha. El problema de la escucha se resuelve enviando las solicitudes de autenticación/autorización a través del protocolo HTTPS. La protección contra la manipulación se controla mediante la firma digital de la información de identificación del dispositivo. La biblioteca AccessEnabler calcula un ID de dispositivo a partir de la información proporcionada por el dispositivo y, a continuación, envía el ID de dispositivo &quot;sin cifrar&quot; a los servidores de autenticación de Primetime como parámetro de solicitud. Los servidores de autenticación de Primetime firman digitalmente el ID de dispositivo con la clave privada de Adobe y lo agregan al token de autenticación que se devuelve al AccessEnabler. Por lo tanto, el ID del dispositivo está enlazado con el token de autenticación. Durante el flujo de autorización, AccessEnabler vuelve a enviar el ID del dispositivo de forma clara, junto con el token de autenticación. Un error en el proceso de validación provocará automáticamente un error en los flujos de trabajo de autenticación/autorización. Los servidores de autenticación de Primetime aplican la clave privada al ID de dispositivo y la comparan con el valor del token de autenticación. Si no coinciden, se produce un error en el flujo de derechos.



**Nota sobre el enlace de dispositivos en AccessEnabler 1.7.5:** A partir de AccessEnabler 1.7.5, se produce un cambio en la forma de calcular el ID del dispositivo para proporcionar información de individualización para un dispositivo iOS. Este cambio refleja un cambio en iOS 7: a partir de iOS 7, Apple ya no proporciona la dirección de WiFi MAC como opción de seguimiento, a favor de su identificador para anunciantes (IDFA). Dado que la información de individualización de una aplicación que se ejecuta en iOS 7 se basa en el IDFA y que esa información está incrustada en los tokens de flujo de derechos, esto significa que hay una serie de posibles efectos diferentes en la experiencia del usuario que resultan de este cambio. Los diferentes efectos posibles se basan en la versión de iOS desde la que el usuario está actualizando, junto con la versión del AccessEnabler desde la que el programador está actualizando. Para obtener más información sobre este cambio, consulte las Notas de la versión incluidas con el SDK 1.7.5 de AccessEnabler.

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
