---
title: Referencia de la API del SDK para JavaScript
description: Referencia de la API del SDK para JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---


# Referencia de la API del SDK para JavaScript {#javascript-sdk-api-reference}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Referencia de API {#api-reference}

Estas funciones inician solicitudes de interacción con un MVPD. Todas las llamadas son asíncronas; debe implementar [callbacks](#callbacks) para gestionar las respuestas:

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

**Descripción:** Identifica el sitio desde el que se originan las solicitudes.  Debe realizar esta llamada antes de cualquier otra llamada API en una sesión de comunicación. 

**Parámetros:**

- *inRequestorID* - Identificador único que se asignó al sitio de origen durante el registro.

- *endpoints* - Este parámetro es opcional. Puede ser uno de los siguientes valores:

   - Matriz que le permite especificar puntos finales para los servicios de autenticación y autorización proporcionados por Adobe (se pueden utilizar diferentes instancias para la depuración). En caso de que se proporcionen varias direcciones URL, la lista de MVPD está compuesta por los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD. De forma predeterminada (si no se especifica ningún valor), se utiliza el proveedor de servicios de Adobe (<http://sp.auth.adobe.com/>).

   Ejemplo:
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *opciones* : un objeto JSON que contiene el valor ID de la aplicación, la configuración de actualización del valor del ID del visitante (cierre de sesión en segundo plano) y la configuración de MVPD (iFrame). Todos los valores son opcionales.
   1. Si se especifica, el visitorID del Experience Cloud se registrará en todos los informes de llamadas de red que realice la biblioteca . Posteriormente, el valor se puede usar para informes de análisis avanzados.
   2. Si se especifica el identificador único de la aplicación -`applicationId` : el valor se añade a todas las llamadas posteriores realizadas por la aplicación como parte del encabezado HTTP X-Device-Info. Este valor se puede recuperar posteriormente de [ESM](/help/authentication/entitlement-service-monitoring-overview.md) con la consulta adecuada.

   **Nota:** Todas las claves JSON distinguen entre mayúsculas y minúsculas.

    Ejemplo:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- El programador puede anular la configuración de MVPD configurada en la autenticación de Adobe Primetime especificando si se requiere un iFrame o no para el inicio de sesión (*iFrameRequired* ) y las dimensiones iFrame (*iFrameWidth* y *iFrameHeight* teclas). El objeto JSON tiene la siguiente plantilla:

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
 

Todas las claves de nivel superior de la plantilla anterior son opcionales y tienen valores predeterminados (*backgroundLogin*, *backgroundLogut* son falsos de forma predeterminada, y mvpdConfig es nulo, lo que significa que no se sobrescribe ninguna configuración de MVPD).

 
- **Nota**: Si especifica valores o tipos no válidos para los parámetros anteriores, se obtendrá un comportamiento no definido.

 

A continuación se muestra un ejemplo de configuración para el siguiente escenario: activar el inicio de sesión y el cierre de sesión sin actualizar, cambiar MVPD1 a inicio de sesión con redireccionamiento de página completo (no iFrame) y MVPD2 a inicio de sesión con iFrame con width=500 y height=300:

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


**Llamadas de retorno activadas:** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[Volver al principio](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**Descripción:** Solicita autorización para el recurso especificado. Cada vez que un cliente intenta acceder a un recurso autorizado, llame a esta función para obtener un token de autorización de duración corta desde Access Enabler. Los ID de recurso se acuerdan con el MVPD que proporciona la autorización.

Utiliza el token de autenticación en caché para el cliente actual. Si no se encuentra dicho token, inicia el proceso de autenticación primero y, a continuación, continúa con la autorización.\
 
**Parámetros:**

- `inResourceID` : ID del recurso para el que el usuario solicita la autorización.
- `redirect_url` - Opcionalmente, proporcione una URL de redireccionamiento, de modo que el proceso de autorización de MVPD devuelva al usuario a esa página en lugar de a la página desde la cual se inició la autorización.


**Llamadas de retorno activadas:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) sobre el éxito, [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) en caso de fallo

>[!CAUTION]
>
>Utilice checkAuthorization() en lugar de getAuthorization() siempre que sea posible. El método getAuthorization() iniciará un flujo de autenticación completo (si el usuario no está autenticado) y esto podría llevar a una implementación complicada por parte del programador.

</b>

[Volver al principio](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**Descripción:** Solicita autenticación para el cliente actual. Normalmente se llama en respuesta a un clic en un botón de inicio de sesión. Comprueba si hay un token de autenticación en caché para el cliente actual. Si no se encuentra dicho token, inicia el proceso de autenticación. Esto invoca el cuadro de diálogo predeterminado o personalizado de selección de proveedores y luego utiliza el proveedor seleccionado para redirigir a la interfaz de inicio de sesión de MVPD.

Cuando se realiza correctamente, crea y almacena un token de autenticación para el usuario. Si la autenticación falla, el proveedor devuelve un mensaje de error apropiado a su [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) llamada de retorno.

**Parámetros:**

- redirect_url : Opcionalmente, proporcione una URL de redireccionamiento, de modo que el proceso de autenticación de MVPD devuelva al usuario a esa página en lugar de a la página desde la que se inició la autenticación.

 **Llamadas de retorno activadas:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Volver al principio](#top)

</br>

## checkAuthN {#checkauthn}

**Descripción:** Comprueba el estado de autenticación actual del cliente actual.  No está asociado a ninguna IU.

**Llamadas de retorno activadas:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[Volver al principio](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**Descripción:** La aplicación utiliza este método para comprobar el estado de autorización del cliente actual y del recurso dado. Se inicia comprobando primero el estado de autenticación. Si no se autentica, se activa la llamada de retorno tokenRequestFailed() y el método se cierra. Si el usuario está autenticado, también déclencheur el flujo de autorización. Consulte los detalles sobre [getAuthorization()](#getAuthZ método ).

>[!TIP]
>
> **Uso de funciones de comprobación de estado**  No es necesario que compruebe el estado de la autenticación o la autorización antes de solicitar la autorización. Puede llamar a estas funciones, por ejemplo, para actualizar su propia visualización de estado. No las utilice cuando requiera interacción del usuario.

**Parámetros:**

- `inResourceID` : ID del recurso para el que el usuario solicita la autorización.

 
**Llamadas de retorno activadas:**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**Descripción:** Solicita el estado de autorización de &quot;comprobación previa&quot; para una lista de recursos.

**Parámetros:**

- *recursos*: El parámetro resources es una matriz de recursos para los que se debe comprobar la autorización. Cada elemento de la lista debe ser una cadena que represente el ID del recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso en la variable `getAuthorization()` es decir, es un valor acordado establecido entre el Programador y el MVPD, o un fragmento RSS de medios. 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

Esta variante de API está disponible a partir de la versión 4.0 del SDK para JS


**Parámetros:**

- *recursos*: El parámetro resources es una matriz de recursos para los que se debe comprobar la autorización. Cada elemento de la lista debe ser una cadena que represente el ID del recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso en la variable `getAuthorization()` es decir, es un valor acordado establecido entre el Programador y el MVPD, o un fragmento RSS de medios. 

- *cache*: Si desea utilizar la caché interna al comprobar los recursos preautorizados. Este es un parámetro opcional, de forma predeterminada, con el valor **true**. Si el valor es true, el comportamiento es idéntico al de la API anterior, lo que significa que las llamadas subsiguientes a esta función utilizarán una caché interna para resolver el recurso preautorizado. Pasar **false** para este parámetro deshabilitará la caché interna, lo que dará como resultado una llamada al servidor cada vez que se utilice la variable **checkPreauthorizedResources** Se llama a la API de .

**Llamadas de retorno activadas:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[Volver al principio](#top)
</br>

## getMetadata(Key) {#getMetadata}

**Descripción:** Recupera información expuesta como metadatos por la biblioteca de Access Enabler.

Existen dos tipos de metadatos: 

- **Estático** (TTL de token de autenticación, TTL de token de autorización e ID de dispositivo) 
- **Metadatos de usuario** (Esto incluye información específica del usuario que se pasa desde el MVPD al dispositivo del usuario durante los flujos de autenticación y/o autorización)

**Más información:** [Metadatos de usuario](#UserMetadata)

**Parámetros:**

- *key*: Un id que especifica los metadatos solicitados:
   - Si la clave es `"TTL_AUTHN",` a continuación, la consulta se realiza para obtener el tiempo de caducidad del token de autenticación.

   - Si la clave es `"TTL_AUTHZ"` y params es una matriz que contiene el id del recurso como una cadena, entonces la consulta se realiza para obtener el tiempo de caducidad del token de autorización asociado al recurso especificado.

   - Si la clave es `"DEVICEID"` a continuación, la consulta se realiza para obtener el id del dispositivo actual. Tenga en cuenta que esta función está deshabilitada de forma predeterminada y los programadores deben ponerse en contacto con Adobe para obtener información sobre la habilitación y las tarifas.

   - Si la clave es de la siguiente lista de tipos de metadatos de usuario, se envía un objeto JSON que contiene los metadatos de usuario correspondientes al [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) función de llamada de retorno:

   - `"zip"` - Código postal

   - `"encryptedZip"` - Código postal cifrado

   - `"householdID"` - Identificador del hogar. En el caso de que un MVPD no admita subcuentas, esto será idéntico al userID.

   - `"maxRating"` - Clasificación parental máxima para el usuario

   - `"userID"` - El identificador de usuario. En el caso de que un MVPD admita subcuentas y el usuario no sea la cuenta principal, userID será diferente a householdID.

   - `"channelID"` - La lista de canales que el usuario puede ver

   - `"is_hoh"` - Indicador que identifica si un usuario es cabeza de familia

   - `"encryptedZip"` - Código postal cifrado

   - `"typeID"` - Indicador que identifica si la cuenta de usuario es principal/secundaria

   - `"primaryOID"` - Identificador del hogar

   - `"postalCode"` - Similar al código postal

   - `"acctID"` - ID de cuenta

   - `"acctParentID"` - ID principal de la cuenta
   **Nota**: Los metadatos de usuario disponibles para un programador dependen de lo que un MVPD ponga a disposición.  Consulte [Metadatos de usuario](#UserMetadata) para la lista actual de metadatos de usuario disponibles.


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
 

**Llamadas de retorno activadas:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[Volver al principio](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**Descripción:** Llame a esta función cuando el usuario haya seleccionado un MVPD desde la interfaz de usuario de selección de proveedores para enviar la selección de proveedores al activador de acceso o llamar a esta función con un parámetro nulo en caso de que el usuario descarte la interfaz de usuario de selección de proveedores sin seleccionar un proveedor. 

**Llamadas de retorno activadas:**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Volver al principio](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**Descripción:** Recupera los resultados de la selección del cliente en el cuadro de diálogo de selección del proveedor. Esto se puede utilizar en cualquier momento después de la comprobación de autenticación inicial.

Esta función es asíncrona y devuelve su resultado a su `selectedProvider()` función de llamada de retorno.

- **MVPD** El MVPD seleccionado actualmente o nulo si no se ha seleccionado ningún MVPD.
- **AE_State** El resultado de la autenticación para el cliente actual es &quot;Nuevo usuario&quot;, &quot;Usuario no autenticado&quot; o &quot;Usuario autenticado&quot;.

 **Llamadas de retorno activadas:** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[Volver al principio](#top)

</br>

## cierre de sesión {#logout}

**Descripción:** Cierre la sesión del cliente actual y borre toda la información de autenticación y autorización de ese usuario. Elimina todos los tokens authN y authZ del sistema del cliente.

 **Llamadas de retorno activadas:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[Volver al principio](#top)

</br>

## Definición de devolución de llamada {#calllback-definitions}

Debe implementar estas llamadas de retorno para administrar las respuestas a sus llamadas de solicitud asincrónicas:

- [rightsLoaded()](#entitlementloaded-entitlementloaded)
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

## rightsLoaded() {#entitlementLoaded}

**Descripción:** Se activa cuando Access Enabler ha completado la inicialización y está listo para recibir solicitudes. Implemente esta llamada de retorno para saber cuándo puede iniciar la comunicación con la API de Access Enabler.
</br>

[Volver al principio](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**Descripción:** Implemente esta llamada de retorno para recibir la información de configuración y la lista de MVPD.

**Parámetros:**

- *configXML*: objeto xml que contiene la configuración del solicitante actual, incluida la lista de MVPD.

 
**Activado por:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[Volver al principio](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**Descripción:** Implemente esta llamada de retorno para invocar su propia interfaz de usuario de selección de proveedores personalizada. El cuadro de diálogo debe utilizar el nombre para mostrar (y el logotipo opcional) para proporcionar las opciones del cliente. Cuando el cliente haya elegido y descartado el cuadro de diálogo, envíe el ID asociado para el proveedor elegido en la llamada a *setSelectedProvider()*.

**Parámetros:**

- *proveedores* - Una matriz de objetos que representan los MVPD solicitados:

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**Activado por:** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[Volver al principio](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**Descripción:** Implemente esta llamada de retorno si el usuario ha seleccionado un MVPD que requiere un iFrame en el que se muestre su interfaz de usuario de la página de inicio de sesión de autenticación.

**Activado por:**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [Volver al principio](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**Descripción:** Implemente esta llamada de retorno para recibir el estado de autenticación (1=autenticado o 0=no autenticado) y un mensaje de error descriptivo si se produjo algún error al intentar determinar el estado de autenticación (cadena vacía al completar correctamente la comprobación).

>[!NOTE]
> 
>Si utiliza la versión actual, [Informe de errores avanzado](/help/authentication/error-reporting.md) sistema, puede ignorar el parámetro errorCode enviado a esta función.  Sin embargo, el indicador isAuthenticated sigue siendo útil para rastrear el estado de autenticación de un usuario en el flujo de derechos


**Parámetros:**

- *isAuthenticated* - Proporciona estado de autenticación: 1 (autenticado) o 0 (no autenticado).
- *errorCode* - Cualquier error que se produjo al determinar el estado de autenticación. Una cadena vacía si no hay ninguna.

 
**Activado por:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[Volver al principio](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>El tipo de dispositivo y el sistema operativo se derivan del uso de una biblioteca Java pública (<http://java.net/projects/user-agent-utils>) y la cadena del agente de usuario. Tenga en cuenta que esta información se proporciona solamente como una forma granular de desglosar las métricas operativas en categorías de dispositivos, pero ese Adobe no puede asumir ninguna responsabilidad por los resultados incorrectos. Utilice la nueva funcionalidad en consecuencia.

**Descripción:** Implemente esta llamada de retorno para recibir datos de seguimiento cuando ocurran eventos específicos. Puede usar esto, por ejemplo, para realizar un seguimiento de cuántos usuarios han iniciado sesión con las mismas credenciales. El seguimiento no se puede configurar actualmente. Con la autenticación de Adobe Primetime 1.6, `sendTrackingData()` también informa de información sobre el dispositivo, el cliente Access Enabler y el tipo de sistema operativo. La variable `sendTrackingData()` la rellamada sigue siendo compatible con versiones anteriores.\
 
- Valores posibles para el tipo de dispositivo:
   - equipo
   - tableta
   - mobile
   - gameconsole
   - unknown

- Valores posibles del tipo de cliente Access Enabler:
   - html5
   - ios
   - android


Pasa el tipo de evento y una matriz de información asociada. Los tipos de eventos son:

| mvpdSelection | El usuario seleccionó un MVPD en un cuadro de diálogo de selección de proveedores. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | Se completó una comprobación de autenticación. |
| authorizationDetection | Se completó una solicitud de autorización. |

</br>
Los datos son específicos de cada tipo de evento:
</br>

| Tipo de evento (cadena) | Datos (matriz) |
|:--- | :--- |
| mvpdSelection | 0: MVPD seleccionado |
|  | 1: Tipo de dispositivo |
|  | 2: Tipo de cliente de Access Enabler |
|  | 3: Sistema operativo |
| authenticationDetection | 0: Si la solicitud de token se realizó correctamente (true/false) |
|  | 1: ID de MVPD |
|  | 2: GUID |
|  | 3: Token ya en la caché (true/false) |
|  | 4: Tipo de dispositivo |
|  | 5: Tipo de cliente de Access Enabler |
|  | 6: Sistema operativo |
| authorizationDetection | 0: Si la solicitud de token se realizó correctamente (true/false) |
|  | 1: ID de MVPD |
|  | 2: GUID |
|  | 3: Token ya en la caché (true/false) |
|  | 4: Error |
|  | 5: Detalles |
|  | 6: Tipo de dispositivo |
|  | 7: Tipo de cliente de Access Enabler |
|  | 8: Sistema operativo |


**Activado por:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[Volver al principio](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**Descripción:** Implemente esta llamada de retorno para recibir el token de medios de corta duración (inToken) y el ID del recurso (inRequestedResourceID)para el que se realizó una solicitud de autorización o de autorización de comprobación y se completó correctamente.

**Activado por:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[Volver al principio](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**Descripción:** Implemente esta llamada de retorno para que se señale cuando haya fallado una solicitud de autorización o de autorización de comprobación. Puede ser usado opcionalmente por un MVPD para proporcionar un mensaje personalizado que será mostrado por el Programador.

>[!IMPORTANT]
>
>Esta función de llamada de retorno forma parte del antiguo sistema original de informes de errores de autenticación de Primetime. Se conserva para la compatibilidad con versiones anteriores, pero no es necesario utilizar esta función si ha implementado sus propias llamadas de retorno utilizando el sistema actual de informes avanzados de errores. El nuevo sistema de informes de errores proporciona información más detallada sobre por qué falló una autorización (u otra operación), junto con los cursos de acción sugeridos para cada tipo de error o advertencia.

**Parámetros:**

- *inRequestedResourceID* - Una cadena que proporciona el ID de recurso que se utilizó en la solicitud de autorización.
- *inRequestErrorCode* - Una cadena que muestra el código de error de autenticación de Adobe Primetime, indicando el motivo del error; los valores posibles son &quot;Error autenticado del usuario&quot; y &quot;Error no autorizado del usuario&quot;; para obtener más información, consulte &quot;Códigos de error de devolución de llamada&quot; a continuación.
- *inRequestDetailedErrorMessage* - Una cadena descriptiva adicional adecuada para la visualización. Si esta cadena descriptiva no está disponible por ningún motivo, la autenticación de Adobe Primetime envía una cadena vacía **(&quot;&quot;&quot;)**.  Un MVPD puede utilizarlo para pasar mensajes de error personalizados o mensajes relacionados con las ventas. Por ejemplo, si a un suscriptor se le niega la autorización para un recurso, el MVPD podría responder con un `*inRequestDetailedErrorMessage*` como: **&quot;Actualmente no tiene acceso a este canal en su paquete. Si desea actualizar su paquete, haga clic en \*aquí\*.&quot;** La autenticación de Adobe Primetime pasa el mensaje a través de esta llamada de retorno al sitio del programador. A continuación, el programador tiene la opción de mostrarlo o ignorarlo. La autenticación de Adobe Primetime también puede utilizar `*inRequestDetailedErrorMessage*` para notificar al programador de la condición que podría haber provocado un error. Por ejemplo, **&quot;Error de red al comunicarse con el servicio de autorización del proveedor&quot;.**

 

**Activado por:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[Volver al principio](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**Descripción:** Llamada de retorno activada por Access Enabler que proporciona la lista de recursos autorizados devuelta después de una llamada a `checkPreauthorizedResources()`.

**Parámetros:**

- *authorizedResources*: lista de recursos autorizados.

**Activado por:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[Volver al principio](#top)

</br>

## setMetadataStatus(key, encryption, data) {#setMetadataStatus(key,encrypted,data)}

**Descripción:** Llamada de retorno activada por Access Enabler que envía los metadatos solicitados mediante un `getMetadata()` llamada a .

**Más información:** [Metadatos de usuario](#userMetadata)

**Parámetros:**

- *key (String)*: Clave de los metadatos para los que se realizó la solicitud.
- *cifrados (booleano)*: Un indicador que señala si el &quot;valor&quot; está cifrado o no. Si esto es &quot;true&quot;, entonces &quot;value&quot; será en realidad una representación JSON Web Encrypted del valor real. 
- *data (objeto JSON)*: Un objeto JSON con la representación de los metadatos. Para solicitudes simples (&#39;`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;), el resultado es una cadena (que representa el TTL de autenticación, el TTL de autorización o el ID del dispositivo). En el caso de una solicitud de metadatos de usuario, el resultado puede ser un objeto primitivo o JSON que represente la carga útil de metadatos. La estructura real de los objetos de metadatos de usuario JSON es similar a la siguiente:

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
 

**Activado por:** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[Volver al principio](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**Descripción:** Implemente esta llamada de retorno para recibir el MVPD seleccionado actualmente y el resultado de la autenticación del usuario actual empaquetado en el `result` parámetro. La variable `result` es un objeto con las siguientes propiedades:

- **MVPD** El MVPD seleccionado actualmente o nulo si no se ha seleccionado ningún MVPD.
- **AE\_State** El resultado de la autenticación del usuario actual, uno de &quot;Nuevo usuario&quot;, &quot;Usuario no autenticado&quot; o &quot;Usuario autenticado&quot;

 **Activado por:** [getSelectedProvider()](#getSelProv)

</br>

[Volver al principio](#top)

</br>

### Códigos de error de devolución de llamada {#callback-error-codes}

| Errores genéricos |  |
|:--- | :--- | 
| Error interno | Error del sistema al intentar procesar la solicitud. |
| Error de proveedor no seleccionado | Se produce cuando el cliente se cancela en el cuadro de diálogo de selección del proveedor |
| Error de proveedor no disponible | Se produce cuando no hay proveedores disponibles. |

| Errores de autenticación |  |
|:--- | :--- | 
| Error de autenticación genérico | Se devuelve cuando el motivo no se conoce o no se puede publicar. |
| Error de autenticación interna | Error del sistema al intentar la autenticación. |
| Error autenticado del usuario | El usuario no está autenticado. |
| Error en varias solicitudes de autenticación | Se recibieron solicitudes de autenticación adicionales antes de que se completara la primera. |

| Errores de autorización |  |
|:--- | :--- | 
| Error de autorización genérico | Se devuelve cuando el motivo no se conoce o no se puede publicar. |
| Error de autorización interna | Error del sistema al intentar autorizar. |
| Error de usuario no autorizado | El cliente no está autorizado a ver el contenido solicitado. |

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

