---
title: Referencia de API del SDK de JavaScript
description: Referencia de API del SDK de JavaScript
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---

# Referencia de API del SDK de JavaScript {#javascript-sdk-api-reference}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Referencia de API {#api-reference}

Estas funciones inician solicitudes de interacción con una MVPD. Todas las llamadas son asincrónicas; debe implementar [callbacks](#callbacks) para gestionar las respuestas:

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor (inRequestorID, extremos, opciones){#setrequestor(inRequestorID,endpoints,options)}

**Descripción:** Identifica el sitio desde el que se originan las solicitudes.  Debe realizar esta llamada antes que cualquier otra llamada de API en una sesión de comunicación.

**Parámetros:**

- *inRequestorID* - El identificador único que el Adobe asignó al sitio de origen durante el registro.

- *puntos finales* - Este parámetro es opcional. Puede tener uno de los siguientes valores:

   - Matriz que permite especificar extremos para los servicios de autenticación y autorización proporcionados por Adobe (se pueden utilizar distintas instancias para la depuración). En caso de que se proporcionen varias direcciones URL, la lista de MVPD estará compuesta por los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD. De forma predeterminada (si no se especifica ningún valor), se utiliza el proveedor de servicios de Adobe (<http://sp.auth.adobe.com/>).

  Ejemplo:
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`

- *opciones* : objeto JSON que contiene el valor ID de aplicación, el valor ID de visitante, la configuración sin actualización (cierre de sesión de inicio de sesión en segundo plano) y la configuración de MVPD (iFrame). Todos los valores son opcionales.
   1. Si se especifica, se informará del ID de visitante de Experience Cloud en todas las llamadas de red realizadas por la biblioteca. El valor se puede utilizar posteriormente en informes de análisis avanzados.
   2. Si se especifica el identificador único de la aplicación:`applicationId` : el valor se agregará a todas las llamadas subsiguientes realizadas por la aplicación como parte del encabezado HTTP X-Device-Info. Este valor se puede obtener posteriormente de [ESM](/help/authentication/entitlement-service-monitoring-overview.md) informes que utilicen la consulta adecuada.

  **Nota:** Todas las claves JSON distinguen entre mayúsculas y minúsculas.

  Ejemplo:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- El programador puede anular la configuración de MVPD configurada en la autenticación de Adobe Primetime, especificando si se requiere un iFrame o no para el inicio de sesión (*iFrameRequired* ) y las dimensiones de iFrame (*iFrameWidth* y *iFrameHeight* teclas). El objeto JSON tiene la siguiente plantilla:

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```


Todas las claves de nivel superior de la plantilla anterior son opcionales y tienen valores predeterminados (*backgroundLogin*, *backgroundLogut* son false de forma predeterminada y mvpdConfig es null (lo que significa que no se anula ninguna configuración de MVPD).


- **Nota**: La especificación de valores o tipos no válidos para los parámetros anteriores dará como resultado un comportamiento indefinido.



Esta es una configuración de ejemplo para el siguiente escenario: activación del inicio de sesión y cierre de sesión sin actualización, cambio de MVPD1 al inicio de sesión de redirección de página completo (no iFrame) y MVPD2 al inicio de sesión de iFrame con anchura=500 y altura=300:

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**Llamadas activadas:** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[Volver al principio](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**Descripción:** Solicita autorización para el recurso especificado. Cada vez que un cliente intente acceder a un recurso autorizable, llame a esta función para obtener un token de autorización de corta duración del Habilitador de acceso. Los ID de recurso se acuerdan con la autorización de la MVPD.

Utiliza el token de autenticación en caché para el cliente actual. Si no se encuentra ese token, inicia primero el proceso de autenticación y, a continuación, continúa con la autorización.

**Parámetros:**

- `inResourceID` : ID del recurso para el que el usuario solicita autorización.
- `redirect_url` - Opcionalmente, proporcione una URL de redireccionamiento, de modo que el proceso de autorización de la MVPD devuelva al usuario a esa página en lugar de a la página desde la cual se inició la autorización.


**Llamadas activadas:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) en caso de éxito, [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) en caso de fallo

>[!CAUTION]
>
>Utilice checkAuthorization() en lugar de getAuthorization() siempre que sea posible. El método getAuthorization() iniciará un flujo de autenticación completo (si el usuario no está autenticado) y esto podría llevar a una implementación complicada por parte del programador.

</b>

[Volver al principio](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**Descripción:** Solicita autenticación para el cliente actual. Normalmente se llama en respuesta a un clic en un botón de inicio de sesión. Busca un token de autenticación en caché para el cliente actual. Si no se encuentra ese token, inicia el proceso de autenticación. Esto invoca el cuadro de diálogo de selección de proveedor predeterminado o personalizado y, a continuación, utiliza el proveedor seleccionado para redirigir a la interfaz de inicio de sesión de la MVPD.

Si se realiza correctamente, crea y almacena un token de autenticación para el usuario. Si la autenticación falla, el proveedor devuelve un mensaje de error apropiado a su [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) devolución de llamada.

**Parámetros:**

- redirect_url: Opcionalmente, proporcione una URL de redireccionamiento para que el proceso de autenticación de MVPD devuelva al usuario a esa página en lugar de a la página desde la que se inició la autenticación.

**Llamadas activadas:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Volver al principio](#top)

</br>

## checkAuthN {#checkauthn}

**Descripción:** Comprueba el estado de autenticación actual del cliente actual.  No asociado a ninguna interfaz de usuario.

**Llamadas activadas:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[Volver al principio](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**Descripción:** La aplicación utiliza este método para comprobar el estado de autorización del cliente actual y del recurso dado. Se inicia comprobando primero el estado de autenticación. Si no se autentica, se activa la llamada de retorno tokenRequestFailed() y se cierra el método. Si el usuario está autenticado, también almacena en déclencheur el flujo de autorización. Consulte los detalles en la [getAuthorization()](método #getAuthZ.

>[!TIP]
>
> **Uso de funciones de comprobación de estado**  No es necesario comprobar el estado de la autenticación o la autorización antes de solicitar la autorización. Puede llamar a estas funciones, por ejemplo, para actualizar su propia visualización de estado. No los utilice cuando requiera la interacción del usuario.

**Parámetros:**

- `inResourceID` : ID del recurso para el que el usuario solicita autorización.


**Llamadas activadas:**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**Descripción:** Solicita el estado de autorización de &quot;comprobación preliminar&quot; para una lista de recursos.

**Parámetros:**

- *recursos*: el parámetro resources es una matriz de recursos para los que se debe comprobar la autorización. Cada elemento de la lista debe ser una cadena que represente el ID de recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso de la variable `getAuthorization()` llamada, es decir, es un valor acordado establecido entre el Programador y el MVPD, o un fragmento RSS de medios.

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

Esta variante de API está disponible a partir de la versión 4.0 del SDK de JS


**Parámetros:**

- *recursos*: el parámetro resources es una matriz de recursos para los que se debe comprobar la autorización. Cada elemento de la lista debe ser una cadena que represente el ID de recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso de la variable `getAuthorization()` llamada, es decir, es un valor acordado establecido entre el Programador y el MVPD, o un fragmento RSS de medios.

- *escondrijo*: Si se debe utilizar la caché interna al comprobar si hay recursos autorizados previamente. Es un parámetro opcional, de forma predeterminada **true**. Si es true, el comportamiento es idéntico al de la API anterior, lo que significa que las llamadas posteriores a esta función utilizarán una caché interna para resolver el recurso autorizado previamente. Pasar **false** para este parámetro deshabilitará la caché interna, lo que dará como resultado una llamada al servidor cada vez que el parámetro **checkPreauthorizedResources** Se llama a la API.

**Llamadas activadas:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)

</br>

[Volver al principio](#top)
</br>

## getMetadata(Key) {#getMetadata}

**Descripción:** Recupera información expuesta como metadatos por la biblioteca del Habilitador de acceso.

Existen dos tipos de metadatos:

- **Estático** (TTL del token de autenticación, TTL del token de autorización e ID del dispositivo)
- **Metadatos del usuario** (Esto incluye información específica del usuario que se pasa de la MVPD al dispositivo del usuario durante los flujos de autenticación o autorización)

**Más información:** [Metadatos del usuario](#UserMetadata)

**Parámetros:**

- *key*: un ID que especifica los metadatos solicitados:
   - Si la clave es `"TTL_AUTHN",` a continuación, se realiza la consulta para obtener el tiempo de caducidad del token de autenticación.

   - Si la clave es `"TTL_AUTHZ"` y params es una matriz que contiene el id de recurso como una cadena. A continuación, se realiza la consulta para obtener la hora de caducidad del token de autorización asociado al recurso especificado.

   - Si la clave es `"DEVICEID"` a continuación, se realiza la consulta para obtener el id del dispositivo actual. Tenga en cuenta que esta función está desactivada de forma predeterminada y los programadores deben ponerse en contacto con el Adobe para obtener información sobre la habilitación y las tarifas.

   - Si la clave es de la siguiente lista de tipos de metadatos de usuario, se envía a un objeto JSON que contiene los metadatos de usuario correspondientes [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) función de llamada de retorno:

   - `"zip"` - Código postal

   - `"encryptedZip"` - Código postal cifrado

   - `"householdID"` - Identificador del hogar. En caso de que una MVPD no admita subcuentas, será idéntico a userID.

   - `"maxRating"` - Calificación parental máxima para el usuario

   - `"userID"` : el identificador de usuario. En el caso de que una MVPD admita subcuentas y el usuario no sea la cuenta principal, userID será diferente a householdID.

   - `"channelID"` - La lista de canales que el usuario puede ver

   - `"is_hoh"` - Indicador que identifica si un usuario es el cabeza de familia

   - `"encryptedZip"` - Código postal cifrado

   - `"typeID"` - Indicador que identifica si la cuenta de usuario es la cuenta principal/secundaria

   - `"primaryOID"` - Identificador del hogar

   - `"postalCode"` - Similar al código postal

   - `"acctID"` - ID de cuenta

   - `"acctParentID"` - ID principal de la cuenta

  **Nota**: los metadatos de usuario reales disponibles para un programador dependen de lo que una MVPD ponga a disposición.  Consulte [Metadatos del usuario](#UserMetadata) para la lista actual de metadatos de usuario disponibles.


Por ejemplo:

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```


**Llamadas activadas:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[Volver al principio](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**Descripción:** Llame a esta función cuando el usuario haya seleccionado una MVPD en la interfaz de usuario de selección de proveedores para enviar la selección de proveedores al Habilitador de acceso o llame a esta función con un parámetro nulo en caso de que el usuario descarte la interfaz de usuario de selección de proveedores sin seleccionar un proveedor.

**Llamadas activadas:**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Volver al principio](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**Descripción:** Recupera los resultados de la selección del cliente en el cuadro de diálogo de selección del proveedor. Esto se puede utilizar en cualquier momento después de la comprobación de autenticación inicial.

Esta función es asincrónica y devuelve su resultado a su `selectedProvider()` función de llamada de retorno.

- **MVPD** La MVPD seleccionada actualmente, o nula si no se ha seleccionado ninguna MVPD.
- **AE_State** El resultado de la autenticación para el cliente actual es uno de &quot;Nuevo usuario&quot;, &quot;Usuario no autenticado&quot; o &quot;Usuario autenticado&quot;

**Llamadas activadas:** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[Volver al principio](#top)

</br>

## cierre de sesión {#logout}

**Descripción:** Cierra la sesión del cliente actual y borra toda la información de autenticación y autorización de ese usuario. Elimina todos los tokens authN y authZ del sistema del cliente.

**Llamadas activadas:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br>

[Volver al principio](#top)

</br>

## Definición de llamada {#calllback-definitions}

Debe implementar estas llamadas de retorno para gestionar las respuestas a sus llamadas de solicitud asincrónicas:

- [rightLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## rightLoaded() {#entitlementLoaded}

**Descripción:** Se activa cuando el Habilitador de acceso ha completado la inicialización y está listo para recibir solicitudes. Implemente esta llamada de retorno para saber cuándo puede iniciar la comunicación con la API del Habilitador de acceso.
</br>

[Volver al principio](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**Descripción:** Implemente esta llamada de retorno para recibir la información de configuración y la lista de MVPD.

**Parámetros:**

- *configXML*: objeto xml que contiene la configuración del SOLICITANTE actual, incluida la lista de MVPD.


**Activado por:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[Volver al principio](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**Descripción:** Implemente esta llamada de retorno para invocar su propia interfaz de usuario de selección de proveedor personalizada. El cuadro de diálogo debe utilizar el nombre para mostrar (y el logotipo opcional) para proporcionar las opciones del cliente. Cuando el cliente haya realizado una elección y haya cerrado el cuadro de diálogo, envíe el ID asociado del proveedor seleccionado en la llamada a *setSelectedProvider()*.

**Parámetros:**

- *proveedores* - Una matriz de objetos que representan las MVPD solicitadas:

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**Activado por:** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[Volver al principio](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**Descripción:** Implemente esta llamada de retorno si el usuario ha seleccionado una MVPD que requiere un iFrame en el que mostrar su interfaz de usuario de la página de inicio de sesión de autenticación.

**Activado por:**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [Volver al principio](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**Descripción:** Implemente esta llamada de retorno para recibir el estado de autenticación (1=autenticado o 0=no autenticado) y un mensaje de error descriptivo si se produce algún error al intentar determinar el estado de autenticación (cadena vacía al completar correctamente la comprobación).

>[!NOTE]
> 
>Si utiliza el actual, [Informes de errores avanzados](/help/authentication/error-reporting.md) , puede ignorar el parámetro errorCode enviado a esta función.  Sin embargo, el indicador isAuthenticated sigue siendo útil para rastrear el estado de autenticación de un usuario en el flujo de derechos


**Parámetros:**

- *isAuthenticated* - Proporciona el estado de autenticación: 1 (autenticado) o 0 (no autenticado).
- *errorCode* - Cualquier error que se haya producido al determinar el estado de autenticación. Una cadena vacía si no hay ninguna.


**Activado por:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[Volver al principio](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>El tipo de dispositivo y el sistema operativo se derivan del uso de una biblioteca Java pública (<http://java.net/projects/user-agent-utils>) y la cadena del agente de usuario. Tenga en cuenta que esta información se proporciona solo como una forma grosera de desglosar las métricas operativas en categorías de dispositivos, pero que ese Adobe no puede responsabilizarse de los resultados incorrectos. Utilice la nueva funcionalidad en consecuencia.

**Descripción:** Implemente esta llamada de retorno para recibir datos de seguimiento cuando se produzcan eventos específicos. Puede utilizar esto, por ejemplo, para realizar un seguimiento de cuántos usuarios han iniciado sesión con las mismas credenciales. El seguimiento no se puede configurar actualmente. Con la autenticación de Adobe Primetime 1.6, `sendTrackingData()` también informa de información sobre el dispositivo, el cliente del Habilitador de acceso y el tipo de sistema operativo. El `sendTrackingData()` la devolución de llamada sigue siendo compatible con versiones anteriores.

- Valores posibles para el tipo de dispositivo:
   - ordenador
   - tableta
   - mobile
   - consola de juegos
   - desconocido

- Valores posibles para el tipo de cliente del Habilitador de acceso:
   - html5
   - ios
   - androide


Pasa el tipo de evento y una matriz de información asociada. Los tipos de eventos son:

| mvpdSelection | El usuario seleccionó una MVPD en un cuadro de diálogo de selección de proveedores. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | Se ha completado una comprobación de autenticación. |
| authorizationDetection | Se completó una solicitud de autorización. |

</br>
Los datos son específicos para cada tipo de evento:
</br>

| Tipo de evento (cadena) | Datos (matriz) |
|:--- | :--- |
| mvpdSelection | 0: MVPD seleccionada |
|  | 1: Tipo de dispositivo |
|  | 2: Tipo de cliente del Habilitador de acceso |
|  | 3: SO |
| authenticationDetection | 0: Si la solicitud de token se realizó correctamente (verdadero/falso) |
|  | 1: ID de MVPD |
|  | 2: GUID |
|  | 3: El token ya está en la caché (verdadero/falso) |
|  | 4: Tipo de dispositivo |
|  | 5. Tipo de cliente del Habilitador de acceso |
|  | 6: SO |
| authorizationDetection | 0: Si la solicitud de token se realizó correctamente (verdadero/falso) |
|  | 1: ID de MVPD |
|  | 2: GUID |
|  | 3: El token ya está en la caché (verdadero/falso) |
|  | 4: Error |
|  | 5: Detalles |
|  | 6: Tipo de dispositivo |
|  | 7: Tipo de cliente del Habilitador de acceso |
|  | 8: SO |


**Activado por:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[Volver al principio](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**Descripción:** Implemente esta llamada de retorno para recibir el token de medios de corta duración (inToken) y el ID del recurso (inRequestedResourceID) para el que se realizó una solicitud de autorización o de autorización de comprobación y que se completó correctamente.

**Activado por:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[Volver al principio](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**Descripción:** Implemente esta llamada de retorno para que se señale cuando haya fallado una autorización o una solicitud de autorización de comprobación. Opcionalmente, un MVPD puede utilizarlo para proporcionar un mensaje personalizado que mostrará el programador.

>[!IMPORTANT]
>
>Esta función de llamada de retorno forma parte del sistema de informes de errores de autenticación de Primetime original más antiguo. Se conserva para la compatibilidad con versiones anteriores, pero no es necesario utilizar esta función en absoluto si ha implementado sus propias devoluciones de llamada mediante el sistema actual de informes de errores avanzados. El nuevo sistema de informes de errores proporciona información más detallada sobre por qué ha fallado una autorización (u otra operación), junto con cursos de acción sugeridos para cada tipo de error o advertencia.

**Parámetros:**

- *inRequestedResourceID* : cadena que proporciona el ID de recurso que se utilizó en la solicitud de autorización.
- *inRequestErrorCode* - Una cadena que muestra el código de error de autenticación de Adobe Primetime, indicando el motivo del error; los valores posibles son &quot;Error de usuario no autenticado&quot; y &quot;Error de usuario no autorizado&quot;; para obtener más detalles, consulte &quot;Códigos de error de devolución de llamada&quot; a continuación.
- *inRequestDetailedErrorMessage* : una cadena descriptiva adicional adecuada para su visualización. Si esta cadena descriptiva no está disponible por ningún motivo, la autenticación de Adobe Primetime envía una cadena vacía **(&quot;&quot;)**.  Un MVPD puede utilizarla para transmitir mensajes de error personalizados o mensajes relacionados con las ventas. Por ejemplo, si se deniega a un suscriptor la autorización para un recurso, la MVPD podría responder con un `*inRequestDetailedErrorMessage*` como: **&quot;Actualmente no tienes acceso a este canal en tu paquete. Si desea actualizar el paquete, haga clic \*aquí\*.&quot;** La autenticación de Adobe Primetime pasa el mensaje a través de esta llamada de retorno al sitio del programador. A continuación, el programador tiene la opción de mostrarlo u omitirlo. La autenticación de Adobe Primetime también puede utilizar `*inRequestDetailedErrorMessage*` para notificar al programador de la condición que podría haber producido un error. Por ejemplo, **&quot;Error de red al comunicarse con el servicio de autorización del proveedor&quot;.**



**Activado por:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[Volver al principio](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**Descripción:** Llamada de retorno activada por el Habilitador de acceso que entrega la lista de recursos autorizados devuelta después de una llamada a `checkPreauthorizedResources()`.

**Parámetros:**

- *authorizedResources*: la lista de recursos autorizados.

**Activado por:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[Volver al principio](#top)

</br>

## setMetadataStatus(clave, cifrado, datos) {#setMetadataStatus(key,encrypted,data)}

**Descripción:** Llamada de retorno activada por el activador de acceso que entrega los metadatos solicitados mediante una `getMetadata()` llamada.

**Más información:** [Metadatos del usuario](#userMetadata)

**Parámetros:**

- *key (String)*: La clave de los metadatos para los que se realizó la solicitud.
- *cifrado (booleano)*: Un indicador que indica si el &quot;valor&quot; está cifrado o no. Si es &quot;true&quot;, &quot;value&quot; será en realidad una representación cifrada con web JSON del valor real.
- *data (objeto JSON)*: un objeto JSON con la representación de los metadatos. Para solicitudes simples (&#39;`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;), el resultado es una cadena (que representa el TTL de autenticación, el TTL de autorización o el ID de dispositivo). En el caso de una solicitud de metadatos de usuario, el resultado puede ser un objeto primitivo o JSON que represente la carga útil de metadatos. La estructura real de los objetos de metadatos de usuario de JSON es similar a la siguiente:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```


Por ejemplo:

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```


**Activado por:** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[Volver al principio](#top)

</br>

## selectedProvider(resultado) {#selectedProvider(result)}

**Descripción:** Implemente esta llamada de retorno para recibir el MVPD seleccionado actualmente y el resultado de la autenticación del usuario actual ajustado en el `result` parámetro. El `result` El parámetro es un objeto con las siguientes propiedades:

- **MVPD** La MVPD seleccionada actualmente, o nula si no se ha seleccionado ninguna MVPD.
- **AE\_State** El resultado de la autenticación para el usuario actual, uno de &quot;Nuevo usuario&quot;, &quot;Usuario no autenticado&quot; o &quot;Usuario autenticado&quot;

**Activado por:** [getSelectedProvider()](#getSelProv)

</br>

[Volver al principio](#top)

</br>

### Códigos de error de devolución {#callback-error-codes}

| Errores genéricos | |
|:--- | :--- | 
| Error interno | Se ha producido un error del sistema al intentar procesar la solicitud. |
| Error de proveedor no seleccionado | Se produce cuando el cliente cancela en el cuadro de diálogo de selección de proveedores |
| Error de proveedor no disponible | Se produce cuando no hay proveedores disponibles. |

| Errores de autenticación | |
|:--- | :--- | 
| Error de autenticación genérica | Se devuelve cuando el motivo no se conoce o no puede publicarse. |
| Error de autenticación interna | Se ha producido un error del sistema al intentar autenticarse. |
| Error de usuario no autenticado | El usuario no está autenticado. |
| Error de varias solicitudes de autenticación | Se recibieron solicitudes de autenticación adicionales antes de que se completara la primera. |

| Errores de autorización | |
|:--- | :--- | 
| Error de autorización genérica | Se devuelve cuando el motivo no se conoce o no puede publicarse. |
| Error de autorización interna | Se ha producido un error del sistema al intentar autorizar. |
| Error de usuario no autorizado | El cliente no tiene autorización para ver el contenido solicitado. |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[Volver al principio](#top)
