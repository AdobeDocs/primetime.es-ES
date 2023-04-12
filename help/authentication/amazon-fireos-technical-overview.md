---
title: Información general técnica de Amazon FireOS
description: Información general técnica de Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 0%

---


# Información general técnica de Amazon FireOS {#amazon-fireos-technical-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Introducción {#intro}

Amazon FireOS AccessEnabler está representado por dos componentes: una biblioteca stub de AccessEnabler utilizada por la aplicación y una biblioteca Android de Java a nivel de sistema que permite que las aplicaciones móviles utilicen la autenticación de Adobe Primetime para los servicios de asignación de derechos de TV Everywhere. Una implementación de Android para Amazon FireOS consiste en la interfaz de AccessEnabler que define la API de asignación de derechos y un protocolo EntitlementDelegate que describe las devoluciones de llamadas que déclencheur la biblioteca. La biblioteca Android AccessEnabler de nivel de sistema permite el acceso a los servicios de Amazon para habilitar el inicio de sesión único a nivel de plataforma.

## Explicación de los flujos de trabajo de cliente nativos {#native_client_workflows}

Los flujos de trabajo de cliente nativos suelen ser los mismos o muy similares a los de los clientes de autenticación Primetime basados en explorador. Sin embargo, hay algunas excepciones, como se describe a continuación.


### Flujo de trabajo posterior a la inicialización {#post-init}

Todos los flujos de trabajo de derechos admitidos por AccessEnabler suponen que ha invocado anteriormente [`setRequestor()`](#setRequestor) para establecer su identidad. Esta llamada se realiza para proporcionar el ID del solicitante solo una vez, normalmente durante la fase de inicialización/configuración de la aplicación.

Con los clientes nativos (por ejemplo, AmazonFireOS), después de la llamada inicial a [`setRequestor()`](#setRequestor), tiene la opción de continuar:

- Puede empezar a realizar llamadas de asignación de derechos inmediatamente y permitir que se pongan en cola sin aviso, si es necesario.
- O bien, puede recibir una confirmación del éxito/fracaso de [`setRequestor()`](#setRequestor) implementando la llamada de retorno setRequestorComplete() .
- O bien, haga ambas cosas.

Depende de usted esperar a que se notifique el éxito de [`setRequestor()`](#setRequestor) o para confiar en el mecanismo de cola de llamadas de AccessEnabler. Dado que todas las solicitudes de autorización y autenticación posteriores necesitan el ID del solicitante y la información de configuración asociada, la variable [`setRequestor()`](#setRequestor) bloquea de forma eficaz todas las llamadas a la API de autenticación y autorización hasta que se complete la inicialización.

### Flujo de trabajo de autenticación inicial genérico {#generic}

El propósito de este flujo de trabajo es iniciar sesión en un usuario con su MVPD.  Después de un inicio de sesión correcto, el servidor back-end envía al usuario un token de autenticación. Aunque la autenticación suele realizarse como parte del proceso de autorización, lo siguiente describe cómo puede funcionar la autenticación de forma aislada y no incluye ningún paso de autorización.

Tenga en cuenta que aunque el siguiente flujo de trabajo de cliente nativo difiere del flujo de trabajo típico de autenticación basada en navegador, los pasos 1-5 son los mismos para clientes nativos y clientes basados en navegador:

1. Su página o reproductor inicia el flujo de trabajo de autenticación con una llamada a [getAuthentication()](#getAuthN), que comprueba si hay un token de autenticación en caché válido. Este método tiene una `redirectURL` parámetro; si no proporciona un valor para `redirectURL`, después de una autenticación correcta, el usuario vuelve a la dirección URL desde la que se inicializó la autenticación.
1. AccessEnabler determina el estado de autenticación actual. Si el usuario está autenticado actualmente, AccessEnabler llama a su `setAuthenticationStatus()` función de llamada de retorno, pasando un estado de autenticación que indica éxito (paso 7 a continuación).
1. Si el usuario no está autenticado, AccessEnabler continúa el flujo de autenticación determinando si el último intento de autenticación del usuario fue exitoso con un MVPD determinado. Si un ID de MVPD se almacena en caché y el `canAuthenticate` El indicador es verdadero O se ha seleccionado un MVPD mediante [`setSelectedProvider()`](#setSelectedProvider), el usuario no recibe el cuadro de diálogo de selección de MVPD. El flujo de autenticación continúa utilizando el valor almacenado en caché del MVPD (es decir, el mismo MVPD que se usó durante la última autenticación correcta). Se realiza una llamada de red al servidor back-end y se redirige al usuario a la página de inicio de sesión de MVPD (paso 6 a continuación).
1. Si no se almacena en caché ningún ID de MVPD y no se seleccionó ningún MVPD usando [`setSelectedProvider()`](#setSelectedProvider) O bien, la variable `canAuthenticate` el indicador se establece en false, la variable [`displayProviderDialog()`](#displayProviderDialog) llamada de retorno. Esta llamada de retorno dirige su página o reproductor para crear la interfaz de usuario que presenta al usuario una lista de MVPD entre los que elegir. Se proporciona una matriz de objetos MVPD que contiene la información necesaria para crear el selector de MVPD. Cada objeto MVPD describe una entidad MVPD y contiene información como el ID del MVPD (por ejemplo, XFINITY, AT\&amp;T, etc.) y la URL donde se puede encontrar el logotipo de MVPD.
1. Una vez seleccionado un MVPD concreto, su página o reproductor debe informar al AccessEnabler de la elección del usuario. Para los clientes que no son de Flash, una vez que el usuario selecciona el MVPD deseado, informará al AccessEnabler de la selección del usuario mediante una llamada a la función [`setSelectedProvider()`](#setSelectedProvider) método. Los clientes de Flash distribuyen un `MVPDEvent` de tipo &quot;`mvpdSelection`&quot;, pasando el proveedor seleccionado.
1. Para las aplicaciones de Amazon, la variable [`navigateToUrl()`](#navigagteToUrl) se ignorará la rellamada. La biblioteca Access Enabler facilita el acceso a un control WebView común para autenticar a los usuarios.
1. A través de la función `WebView`, el usuario llega a la página de inicio de sesión de MVPD e introduce sus credenciales. Tenga en cuenta que durante esta transferencia se producen varias operaciones de redireccionamiento. 
1. Una vez que WebView termine la autenticación, se cerrará e informará al AccessEnabler de que el usuario ha iniciado sesión correctamente, AccessEnabler recupera el token de autenticación real del servidor back-end. AccessEnabler llama a la función [`setAuthenticationStatus()`](#setAuthNStatus) llamada de retorno con un código de estado de 1, que indica que la llamada de retorno ha sido satisfactoria. Si hay un error durante la ejecución de estos pasos, la variable [`setAuthenticationStatus()`](#setAuthNStatus) la rellamada se activa con un código de estado de 0, junto con un código de error correspondiente, que indica que el usuario no está autenticado.

### Flujo de trabajo de cierre de sesión {#logout}

Para los clientes nativos, los cierres de sesión se gestionan de manera similar al proceso de autenticación descrito anteriormente. Siguiendo este patrón, AccessEnabler creará un `WebView` y cargará el control con la URL del extremo de cierre de sesión en el servidor back-end. Una vez completado el proceso de cierre de sesión, se borran los tokens.

Tenga en cuenta que el flujo de cierre de sesión difiere del flujo de autenticación en que no se requiere que el usuario interactúe con la variable `WebView` de cualquier manera. Una vez finalizado el cierre de sesión, AccessEnabler llama a la función `setAuthenticationStatus()` llamada de retorno con un código de estado de 0, que indica que el usuario no está autenticado.

## Tokens {#tokens}

### Definiciones y uso {#definitions}

La solución de derechos de autenticación de Primetime gira en torno a la generación de datos específicos (tokens) que la autenticación de Primetime genera al completarse correctamente los flujos de trabajo de autenticación y autorización. Estos tokens se almacenan localmente en el dispositivo Amazon FireOS del cliente.

Los tokens tienen una vida útil limitada; una vez caducado, es necesario volver a emitir los tokens mediante el reinicio de los flujos de trabajo de autenticación o autorización.

Hay tres tipos de tokens emitidos durante los flujos de trabajo de derechos:

- **Token de autenticación** - El resultado final del flujo de trabajo de autenticación de usuario será un GUID de autenticación que AccessEnabler puede utilizar para realizar consultas de autorización en nombre del usuario. Este GUID de autenticación tendrá un valor de tiempo de vida (TTL) asociado que puede ser diferente de la propia sesión de autenticación del usuario. La autenticación de Primetime genera un token de autenticación vinculando el GUID de autenticación al dispositivo que inicia las solicitudes de autenticación.
- **Token de autorización** - Otorga acceso a un recurso protegido específico identificado por una `resourceID`. Consiste en una concesión de autorización expedida por la parte autorizante junto con el original `resourceID`. Esta información está enlazada al dispositivo que inicia la solicitud.
- **Token de medio de corta duración** - AccessEnabler otorga acceso a la aplicación de alojamiento de un recurso determinado mediante la devolución de un token multimedia de corta duración. Este token se genera en función del token de autorización adquirido anteriormente para ese recurso específico. Además, este token no está enlazado al dispositivo y la duración asociada es significativamente más corta (de forma predeterminada: 5 minutos).

Tras la autenticación y autorización correctas, la autenticación de Primetime emitirá autenticación, autorización y tokens de medios de corta duración. Estos tokens deben almacenarse en caché en el dispositivo del usuario y utilizarse durante el periodo de tiempo de vida asociado.

### Directrices de almacenamiento en caché {#caching}


#### Token de autenticación

- **AccessEnabler 1.10.1 para FireOS **se basa en AccessEnabler para Android 1.9.1: Este SDK introduce un nuevo método de almacenamiento de tokens, que permite varios bloques Programmer-MVPD y, por lo tanto, varios tokens de autenticación. 

#### Token de autorización

En un momento dado, AccessEnabler solo almacena en caché UN token de autorización por recurso. Puede haber varios tokens de autorización en la caché, pero están asociados a diferentes recursos. Siempre que se emite un nuevo token de autorización y ya existe uno antiguo para el mismo recurso, el nuevo token sobrescribe el valor almacenado en caché existente.

#### Token de medio 

El token de medio de corta duración NO debe almacenarse en caché en absoluto. El token multimedia debe recuperarse del servidor cada vez que se llama a una API de autorización, ya que está restringido a un uso único.

### Persistencia {#persistence}

Los tokens deben ser persistentes en ejecuciones consecutivas de la misma aplicación. Esto significa que una vez que se han adquirido los tokens de autenticación y autorización y el usuario cierra la aplicación, los mismos tokens están disponibles para la aplicación cuando el usuario vuelve a abrir la aplicación. Además, es deseable que estos tokens sean persistentes en varias aplicaciones. En otras palabras, después de que un usuario utilice una aplicación para iniciar sesión con un proveedor de identidad específico (obteniendo correctamente la autenticación y los tokens de autorización), se pueden utilizar los mismos tokens a través de una aplicación diferente y ya no se solicita al usuario que especifique sus credenciales al iniciar sesión mediante el mismo proveedor de identidad.

Este tipo de flujo de trabajo de autenticación y autorización optimizado es lo que hace que la solución de autenticación de Primetime sea una implementación verdadera de TV en todas partes. Desde un punto de vista puramente de ingeniería, la biblioteca Android AccessEnabler trabaja en torno a los problemas del uso compartido de datos entre aplicaciones almacenando los datos token en un archivo de base de datos ubicado en un almacenamiento externo. Estos recursos compartidos a nivel de sistema proporcionan los ingredientes clave que permiten la implementación del caso de uso de tokens persistentes deseados:

- Soporte para almacenamiento estructurado: el almacenamiento del token de autenticación de Primetime no es solo una estructura de memoria lineal simple similar al búfer. Proporciona un mecanismo de almacenamiento parecido a un diccionario que permite la indexación de datos en función de los valores clave especificados por el usuario.
- Compatibilidad con la persistencia de los datos mediante el sistema de archivos subyacente : El contenido del archivo de base de datos se mantiene de forma predeterminada y los datos se guardan en la memoria externa del dispositivo.

Una vez que un token en particular se coloca en la caché de tokens, la biblioteca AccessEnabler comprueba su validez en diferentes momentos.  Un token válido se define como:

- El TTL del token no ha caducado
- El emisor del token se incluye en la lista de proveedores de identidad permitidos

El almacenamiento de tokens puede admitir varias combinaciones Programador-MVPD, basadas en una estructura de mapas anidada de varios niveles que puede contener varios tokens de autenticación. Este nuevo almacenamiento no afecta a la API pública de AccessEnabler de ninguna manera y no requiere cambios por parte del programador. Este es un ejemplo que ilustra esta funcionalidad más reciente:

1. Abra App1 (desarrollado por Programmer1).
1. Autentíquese con MVPD1 (que está integrado con Programmer1).
1. Suspender / Cerrar la aplicación actual y abrir App2 (desarrollado por Programmer2).
1. Supongamos que Programmer2 no está integrado con MVPD2; por lo tanto, el usuario NO se autenticará en App2.
1. Autentíquese con MVPD2 (que está integrado con Programmer2) en App2.
1. Vuelva a la aplicación 1; el usuario seguirá estando autenticado con el programador 1.

### Formato {#format}

#### Token de autenticación {#authn_token}

La lista siguiente presenta el formato del token de autenticación:

```JSON
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

```JSON
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


#### Token de medio corto {#short_media_token}

El listado siguiente presenta el formato del token de medio corto.  Este token está expuesto a la aplicación del programador.  Se pasa a la aplicación del programador al final de un proceso de asignación de derechos exitoso:

```JSON
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
 

#### Enlace de dispositivos {#device_binding}

En las listas XML anteriores, observe la etiqueta titulada `simpleTokenFingerprint`. El propósito de esta etiqueta es albergar información nativa sobre la individualización del ID del dispositivo. La biblioteca AccessEnabler puede obtener dicha información de personalización y ponerla a disposición de los servicios de autenticación de Primetime durante las llamadas de asignación de derechos. El servicio utilizará esta información e la integrará en los tokens reales, lo que vinculará efectivamente los tokens a un dispositivo específico. El objetivo final de esto es hacer que los tokens no se puedan transferir entre dispositivos.

En las listas XML anteriores, observe la etiqueta titulada simpleTokenFingerprint. El propósito de esta etiqueta es albergar información nativa sobre la individualización del ID del dispositivo. La biblioteca AccessEnabler puede obtener dicha información de personalización y ponerla a disposición de los servicios de autenticación de Primetime durante las llamadas de asignación de derechos. El servicio utilizará esta información e la integrará en los tokens reales, lo que vinculará efectivamente los tokens a un dispositivo específico. El objetivo final de esto es hacer que los tokens no se puedan transferir entre dispositivos.

Como esta es obviamente una característica relacionada con la seguridad, esta información es inherentemente &quot;sensible&quot; desde el punto de vista de la seguridad. Como resultado, esta información debe protegerse tanto de la manipulación como de la escucha. El problema de la escucha se resuelve enviando las solicitudes de autenticación/autorización a través del protocolo HTTPS. La protección de manipulación se gestiona mediante la firma digital de la información de identificación del dispositivo. La biblioteca AccessEnabler calcula un ID de dispositivo a partir de la información proporcionada por el dispositivo y, a continuación, envía el ID de dispositivo &quot;en blanco&quot; a los servidores de autenticación de Primetime como parámetro de solicitud.  Los servidores de autenticación de Primetime firman digitalmente el ID del dispositivo con la clave privada de Adobe y lo añaden al token de autenticación devuelto a AccessEnabler. Por lo tanto, el ID del dispositivo está enlazado con el token de autenticación.  Durante el flujo de autorización, AccessEnabler vuelve a enviar el ID del dispositivo en la etiqueta clear, junto con el token de autenticación.  El fallo del proceso de validación provocará automáticamente un error en los flujos de trabajo de autenticación/autorización.  Los servidores de autenticación de Primetime aplican la clave privada al ID del dispositivo y la comparan con el valor del token de autenticación.  Si no coinciden, el flujo de asignación de derechos falla.
