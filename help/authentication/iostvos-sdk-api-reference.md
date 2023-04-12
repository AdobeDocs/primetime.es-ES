---
title: Referencia de la API de iOS/tvOS
description: Referencia de la API de iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '7000'
ht-degree: 0%

---


# Referencia de la API del SDK para iOS/tvOS {#iostvos-sdk-api-reference}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#intro}

En esta página se describen los métodos y las funciones de llamada de retorno expuestos por el cliente nativo de iOS/tvOS para la autenticación de Adobe Primetime. Los métodos y las funciones de llamada de retorno que se describen aquí se definen en la variable `AccessEnabler.h` y `EntitlementDelegate.h` archivos de encabezado; puede encontrarlos en el SDK de iOS AccessEnabler aquí: `[SDK directory]/AccessEnabler/headers/api/`


Documentación asociada:

* Para obtener una descripción del flujo de derechos de autenticación de Primetime básico, consulte [Flujo de derechos](/help/authentication/entitlement-flow.md).
* Para obtener un tutorial paso a paso sobre cómo implementar el flujo de derechos de autenticación de Primetime mediante esta API, consulte [Guía de integración de iOS](/help/authentication/iostvos-sdk-cookbook.md).
* Para obtener el último SDK de iOS AccessEnabler, consulte [Biblioteca de habilitadores de acceso nativos de iOS](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

>[!NOTE]
>
>El Adobe le anima a utilizar solo la autenticación de Primetime *public* API:
>
>* Las API públicas están disponibles y se han probado completamente en todos los tipos de clientes admitidos. Para cualquier función pública, nos aseguramos de que cada tipo de cliente tenga una versión correspondiente de los métodos asociados.
>* Las API públicas deben ser lo más estables posible, para admitir la compatibilidad con versiones anteriores y garantizar que las integraciones de socios no se rompan. Sin embargo, para las API no públicas, nos reservamos el derecho de cambiar su firma en cualquier momento futuro. Si se encuentra con un flujo particular que no se puede admitir mediante una combinación de las llamadas públicas actuales a la API de autenticación de Primetime, el mejor enfoque es informarnos. Teniendo en cuenta sus necesidades, podemos modificar las API públicas y proporcionar una solución estable para el futuro.


</br>

## Referencia de API {#apis}

* [init](#initWithSoftwareStatement):softwareStatement : crea una instancia del objeto AccessEnabler.

* **[OBSOLETO]** [init](#init) - Crea una instancia del objeto AccessEnabler.

* [setOptions:options:](#setOptions) : configura opciones globales del SDK como profile o visitorID.

* [setRequestor:](#setReqV3)[requestorID](#setReqV3),[setRequestor:requestorID:serviceProviders:](#setReqV3) - Establece la identidad del programador.

* **[OBSOLETO]** [setRequestor:signedRequestorId:](#setReq),[setRequestor:signedRequestorId:serviceProviders:](#setReq) - Establece la identidad del programador.

* **[OBSOLETO]** [setRequestor:signedRequestorId:secret:publicKey](#setReq_tvos), [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos)- Establece la identidad del programador.

* [setRequestorComplete:](#setReqComplete) - Informa a la aplicación de que la fase de configuración ha finalizado.

* [checkAuthentication](#checkAuthN) - Comprueba el estado de autenticación del usuario actual.

* [getAuthentication](#getAuthN), [getAuthentication:withData:](#getAuthN) : inicia el flujo de trabajo de autenticación completo.

* [getAuthentication:filter](#getAuthN_filter),[getAuthentication:withData:](#getAuthN)[yFilter](#getAuthN_filter) : inicia el flujo de trabajo de autenticación completo.

* [displayProviderDialog:](#dispProvDialog) - Informa a su aplicación de que cree una instancia de los elementos de IU adecuados para que el usuario seleccione un MVPD.

* [setSelectedProvider:](#setSelProv) - Informa a AccessEnabler de la selección MVPD del usuario.

* [navegarToUrl:](#nav2url) - Informa a su aplicación de que el usuario debe ser presentado con la página de inicio de sesión de MVPD.

* [navegarToUrl:useSVC:](#nav2urlSVC) - Informa a su aplicación de que el usuario debe ser presentado con la página de inicio de sesión de MVPD, utilizando SFSafariViewController

* [handleExternalURL:url](#handleExternalURL) - Completa el flujo de autenticación/cierre de sesión.

* **[OBSOLETO]** [getAuthenticationToken](#getAuthNToken) - Solicita el token de autenticación del servidor back-end.

* [setAuthenticationStatus:errorCode:](#setAuthNStatus) - Informa a la aplicación del estado del flujo de autenticación.

* [checkPreauthorizedResources:](#checkPreauth) - Determina si el usuario ya está autorizado a ver recursos protegidos específicos.

* [checkPreauthorizedResources:cache:](#checkPreauthCache) - Determina si el usuario ya está autorizado a ver recursos protegidos específicos.

* [preauthorizedResources:](#preauthResources) - Proporciona una lista de los recursos que el usuario ya está autorizado a ver.

* [checkAuthorization:](#checkAuthZ), [checkAuthorization:withData:](#checkAuthZ) - Comprueba el estado de autorización del usuario actual.

* [getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ) - Inicia el flujo de autorización.

* [setToken:forResource:](#setToken) - Informa a su aplicación de que el flujo de autorización se completó correctamente.

* [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) - Informa a su aplicación de que el flujo de autorización ha fallado.

* [cierre de sesión](#logout) - Inicia el flujo de cierre de sesión.

* [getSelectedProvider](#getSelProv) - Determina el proveedor seleccionado actualmente.

* [selectedProvider:](#selProv) - Proporciona información sobre el MVPD seleccionado actualmente a su aplicación.

* [getMetadata:](#getMeta) - Recupera información expuesta como metadatos por la biblioteca AccessEnabler.

* [currentTvProviderDialog:](#presentTvDialog) - Informa a la aplicación de que muestra el cuadro de diálogo SSO de Apple.

* [dismissTvProviderDialog:](#dismissTvDialog) - Informa a la aplicación de que oculte el cuadro de diálogo SSO de Apple.

* [setMetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus) - Entrega los metadatos solicitados por un [getMetadata:](#getMeta) llamada a .

* [sendTrackingData:forEventType:](#sendTracking) : ofrece información de datos de seguimiento.

* [MVPD](#mvpd) - La clase MVPD. [Contiene información sobre el MVPD]

### init:softwareStatement {#initWithSoftwareStatement}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Crea una instancia del objeto AccessEnabler. Debe haber una sola instancia de AccessEnabler por instancia de aplicación.

| **Llamada de API: Constructor de iOS AccessEnabler** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**Disponibilidad:** v3.0+

**Parámetros:**

* **SoftwareStatement:** Cadena que identifica la aplicación en el sistema de Adobe. Consulte cómo obtener una declaración de software.

[De vuelta al principio...](#apis)



### init - [OBSOLETO]{#init}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Crea una instancia del objeto AccessEnabler. Debe haber una sola instancia de AccessEnabler por instancia de aplicación.

| Llamada de API: Constructor de iOS AccessEnabler |
| --- |
| ```- (id) init;``` |

**Disponibilidad:** v1.0+ **Hasta:** v3.0

**Parámetros:** Ninguna

[De vuelta al principio...](#apis)

</br>

### setOptions:options {#setOptions}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Configura las opciones globales del SDK. Acepta un NSDictionary como argumento. Los valores del diccionario se pasarán al servidor junto con cada llamada de red que realice el SDK.

**Nota:** Los valores se pasarán al servidor independientemente del flujo actual (autenticación/autorización). Si desea cambiar los valores, puede llamar a este método en cualquier momento.

| Llamada de API: setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**Disponibilidad:** v2.3.0+

**Parámetros:**

* *opciones*: Un NSDictionary que contiene opciones globales del SDK. Actualmente están disponibles las siguientes opciones:
   * **applicationProfile** - Se puede utilizar para realizar configuraciones de servidor basadas en este valor.
   * **visitorID** - El Marketing Cloud visitorID. Este valor se puede usar posteriormente para informes de análisis avanzados.
   * **handleSVC** - Booleano que indica si el programador administrará el SFSafariViewControlers. Consulte [Compatibilidad con SFSafariViewController en el SDK para iOS 3.2+](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) para obtener más información.
      * Si está configurado como **false,** el SDK presentará automáticamente al usuario final un SFSafariViewController. El SDK navegará aún más hasta la dirección URL de la página de inicio de sesión de los MVPD.
      * Si está configurado como **true,** el SDK **NOT** presentar automáticamente al usuario final con un SFSafariViewController. El SDK profundizará en el déclencheur **navegar(toUrl:{url}, useSVC:YES)**.
* **device\_info** - La información del cliente tal como se describe en [Pasar información de clientes](/help/authentication/passing-client-information-device-connection-and-application.md).

[De vuelta al principio...](#apis)


### setRequestor:requestorID, setRequestor:requestorID:serviceProviders: {#setReqV3}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Establece la identidad del programador. A cada programador se le asigna un ID único al registrarse con Adobe para el sistema de autenticación de Primetime. Cuando se trata de SSO y tokens remotos, el estado de autenticación puede cambiar cuando la aplicación está en segundo plano, se puede volver a llamar a setRequestor cuando la aplicación se ponga en primer plano para sincronizar con el estado del sistema (obtenga un token remoto si SSO está habilitado o elimine el token local si se ha producido un cierre de sesión mientras tanto).

La respuesta del servidor contiene una lista de MVPD junto con información de configuración adjunta a la identidad del Programador. El código AccessEnabler utiliza internamente la respuesta del servidor. Solo el estado de la operación (es decir, SUCCESS/FAIL) se presenta a la aplicación a través de la variable `setRequestorComplete:` llamada de retorno.

Si la variable `urls` no se usa, la llamada de red resultante se dirige a la dirección URL predeterminada del proveedor de servicios: el entorno de producción/VERSIÓN de Adobe.


Si se proporciona un valor para la variable `urls` , la llamada de red resultante se dirige a todas las direcciones URL proporcionadas en la variable `urls` parámetro. Todas las solicitudes de configuración se activan simultáneamente en subprocesos separados. El primer encuestado tiene prioridad al compilar la lista de MVPD. Para cada MVPD de la lista, AccessEnabler recuerda la URL del proveedor de servicios asociado. Todas las solicitudes de asignación de derechos subsiguientes se dirigen a la URL asociada al proveedor de servicios que estaba emparejado con el MVPD de destino durante la fase de configuración.

| Llamada de API: configuración del solicitante |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**Disponibilidad:** v3.0+

| Llamada de API: configuración del solicitante |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**Disponibilidad:** v3.0+

**Parámetros:**

* *requestorID*: ID exclusivo asociado al programador. Pase el ID exclusivo asignado por Adobe a su sitio cuando se registre por primera vez con el servicio de autenticación de Primetime.
* *url*: Parámetro opcional; de forma predeterminada, se utiliza el proveedor de servicios de Adobe (http://sp.auth.adobe.com/). Esta matriz le permite especificar puntos finales para los servicios de autenticación y autorización proporcionados por Adobe (se pueden utilizar diferentes instancias para la depuración). Puede utilizarlo para especificar varias instancias del proveedor del servicio de autenticación de Primetime. Al hacerlo, la lista de MVPD está compuesta por los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD.

>[!NOTE]
>
>Si se llama sin la función `serviceProviders` , la biblioteca recuperará la configuración del proveedor de servicios predeterminado (es decir, `https://sp.auth.adobe.com` para el perfil de producción o `https://sp.auth-staging.adobe.com` para el perfil de ensayo). Si la variable `serviceProviders` , debe ser una matriz de direcciones URL. La información de configuración se recupera de todos los puntos finales especificados y se combina. Si existe información duplicada en diferentes respuestas del proveedor de servicios, el conflicto se resuelve en favor del servidor que responde más rápido (es decir, el servidor con el tiempo de respuesta más corto tiene prioridad).

**Llamadas de retorno activadas:** [`setRequestorComplete:`](#setReqComplete)

[De vuelta al principio...](#apis)

</br>

### setRequestor:setSignedRequestorId:, setRequestor:setSignedRequestorId:serviceProviders: - [OBSOLETO] {#setReq}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Establece la identidad del programador. A cada programador se le asigna un ID único al registrarse con Adobe para el sistema de autenticación de Primetime. Cuando se trata de SSO y tokens remotos, el estado de autenticación puede cambiar cuando la aplicación está en segundo plano, se puede volver a llamar a setRequestor cuando la aplicación se ponga en primer plano para sincronizar con el estado del sistema (obtenga un token remoto si SSO está habilitado o elimine el token local si se ha producido un cierre de sesión mientras tanto).

La respuesta del servidor contiene una lista de MVPD junto con información de configuración adjunta a la identidad del Programador. El código AccessEnabler utiliza internamente la respuesta del servidor. Solo el estado de la operación (es decir, SUCCESS/FAIL) se presenta a la aplicación a través de la variable `setRequestorComplete:` llamada de retorno.

Si la variable `urls` no se usa, la llamada de red resultante se dirige a la dirección URL predeterminada del proveedor de servicios: el entorno de producción/VERSIÓN de Adobe.

Si se proporciona un valor para la variable `urls` , la llamada de red resultante se dirige a todas las direcciones URL proporcionadas en la variable `urls` parámetro. Todas las solicitudes de configuración se activan simultáneamente en subprocesos separados. El primer encuestado tiene prioridad al compilar la lista de MVPD. Para cada MVPD de la lista, AccessEnabler recuerda la URL del proveedor de servicios asociado. Todas las solicitudes de asignación de derechos subsiguientes se dirigen a la URL asociada al proveedor de servicios que estaba emparejado con el MVPD de destino durante la fase de configuración.

| Llamada de API: configuración del solicitante |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**Disponibilidad:** v1.0+ **Hasta:** v3.0

| Llamada de API: configuración del solicitante |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**Disponibilidad:** v1.0+ **Hasta:** v3.0

**Parámetros:**

* *requestorID*: ID exclusivo asociado al programador. Pase el ID exclusivo asignado por Adobe a su sitio cuando se registre por primera vez en el servicio de autenticación de Primetime.
* *signedRequestorID*: **Este parámetro existe en iOS AccessEnabler versiones 1.2 y posteriores.** Una copia del ID del solicitante que se firma digitalmente con su clave privada. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*: Parámetro opcional; de forma predeterminada, se utiliza el proveedor de servicios de Adobe (http://sp.auth.adobe.com/). Esta matriz le permite especificar puntos finales para los servicios de autenticación y autorización proporcionados por Adobe (se pueden utilizar diferentes instancias para la depuración). Puede utilizarlo para especificar varias instancias del proveedor del servicio de autenticación de Primetime. Al hacerlo, la lista de MVPD está compuesta por los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD.

**Notas:** Si se llama sin la función `serviceProviders` , la biblioteca recuperará la configuración del proveedor de servicios predeterminado (es decir,`https://sp.auth.adobe.com` para el perfil de producción o `https://sp.auth-staging.adobe.com` para el perfil de ensayo). Si la variable `serviceProviders` , debe ser una matriz de direcciones URL. La información de configuración se recupera de todos los puntos finales especificados y se combina. Si existe información duplicada en diferentes respuestas del proveedor de servicios, el conflicto se resuelve en favor del servidor que responde más rápido (es decir, el servidor con el tiempo de respuesta más corto tiene prioridad).

**Llamadas de retorno activadas:** [`setRequestorComplete:`](#setReqComplete)


[De vuelta al principio...](#apis)

### setRequestor:setSignedRequestorId:secret:publicKey, setRequestor:setSignedRequestorId:serviceProviders:secret:publicKey - [OBSOLETO] {#setReq_tvos}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Establece la identidad del programador. A cada programador se le asigna un ID único al registrarse con Adobe para el sistema de autenticación de Primetime. Esta configuración debe realizarse solo una vez durante el ciclo de vida de la aplicación.

La respuesta del servidor contiene una lista de MVPD junto con información de configuración adjunta a la identidad del Programador. El código AccessEnabler utiliza internamente la respuesta del servidor. Solo el estado de la operación (es decir, SUCCESS/FAIL) se presenta a la aplicación a través de la variable `setRequestorComplete:` llamada de retorno.

Si la variable `urls` no se usa, la llamada de red resultante se dirige a la dirección URL predeterminada del proveedor de servicios: el entorno de producción/VERSIÓN de Adobe.

Si se proporciona un valor para la variable `urls` , la llamada de red resultante se dirige a todas las direcciones URL proporcionadas en la variable `urls` parámetro. Todas las solicitudes de configuración se activan simultáneamente en subprocesos separados. El primer encuestado tiene prioridad al compilar la lista de MVPD. Para cada MVPD de la lista, AccessEnabler recuerda la URL del proveedor de servicios asociado. Todas las solicitudes de asignación de derechos subsiguientes se dirigen a la URL asociada al proveedor de servicios que estaba emparejado con el MVPD de destino durante la fase de configuración.



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: configuración del solicitante</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID
               secret:(NSString *)secret
            publicKey:(NSString *)publicKey;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidad:** v2.0+ **Hasta:** v3.0

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: configuración del solicitante</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID 
     serviceProviders:(NSArray *)urls</code></pre>
<p><code class="sourceCode objectivec">               secret:(NSString *)secret</code></p>
<p><code class="sourceCode objectivec">            publicKey:(NSString *)publicKey;</code></p></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v2.0+ **Hasta:** v3.0

**Parámetros:**

* *requestorID*: ID exclusivo asociado al programador. Pase el ID exclusivo asignado por Adobe a su sitio cuando se registre por primera vez en el servicio de autenticación de Primetime.
* *signedRequestorID*: **Este parámetro existe en iOS AccessEnabler versiones 1.2 y posteriores.** Una copia del ID del solicitante que se firma digitalmente con su clave privada. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*: Parámetro opcional; de forma predeterminada, se utiliza el proveedor de servicios de Adobe (http://sp.auth.adobe.com/). Esta matriz le permite especificar puntos finales para los servicios de autenticación y autorización proporcionados por Adobe (se pueden utilizar diferentes instancias para la depuración). Puede utilizarlo para especificar varias instancias del proveedor del servicio de autenticación de Primetime. Al hacerlo, la lista de MVPD está compuesta por los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD.
* secret y publicKey: Clave pública y secreta utilizada para firmar las segundas llamadas de pantalla. Para obtener más información, consulte [Documentación sin cliente](#create_dev).

Si se llama sin la función `serviceProviders` , la biblioteca recuperará la configuración del proveedor de servicios predeterminado (p. ej., `https://sp.auth.adobe.com` para el perfil de producción o https://sp.auth-staging.adobe.com para el perfil de ensayo). Si la variable `serviceProviders` , debe ser una matriz de direcciones URL. La información de configuración se recupera de todos los puntos finales especificados y se combina. Si existe información duplicada en diferentes respuestas del proveedor de servicios, el conflicto se resuelve en favor del servidor que responde más rápido (es decir, el servidor con el tiempo de respuesta más corto tiene prioridad).

**Llamadas de retorno activadas:** [`setRequestorComplete:`](#setReqComplete)

[De vuelta al principio...](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler que informa a su aplicación de que la fase de configuración ha finalizado. Esto es una señal de que la aplicación puede empezar a emitir solicitudes de asignación de derechos. La aplicación no puede emitir solicitudes de asignación de derechos hasta que se complete la fase de configuración.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: configuración del solicitante completada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidad:** v1.0+

**Parámetros**:

* *status*: puede tomar uno de los siguientes valores:
   * `ACCESS_ENABLER_STATUS_SUCCESS` : la fase de configuración se completó correctamente
   * `ACCESS_ENABLER_STATUS_ERROR` : error en la fase de configuración

**Activado por:**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[De vuelta al principio...](#apis)

</br>

### checkAuthentication {#checkAuthN}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Comprueba el estado de autenticación del usuario actual.
Para ello, busca un token de autenticación válido en el espacio de almacenamiento del token local. Llamar a este método no realiza llamadas de red. La aplicación lo utiliza para consultar el estado de autenticación del usuario y actualizar la IU en consecuencia (es decir, actualizar la IU de inicio/cierre de sesión). El estado de autenticación se comunica a la aplicación a través del [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) llamada de retorno.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: comprobar el estado de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[De vuelta al principio...](#apis)

</br>

### getAuthentication, getAuthentication:withData: {#getAuthN}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Inicia el flujo de trabajo de autenticación completo. Se inicia comprobando el estado de autenticación. Si aún no se ha autenticado, se inicia el flujo de autenticación state-machine:

* si el último intento de autenticación fue exitoso, la fase de selección de MVPD se omite y la variable [`navigateToUrl:`](#nav2url) se activa la rellamada. La aplicación utiliza esta llamada de retorno para crear una instancia del control WebView que presenta al usuario la página de inicio de sesión de MVPD. **[NOTA: A partir de Access Enabler 1.5, esta funcionalidad no está disponible debido a una limitación en el SDK].**
* si el último intento de autenticación no se realizó correctamente o si el usuario cerró la sesión de forma explícita, la variable [`displayProviderDialog:`](#dispProvDialog) se activa la rellamada. Su aplicación utiliza esta llamada de retorno para mostrar la IU de selección de MVPD. Además, se requiere que la aplicación reanude el flujo de autenticación informando a la biblioteca de AccessEnabler sobre la selección de MVPD del usuario a través del [`setSelectedProvider:`](#setSelProv) método.

Como las credenciales del usuario se verifican en la página de inicio de sesión de MVPD, su aplicación es necesaria para supervisar las operaciones de redirección múltiple que se producen mientras el usuario se autentica en la página de inicio de sesión de MVPD. Cuando se introducen las credenciales correctas, el control WebView se redirige a una URL personalizada definida por la variable `ADOBEPASS_REDIRECT_URL` constante. WebView no pretende cargar esta dirección URL. La aplicación debe interceptar esta dirección URL e interpretar este evento como una señal de que la fase de inicio de sesión ha finalizado. A continuación, debe entregar el control al AccessEnabler para completar el flujo de autenticación (llamando a la variable [handleExternalURL](#handleExternalURL) método).

Finalmente, el estado de autenticación se comunica a la aplicación a través de la variable [setAuthenticationStatus:errorCode:](#setAuthNStatus) llamada de retorno.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: inicia el flujo de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: inicia el flujo de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Disponibilidad:** v1.9+

**Parámetros:**

* *forceAuthn*: Un indicador que especifica si se debe iniciar el flujo de autenticación, independientemente de si el usuario ya está autenticado o no.
* *data*: Un diccionario que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK.

**Llamadas de retorno activadas:** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[De vuelta al principio...](#apis)

</br>

### getAuthentication:filter, getAuthentication:withData:yFilter {#getAuthN_filter}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Inicia el flujo de trabajo de autenticación completo. Se inicia comprobando el estado de autenticación. Si aún no se ha autenticado, se inicia el flujo de autenticación state-machine:

* [currentTvProviderDialog()](#presentTvDialog) se llamará a si el solicitante actual tiene al menos un MVPD que admita SSO. Si ningún MVPD admite SSO, el flujo de autenticación clásico comenzará y el parámetro de filtro se ignorará.
* Una vez que el usuario completa el flujo SSO de Apple [dismissTvProviderDialog()](#dismissTvDialog) se activará y el proceso de autenticación finalizará.

Finalmente, el estado de autenticación se comunica a la aplicación a través de la variable [setAuthenticationStatus:errorCode:](#setAuthNStatus) llamada de retorno.

**Disponibilidad:** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: inicia el flujo de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSDictionary *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: inicia el flujo de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSDictionary *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parámetros:**

* *forceAuthn*: Un indicador que especifica si se debe iniciar el flujo de autenticación, independientemente de si el usuario ya está autenticado o no.
* *data*: Un diccionario que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK. 
* filtro: Un diccionario con dos listas de id de MVPD que deberían aparecer en el cuadro de diálogo SSO de Apple. Cualquier MVPD que no admita SSO será ignorada, pero el pedido será respetado. El diccionario debe tener dos claves:
   * TV\_PROVIDERS: Una lista con todos los MVPD que deberían aparecer en el selector
   * FEATURED\_TV\_PROVIDERS: Una lista con todos los MVPD que deben marcarse como incluidos en el selector. Los MVPD de esta lista también deben especificarse en la lista TV\_PROVIDERS.

**Disponibilidad:** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: inicia el flujo de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSArray *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: inicia el flujo de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSArray *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parámetros:**

* *forceAuthn*: Un indicador que especifica si se debe iniciar el flujo de autenticación, independientemente de si el usuario ya está autenticado o no.
* *data*: Un diccionario que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK. 
* filtro: Una lista de ID de MVPD que deberían aparecer en el cuadro de diálogo de SSO de Apple. Cualquier MVPD que no admita SSO será ignorada, pero el pedido será respetado.

**Llamadas de retorno activadas:** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[De vuelta al principio...](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler para informar a la aplicación de que es necesario crear una instancia de los elementos de la interfaz de usuario correspondientes para permitir al usuario seleccionar el MVPD deseado. La rellamada proporciona una lista de objetos MVPD con información adicional que puede ayudar a crear correctamente el panel de la interfaz de usuario de selección (como la URL que señala al logotipo de MVPD, el nombre descriptivo, etc.)

Una vez que el usuario ha seleccionado el MVPD deseado, la aplicación de la capa superior es necesaria para reanudar el flujo de autenticación llamando a `setSelectedProvider:` y transmitirle el ID del MVPD correspondiente a la selección del usuario.

**Anulación del flujo de autenticación** - Este es un punto en el que el usuario tiene la capacidad de presionar el botón &quot;Atrás&quot;, que equivale a anular el flujo de autenticación. En ese caso, la aplicación debe llamar a la función [setSelectedProvider:](#setSelProv) , pasando null como parámetro, para dar a AccessEnabler la oportunidad de restablecer su máquina-estado de autenticación.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: mostrar la IU de selección de MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidad:** v1.0+

**Parámetros**:

* *mvpds*: lista de objetos MVPD que contienen información relacionada con MVPD que la aplicación puede utilizar para crear los elementos de la interfaz de usuario de selección de MVPD.

**Activado por:** ` getAuthentication, `[getAuthentication:withData:](#getAuthN),` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[De vuelta al principio...](#apis)

</br>

#### setSelectedProvider: {#setSelProv}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Su aplicación llama a este método para informar al habilitador de acceso de la selección de MVPD del usuario. La aplicación puede utilizar este método para seleccionar o cambiar el proveedor de servicios utilizado para la autenticación.

Si el MVPD seleccionado es un MVPD TempPass, se autenticará automáticamente con ese MVPD sin necesidad de llamar a getAuthentication() después.

Tenga en cuenta que esto no es posible para el pase temporal promocional donde se proporcionan parámetros adicionales en el método getAuthentication() .

Al pasar *null* como parámetro, Access Enabler supone que el usuario ha cancelado el flujo de autenticación (es decir, ha presionado el botón &quot;Atrás&quot;), y responde restableciendo el equipo-estado de autenticación y llamando a la función [setAuthenticationStatus:errorCode:](#setAuthNStatus) llamada de retorno con la función `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` código de error.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: establecer el proveedor seleccionado actualmente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[De vuelta al principio...](#apis)

</br>

#### navegarToUrl: {#nav2url}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción:** Llamada de retorno activada por AccessEnabler para solicitar a su aplicación que cree una instancia de un controlador UIWebView/WKWebView y que cargue la URL proporcionada en la llamada de retorno **`url`** parámetro. La devolución de llamada pasa la variable **`url`** que representa la dirección URL del extremo de autenticación o la dirección URL del extremo de cierre de sesión.

Como UIWebView/WKWebView` `el controlador de pasa por varias redirecciones, su aplicación debe supervisar la actividad del controlador y detectar el momento en que carga una URL personalizada específica definida por el `ADOBEPASS_REDIRECT_URL `constante (p. ej. `adobepass://ios.app`). Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue realmente. Su aplicación solo debe interpretarla como una señal de que el flujo de autenticación o cierre de sesión se ha completado y de que es seguro cerrar el controlador. Cuando el controlador carga esta URL personalizada específica, la aplicación debe cerrar UIWebView/WKWebView e invocar AccessEnabler&#39;s `handleExternalURL:url `método de API.

**Nota:** Tenga en cuenta que en el caso del flujo de autenticación, este es un punto en el que el usuario tiene la capacidad de presionar el botón &quot;Atrás&quot;, que equivale a la anulación del flujo de autenticación. En este caso, la aplicación debe llamar a la función [setSelectedProvider:](#setSelProv) paso de métodos **`nil`** como parámetro y dando la oportunidad a AccessEnabler de restablecer su máquina-estado de autenticación.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: mostrar página de inicio de sesión de MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros**:

* *url*: la URL que señala a la página de inicio de sesión de MVPD

**Activado por:** [setSelectedProvider:](#setSelProv)

 

[De vuelta al principio...](#apis)

</br>

#### navegarToUrl:useSVC: {#nav2urlSVC}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción:** Llamada de retorno activada por AccessEnabler en lugar de la función `navigateToUrl:` llamada de retorno en caso de que la aplicación haya habilitado anteriormente la administración manual del controlador de vista Safari (SVC) a través de la [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](#setOptions) y solo en el caso de MVPD que requieran un controlador de vista Safari (SVC). Para todos los demás MVPD, la variable `navigateToUrl:` se llamará a . Consulte[Compatibilidad con SFSafariViewController en el SDK para iOS 3.2+](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) para obtener más información sobre cómo se debe administrar Safari View Controller (SVC).

Similar a la variable `navigateToUrl:` devolución de llamada `navigateToUrl:useSVC:` se activa mediante AccessEnabler para solicitar a la aplicación que cree una instancia de `SFSafariViewController` y para cargar la URL proporcionada en la llamada de retorno **`url`** parámetro. La devolución de llamada pasa la variable **`url`** que representa la dirección URL del extremo de autenticación o la dirección URL del extremo de cierre de sesión, y la variable **`useSVC`** que especifica que la aplicación debe utilizar un `SFSafariViewController`.

Como `SFSafariViewController` el controlador de usa varias redirecciones, la aplicación debe supervisar la actividad del controlador y detectar el momento en que carga una URL personalizada específica definida por el `application's custom scheme` (p. ej.** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`). Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue realmente. Su aplicación solo debe interpretarla como una señal de que el flujo de autenticación o cierre de sesión se ha completado y de que es seguro cerrar el controlador. Cuando el controlador carga esta dirección URL personalizada específica, la aplicación debe cerrar la `SFSafariViewController` y llame a AccessEnabler `handleExternalURL:url `método de API.

**Nota:** Tenga en cuenta que en el caso del flujo de autenticación, este es un punto en el que el usuario tiene la capacidad de presionar el botón &quot;Atrás&quot;, que equivale a la anulación del flujo de autenticación. En este caso, la aplicación debe llamar a la función [setSelectedProvider:](#setSelProv) paso de métodos **`nil`** como parámetro y dando la oportunidad a AccessEnabler de restablecer su máquina-estado de autenticación.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: mostrar la página de inicio de sesión de MVPD en SFSafariViewController</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>@optional
- (void) navigateToUrl:(NSString *)url useSVC:(BOOL)useSVC; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:**v 3.2+

**Parámetros**:

* *url:* la URL que señala a la página de inicio de sesión de MVPD
* *useSVC:* si la url debe cargarse en SFSafariViewController.

**Activado por:**[ setOptions:](#setOptions) before [setSelectedProvider:](#setSelProv) 

[De vuelta al principio...](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Su aplicación llama a este método para completar el flujo de autenticación o cierre de sesión. Se debe llamar a este método justo después de que la aplicación detecte el momento en que el `UIWebView/WKWebView or SFSafariViewController` se redirige a una dirección URL personalizada específica. En caso de que la aplicación deba utilizar un `SFSafariViewController `el controlador define la dirección URL personalizada específica `application's custom scheme` (p. ej.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta URL personalizada específica la define el `ADOBEPASS_REDIRECT_URL `constante (p. ej. `adobepass://ios.app`).

En el caso del flujo de autenticación, AccessEnabler completa el flujo recuperando el token de autenticación del servidor back-end y almacenándolo localmente en el almacenamiento de token. AccessEnabler informará a su aplicación de que el flujo de autenticación se completa llamando a la función `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> llamada de retorno con un código de estado de 1, que indica que la llamada de retorno ha sido satisfactoria. Si hay un error durante la ejecución de estos pasos, la variable `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> la rellamada se activa con un código de estado de 0, que indica un error de autenticación, así como un código de error correspondiente.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: completar el flujo de autenticación o cierre de sesión</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code> (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v3.0+

**Parámetros:** 

* *url*: La dirección URL interceptada de la ` UIWebView/WKWebView or SFSafariViewController ` control como cadena.


**Llamadas de retorno activadas:** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[De vuelta al principio...](#apis)

</br>

#### getAuthenticationToken - [OBSOLETO] {#getAuthNToken}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Completa el flujo de autenticación al solicitar el token de autenticación del servidor back-end. Su aplicación debe llamar a este método solo en respuesta al evento en el que el control WebView que aloja la página de inicio de sesión de MVPD se redirija a la URL personalizada definida por la variable `ADOBEPASS_REDIRECT_URL` constante.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: recuperar el token de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthenticationToken; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+ **Hasta:** v3.0

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[De vuelta al principio...](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler que informa a la aplicación del estado del flujo de autenticación. Hay muchos lugares donde este flujo puede fallar, ya sea como resultado de la interacción del usuario o debido a otros escenarios imprevistos (por ejemplo, problemas de conectividad de red, etc.). Esta rellamada informa a la aplicación del estado de éxito/error del flujo de autenticación, al tiempo que proporciona información adicional sobre el motivo del error, cuando es necesario.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: informar del estado del flujo de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setAuthenticationStatus:(int)status 
                       errorCode:(NSString *)code; </code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidad:** v1.0+

**Parámetros**:

* *status*: puede tomar uno de los siguientes valores:
   * `ACCESS_ENABLER_STATUS_SUCCESS` - el flujo de autenticación se completó correctamente
   * `ACCESS_ENABLER_STATUS_ERROR` - error en el flujo de autenticación
* *code*: motivo del error. If *status* es `ACCESS_ENABLER_STATUS_SUCCESS`, luego *code* es una cadena vacía (es decir, definida por la variable `USER_AUTHENTICATED` constante). En caso de error, este parámetro puede tomar uno de los siguientes valores:
   * `USER_NOT_AUTHENTICATED_ERROR` - El usuario no está autenticado. En respuesta a la [checkAuthentication:](#checkAuthN) llamada de método cuando no hay ningún token de autenticación válido en la caché de token local.
   * `PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler ha restablecido el estado-máquina de autenticación después de pasar la aplicación de capa superior *null* a [`setSelectedProvider:`](#setSelProv) para anular el flujo de autenticación.  Presumiblemente, el usuario ha cancelado el flujo de autenticación (es decir, ha presionado el botón &quot;Atrás&quot;).
   * `GENERIC_AUTHENTICATION_ERROR` : el flujo de autenticación falló debido a motivos como la falta de disponibilidad de la red o el usuario canceló el flujo de autenticación explícitamente.

**Activado por:** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN),` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[De vuelta al principio...](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** La aplicación utiliza este método para determinar si el usuario ya está autorizado a ver recursos protegidos específicos. El propósito principal de este método es recuperar información para utilizarla al decorar la interfaz de usuario **(por ejemplo, indicando el estado de acceso con los iconos de bloqueo y desbloqueo).**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: establecer el proveedor seleccionado actualmente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.3+

**Parámetros:**

* *recursos:* matriz de recursos para los que se debe comprobar la autorización. Cada elemento de la lista debe ser una cadena que represente el ID del recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso en la llamada de , es decir, debe ser un valor acordado establecido entre el Programador y el MVPD o un fragmento RSS de medios.

**Llamada de retorno activada:** [`preauthorizedResources:`](#preauthResources)

[De vuelta al principio...](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** La aplicación utiliza este método para determinar si el usuario ya está autorizado a ver recursos protegidos específicos. El objetivo principal de este método es recuperar información para utilizarla al decorar la interfaz de usuario (por ejemplo, indicar el estado de acceso con los iconos de bloqueo y desbloqueo). La variable **cache** controla si la caché interna se utiliza para resolver recursos.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: establecer el proveedor seleccionado actualmente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**Disponibilidad:** v3.1+

 

**Parámetros:**

* *recursos:* matriz de recursos para los que se debe comprobar la autorización. Cada elemento de la lista debe ser una cadena que represente el ID del recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso en la variable `getAuthorization:` , es decir, debe ser un valor acordado establecido entre el Programador y el MVPD o un fragmento RSS de medios.
* *caché:* Boolean que especifica si se utiliza la caché interna para resolver recursos. Si es false, se omitirá la caché, lo que dará como resultado llamadas al servidor cada vez que se llame a esta API.

**Llamada de retorno activada:** [`preauthorizedResources:`](#preauthResources)

[De vuelta al principio...](#apis)

</br>

### preauthorizedResources: {#preauthResources}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción:** Llamada de retorno activada por `checkPreauthorizedResources:`. Proporciona una lista de los recursos que el usuario ya está autorizado a ver.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: establecer el proveedor seleccionado actualmente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.3+

**Parámetros:**

* `resources`: matriz de recursos para los que el usuario ya está autorizado a ver.

**Activado por:** [`checkPreauthorizedResources:`](#checkPreauth)

 

[De vuelta al principio...](#apis)

</br>

### checkAuthorization:, checkAuthorization:withData: {#checkAuthZ}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** La aplicación utiliza este método para comprobar el estado de autorización. Se inicia comprobando primero el estado de autenticación. Si no se autentica, la variable [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) se activa la rellamada y el método se cierra. Si el usuario está autenticado, también déclencheur el flujo de autorización. Consulte los detalles sobre [`getAuthorization:`](#getAuthZ) método.


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: comprobar el estado de autorización</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: comprobar el estado de autorización</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource:
                   withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.9+

**Parámetros:**

* *recurso*: el ID del recurso para el que el usuario solicita la autorización.
* *data*: Un diccionario que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK. 

**Llamadas de retorno activadas:**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[De vuelta al principio...](#apis)

</br>

### getAuthorization:, getAuthorization:withData: {#getAuthZ}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** La aplicación utiliza este método para iniciar el flujo de autorización. Si el usuario no está autenticado, también inicia el flujo de autenticación. Si el usuario se autentica, AccessEnabler procede a enviar solicitudes para el token de autorización (si no hay ningún token de autorización válido en la caché de token local) y para el token de medios de corta duración. Una vez obtenido el token de contenido corto, el flujo de autorización se considera completo. La variable [setToken:forResource:](#setToken) se activa la rellamada de y el token de contenido corto se envía como parámetro a la aplicación. Si, por cualquier razón, la autorización falla, la variable [tokenRequestFailed:forEventType:](#tokenReqFailed) se activa la llamada de retorno y se proporcionan el código o los detalles del error.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: iniciar el flujo de autorización</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: iniciar el flujo de autorización</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource:
                 withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

 

**Disponibilidad:** v1.9+

**Parámetros:**

* *recurso*: el ID del recurso para el que el usuario solicita la autorización.
* *data*: Un diccionario que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK. 

**Llamadas de retorno activadas:** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**Llamadas de retorno adicionales activadas:**\
Este método también puede almacenar en déclencheur las siguientes llamadas de retorno (si también se inicia el flujo de autenticación): `setAuthenticationStatus:errorCode:`, `displayProviderDialog:`\
 
**NOTA: Utilice checkAuthorization: / checkAuthorization:withData: en lugar de getAuthorization: / getAuthorization:withData: siempre que sea posible. getAuthorization: / getAuthorization:withData: iniciará un flujo de autenticación completo (si el usuario no está autenticado) y esto podría llevar a una implementación complicada por parte del programador.**

[De vuelta al principio...](#apis)

</br>

### setToken:forResource: {#setToken}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler que informa a su aplicación de que el flujo de autorización se completó correctamente. El token de contenido de corta duración también se entrega como parámetro.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: el flujo de autorización se completó correctamente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setToken:(NSString *)token 
      forResource:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros**:

* *token*: el token de medio de vida corta
* *recurso*: el recurso para el que se obtuvo la autorización

**Activado por:** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ),` `[getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)

[De vuelta al principio...](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription: {#tokenReqFailed}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler que informa a la aplicación de capa superior de que el flujo de autorización ha fallado.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: error en el flujo de autorización</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) tokenRequestFailed:(NSString *)resource 
                  errorCode:(NSString *)code 
           errorDescription:(NSString *)description; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros**:

* *recurso*: Recurso para el que se obtuvo la autorización.
* *code*: El código de error asociado con el escenario de error. Valores posibles:
   * `USER_NOT_AUTHORIZED_ERROR` : el usuario no pudo autorizar para el recurso dado
* *descripción*: Detalles adicionales sobre el escenario de error. Si esta cadena descriptiva no está disponible por ningún motivo, la autenticación de Primetime envía una cadena vacía **(&quot;&quot;&quot;)**. \
   Una MVPD puede utilizar esta cadena para pasar mensajes de error personalizados o mensajes relacionados con las ventas. Por ejemplo, si a un suscriptor se le niega la autorización para un recurso, el MVPD podría enviar un mensaje como: &quot;Actualmente no tiene acceso a este canal en su paquete. Si desea actualizar el paquete, haga clic en **here**.&quot; La autenticación de Primetime pasa el mensaje a través de esta llamada de retorno al programador, que tiene la opción de mostrarlo o ignorarlo. La autenticación de Primetime también puede utilizar este parámetro para proporcionar una notificación de la condición que podría haber provocado un error. Por ejemplo, &quot;Se produjo un error de red al comunicarse con el servicio de autorización del proveedor&quot;.

**Activado por:** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[De vuelta al principio...](#apis)

</br>

### cierre de sesión {#logout}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Su aplicación llama a este método para iniciar el flujo de cierre de sesión. El cierre de sesión es el resultado de una serie de operaciones de redireccionamiento HTTP debido al hecho de que el usuario necesita cerrar la sesión tanto desde los servidores de autenticación de Primetime como desde los servidores de MVPD. Debido a que este flujo no se puede completar con una solicitud HTTP simple emitida por la biblioteca AccessEnabler, una `UIWebView/WKWebView or SFSafariViewController` debe crearse una instancia del controlador para poder seguir las operaciones de redireccionamiento HTTP.

El flujo de cierre de sesión difiere del flujo de autenticación en que no se requiere que el usuario interactúe con la variable `UIWebView/WKWebView or SFSafariViewController`  de cualquier manera. Por lo tanto, Adobe recomienda que haga el control invisible (es decir, oculto) durante el proceso de cierre de sesión.

Se utiliza un patrón similar al flujo de autenticación. iOS AccessEnabler déclencheur el `navigateToUrl:` o `navigateToUrl:useSVC:` para crear un `UIWebView/WKWebView or SFSafariViewController` y para cargar la URL proporcionada en la llamada de retorno `url` parámetro. Esta es la dirección URL del extremo de cierre de sesión en el servidor back-end. Para el AccessEnabler de tvOS ni el `navigateToUrl:` o `navigateToUrl:useSVC:` llamada de retorno.

A medida que pasa por varias redirecciones, la aplicación debe monitorizar la actividad de la variable `UIWebView/WKWebView or SFSafariViewController `controle y detecte el momento en que carga una URL personalizada específica. Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue realmente. Su aplicación solo debe interpretarla como una señal de que el flujo de cierre de sesión se ha completado y de que es seguro cerrar el controlador. Cuando el controlador carga esta dirección URL personalizada específica, la aplicación debe cerrar el controlador e invocar AccessEnabler `handleExternalURL:url `método de API. En caso de que la aplicación deba utilizar un `SFSafariViewController `el controlador define la dirección URL personalizada específica `application's custom scheme` (p. ej.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta URL personalizada específica la define el `ADOBEPASS_REDIRECT_URL `constante (p. ej. `adobepass://ios.app`).

Al final, AccessEnabler llamará a la función [`setAuthenticationStatus()`](#setAuthNStatus) llamada de retorno con un código de estado de 0, que indica el éxito del flujo de cierre de sesión.

**Nota:** Si el usuario ha iniciado sesión con Apple SSO, se activará el estado de VSA203. En este caso, se debe indicar al usuario que cierre la sesión también desde la configuración del sistema. Si no lo hace, se volverá a autenticar cuando se reinicie la aplicación.


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: iniciar el flujo de cierre de sesión</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[De vuelta al principio...](#apis)

</br>

### getSelectedProvider {#getSelProv}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Utilice este método para determinar el proveedor seleccionado actualmente.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: determinar el MVPD seleccionado actualmente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** [`selectedProvider:`](#selProv)

[De vuelta al principio...](#apis)

</br>

### selectedProvider {#selProv}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler que proporciona información sobre el MVPD seleccionado actualmente a la aplicación.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: información sobre el MVPD seleccionado actualmente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros**:

* *mvpd*: objeto que contiene información sobre el MVPD seleccionado actualmente

**Activado por:** [`getSelectedProvider`](#getSelProv)

[De vuelta al principio...](#apis)

</br>

### getMetadata: {#getMeta}

**Archivo:** AccessEnabler/headers/AccessEnabler.h

**Descripción:** Utilice este método para recuperar información expuesta como metadatos por la biblioteca AccessEnabler. La aplicación puede acceder a estos datos proporcionando un diccionario *key* parámetro de entrada.

Hay dos tipos de metadatos disponibles para los programadores:

* Metadatos estáticos (TTL token de autenticación, TTL token de autorización e ID de dispositivo) 
* Metadatos de usuario (información específica del usuario, como ID de usuario o código postal); se puede pasar de un MVPD al dispositivo de un usuario durante los flujos de autenticación y autorización)

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de API: consulta de AccessEnabler para metadatos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros:**

* *keyDictionary*: una estructura de datos de diccionario, con el siguiente formato:
   * Si la clave es `METADATA_OPCODE_KEY` y el valor es `METADATA_AUTHENTICATION`, se realiza la consulta para obtener el tiempo de caducidad del token de autenticación.
   * Si la clave es `METADATA_OPCODE_KEY` y el valor es `METADATA_AUTHORIZATION` **y**\
      key is `METADATA_RESOURCE_ID_KEY` y es un ID de recurso determinado, entonces la consulta se realiza para obtener el tiempo de caducidad del token de autorización asociado al recurso especificado.
   * Si la clave es `METADATA_OPCODE_KEY` y el valor es `METADATA_DEVICE_ID`, se realiza la consulta para obtener el id del dispositivo actual. Tenga en cuenta que esta función está deshabilitada de forma predeterminada y los programadores deben ponerse en contacto con Adobe para obtener información sobre la habilitación y las tarifas.
   * Si la clave es `METADATA_OPCODE_KEY` y el valor es `METADATA_USER_META` **y** key is `METADATA_USER_META_KEY` y valor es el nombre de los metadatos, entonces la consulta se realiza para los metadatos de usuario. La lista de tipos de metadatos de usuario disponibles:
      * `zip` - Lista de códigos postales
      * `householdID` - Identificador del hogar. En el caso de que un MVPD no admita subcuentas, esto será idéntico a `userID`.
      * `maxRating` - Recopilación de calificaciones parentales máximas para el usuario
      * `userID` - El identificador de usuario. Si un MVPD admite subcuentas y el usuario no es la cuenta principal, `userID` será diferente a `householdID.`
      * `channelID` - Una lista de canales que un usuario puede ver.
   >[!NOTE]
   >
   >Los metadatos de usuario disponibles para un programador dependen de lo que un MVPD ponga a disposición. Esta lista se ampliará a medida que los nuevos metadatos estén disponibles y se añadan al sistema de autenticación de Primetime.

**Llamadas de retorno activadas:** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**Más información:** [Metadatos de usuario](/help/authentication/user-metadata.md)

[De vuelta al principio...](#apis)

</br>

### currentTVProviderDialog {#presentTvDialog}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler después de llamar a[getAuthentication()](#getAuthN) si el solicitante actual admite al menos un MVPD con compatibilidad con SSO.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: resultado de los flujos de SSO</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v2.0+

**Parámetros**:

* viewController: representa el cuadro de diálogo SSO de Apple. Este viewController debe mostrarse en la pantalla.

**Activado por:** [`getAuthentication`](#getAuthN)

**Más información:** [Inicio de sesión único de iOS/tvOS](#presentTvDialog)

[De vuelta al principio...](#apis)

</br>

### dismissTVProviderDialog {#dismissTvDialog}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler después de que el usuario cierre el cuadro de diálogo de SSO de Apple.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: resultado de los flujos de SSO</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v2.0+

**Parámetros**:

* viewController: representa el cuadro de diálogo SSO de Apple. Este viewController debe eliminarse de la pantalla.

**Activado por:** Acción del usuario

**Más información:** [Inicio de sesión único de iOS/tvOS](#presentTvDialog)

[De vuelta al principio...](#apis)

</br>

### setMetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler que envía los metadatos solicitados mediante un [`getMetadata:`](#getMeta) llamada a .

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Llamada de retorno: resultado de la solicitud de recuperación de metadatos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setMetadataStatus:(id)metadata
                 encrypted:(bool)encrypted 
                    forKey:(int)key 
              andArguments:(NSDictionary *)arguments; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidad:** v1.0+

**Parámetros**:

* *metadata*: Los metadatos solicitados. Este valor es un `NSString` en el caso de los metadatos estáticos (TTL de autenticación, TTL de autorización, ID de dispositivo).  Es un objeto complejo al solicitar metadatos específicos del usuario. Este objeto complejo suele ser la representación Objective-C de una carga útil JSON (por ejemplo, &#39;{&quot;street&quot;: &quot;Avenida principal&quot;, &quot;edificios&quot;: [&quot;150&quot;, &quot;320&quot;]}&#39; se traduce en Objective-C como NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;, &quot;blocks&quot; -> NSArray(&quot;150&quot;, &quot;320&quot;)).   Objeto JSON de metadatos de ejemplo:

```JSON
        {
            updated: 1334243471,
            encrypted: ["encryptedProp"],
            data: {
                zip: ["12345", "34567"],
                maxRating: { 
                    "MPAA": "PG-13",
                    "VCHIP": "TV-Y", 
                    "URL": "http://exam.pl/e/manage/ratings"
                },
                householdID: "3456",
                userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
                channelID: ["channel-1", "channel-2"]
            }
```

* *cifrados*: Valor booleano que especifica si los metadatos recuperados están cifrados o no. Este parámetro es significativo solo para solicitudes de metadatos de usuario, no tiene significado para metadatos estáticos (por ejemplo, TTL de autenticación) que siempre se reciben sin encriptar. Si este parámetro se establece en true, corresponde al programador obtener el valor de los metadatos de usuario sin encriptar realizando un descifrado RSA utilizando la clave privada de lista blanca (la misma clave privada que se usa para firmar el ID del solicitante en la variable [`setRequestor:setSignedRequestorId:`](#setReq) y `setRequestor:setSignedRequestorId:serviceProviders: `llamadas a ).

* *key*: Clave utilizada para formular la solicitud de recuperación de metadatos.

* *argumentos*: El mismo diccionario que se pasó a [`getMetadata:`](#getMeta) llamada a . Esto se proporciona para permitir que la aplicación coincida con las solicitudes con las respuestas.

**Activado por:** [`getMetadata:`](#getMeta)

**Más información:** [Metadatos de usuario](/help/authentication/user-metadata.md)


[De vuelta al principio...](#apis)

</br>

### MVPD {#mvpd}

**Archivo:** AccessEnabler/headers/model/MVPD.h

**Descripción** Describe el objeto MVPD. Se puede utilizar para obtener información sobre las propiedades de MVPD.

**Disponibilidad:** v1.0+ [la propiedad boardingStatus está disponible en v2.2] 

**Propiedades**:

* ID (NSString): El ID de MVPD.
* (NSString) displayName - El nombre de MVPD. [Debe utilizarse para mostrarse en el selector]
* LogoURL (NSString) - La dirección del logotipo de MVPD.
* (BOOL) enablePlatformServices : si es verdadero, el MVPD admite servicios SSO como [Apple SSO](#presentTvDialog).
* (NSString) boardingStatus : puede tener 3 valores:
   * nil - El MVPD no es compatible con el SSO de Apple.
   * SELECTOR : El MVPD puede aparecer en el selector de Apple, pero el flujo de autenticación se realiza mediante Adobe.
   * COMPATIBLE: El MVPD es totalmente compatible con Apple y utilizará el token SSO de Apple.

[De vuelta al principio...](#apis)

</br>

## Seguimiento de eventos {#tracking}

AccessEnabler déclencheur una llamada de retorno adicional que no está necesariamente relacionada con los flujos de derechos. Implementación de [`sendTrackingData()`](#sendTracking) la función de llamada de retorno es opcional, pero permite a la aplicación rastrear eventos específicos y compilar estadísticas como el número de intentos de autenticación/autorización correctos/fallidos. 

### sendTrackingData:forEventType: {#sendTracking}

**Archivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descripción** Llamada de retorno activada por AccessEnabler que indica a la aplicación la aparición de varios eventos, como la finalización/el fallo de los flujos de autenticación/autorización. Con la autenticación de Primetime 1.6, el tipo de dispositivo, el tipo de cliente AccessEnabler y el sistema operativo reciben los informes de [`sendTrackingData()`](#sendTracking). La variable [`sendTrackingData()`](#sendTracking) la rellamada sigue siendo compatible con versiones anteriores.

**Llamada de retorno: seguimiento de eventos**

```
(void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event;
```

**Disponibilidad:** v1.0+

**Nota:** El tipo de dispositivo y el sistema operativo se derivan del uso de una biblioteca Java pública (<http://java.net/projects/user-agent-utils>) y la cadena del agente de usuario. Tenga en cuenta que esta información se proporciona solamente como una forma granular de desglosar las métricas operativas en categorías de dispositivos, pero ese Adobe no puede asumir ninguna responsabilidad por los resultados incorrectos. Utilice la nueva funcionalidad en consecuencia.

* Valores posibles para el tipo de dispositivo:
   * `computer`
   * `tablet`
   * `mobile`
   * `gameconsole`
   * `unknown`

* Valores posibles del tipo de cliente AccessEnabler:
   * `flash`
   * `html5`
   * `ios`
   * `android`


**Parámetros**:

* *evento*: el código del evento que se está rastreando. Existen tres tipos de eventos de seguimiento posibles:
   * **authorizationDetection:** cada vez que se devuelve una solicitud de token de autorización (evento `TRACKING_AUTHORIZATION`)
   * **authenticationDetection:** cada vez que se produce una comprobación de autenticación (el evento es `TRACKING_AUTHENTICATION`)
   * **mvpdSelection:** cuando el usuario selecciona un MVPD en el formulario de selección de MVPD (el evento es `TRACKING_GET_SELECTED_PROVIDER`)
* *data*: datos adicionales asociados al evento registrado. Estos datos se presentan en forma de una lista de valores.

**Activado por:** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN), `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ), `setSelectedProvider:`

Instrucciones para interpretar los valores de la variable *data* matriz:

* Para trackingEventType `TRACKING_AUTHENTICATION:`
   * **0** - Si la solicitud del token se ha realizado correctamente (true/false) y si se ha realizado correctamente:
   * **1** - Cadena de ID de MVPD
   * **2** - GUID (con hash md5)
   * **3** - Token ya en la caché (true/false)
   * **4** - Tipo de dispositivo
   * **5** - Tipo de cliente AccessEnabler
   * **6** - Tipo de sistema operativo

* Para trackingEventType `TRACKING_AUTHORIZATION:`
   * **0** - Si la solicitud del token se ha realizado correctamente (true/false) y si se ha realizado correctamente:
   * **1** - ID de MVPD
   * **2** - GUID (con hash md5)
   * **3** - Token ya en la caché (true/false)
   * **4** - Error
   * **5** - Detalles
   * **6** - Tipo de dispositivo
   * **7** - Tipo de cliente AccessEnabler
   * **8** - Tipo de sistema operativo
* Para trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
   * **0** - ID del MVPD seleccionado actualmente
   * **1** - Tipo de dispositivo
   * **2** - Tipo de cliente AccessEnabler
   * **3** - Tipo de sistema operativo

</br>

## Información relacionada {#related}

* [Guía de integración de iOS](/help/authentication/iostvos-sdk-cookbook.md)
* [Información general técnica de iOS](/help/authentication/iostvos-sdk-overview.md)
* [Flujo de derechos](/help/authentication/entitlement-flow.md)
   <!--* [Tracking Data in Primetime authentication](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)-->
