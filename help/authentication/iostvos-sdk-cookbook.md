---
title: Guía de iOS/tvOS
description: Guía de iOS/tvOS
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '2434'
ht-degree: 0%

---


# Guía del SDK para iOS/tvOS {#iostvos-sdk-cookbook}

- [Introducción](#intro)
- [Flujos de derechos](#entitlement)
- [Información relacionada](#related)

>[!NOTE]
>
>**Aviso**: El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>


## Introducción {#intro}

En este documento se describen los flujos de trabajo de derechos que la aplicación de nivel superior de un programador puede implementar a través de las API expuestas por la biblioteca AccessEnabler de iOS/tvOS.

 

La solución de derechos de autenticación de Adobe Primetime para iOS/tvOS se divide en dos dominios:

- Dominio de la interfaz de usuario: es la capa de aplicación de nivel superior que implementa la interfaz de usuario y utiliza los servicios proporcionados por la biblioteca AccessEnabler para proporcionar acceso a contenido restringido.
- Dominio de AccessEnabler : aquí es donde se implementan los flujos de trabajo de derechos en forma de:
   - Llamadas de red realizadas a los servidores back-end de Adobe
   - Reglas de lógica empresarial relacionadas con los flujos de trabajo de autenticación y autorización
   - Administración de varios recursos y procesamiento del estado del flujo de trabajo (como la caché de tokens)

El objetivo del dominio AccessEnabler es ocultar todas las complejidades de los flujos de trabajo de derechos y proporcionar a la aplicación de capa superior (a través de la biblioteca AccessEnabler) un conjunto de simples primitivos de derechos con los que se implementan los flujos de trabajo de derechos:

1. Establecer la identidad del solicitante
1. Comprobación y obtención de autenticación para un proveedor de identidad en particular
1. Comprobar y obtener autorización para un recurso en particular
1. Cerrar sesión
1. Flujos SSO de Apple mediante la proxie del marco VSA de Apple

La actividad de red de AccessEnabler se realiza en su propio subproceso, por lo que el subproceso de interfaz de usuario nunca se bloquea. Como resultado, el canal de comunicación bidireccional entre los dos dominios de aplicación debe seguir un patrón completamente asincrónico:

- La capa de aplicación de interfaz de usuario envía mensajes al dominio AccessEnabler mediante las llamadas de API expuestas por la biblioteca AccessEnabler.
- AccessEnabler responde a la capa de la interfaz de usuario mediante los métodos de rellamada incluidos en el protocolo AccessEnabler que la capa de la interfaz de usuario registra con la biblioteca AccessEnabler.

 

## Configuración del ID de visitante {#visitorIDSetup}

Configuración de un [Marketing Cloud visitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) es muy importante desde el punto de vista analítico. Una vez que se establece un valor visitorID , el SDK envía esta información junto con cada llamada de red y el servidor de autenticación de Adobe Primetime recopila esta información. En el futuro, podrá correlacionar los análisis del servicio de autenticación de Adobe Primetime con cualquier otro informe de análisis que pueda tener de otras aplicaciones o sitios web. Encontrará información sobre cómo configurar visitorID [here](#setOptions).

 

## Flujos de derechos {#entitlement}

A.  [Requisitos previos](#prereqs) </br>
B.  [Flujo de inicio](#startup_flow) </br>
C.  [Flujo de autenticación con Apple SSO](#authn_flow_wo_applesso)  </br>
D.  [Flujo de autenticación con Apple SSO en iOS](#authn_flow_with_applesso) </br>
E.  [Flujo de autenticación con Apple SSO en tvOS](#authn_flow_with_applesso_tvOS) </br>
F.  [Flujo de autorización](#authz_flow) </br>
G.  [Ver flujo de medios](#media_flow) </br>
H.  [Flujo de sesión sin SSO de Apple](#logout_flow_wo_AppleSSO) </br>
I.  [Flujo de sesión con Apple SSO](#logout_flow_with_AppleSSO) </br>

 

### A. Requisitos previos {#prereqs}

1. Cree sus funciones de llamada de retorno:
   - `setRequestorComplete()` </br>
      - Activado por [setRequestor()](#$setReq), devuelve el éxito o el error. </br>
      - Correcto indica que puede continuar con las llamadas de asignación de derechos.
   - [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      - Activado por [`getAuthentication()`](#$getAuthN) solo si el usuario no ha seleccionado un proveedor (MVPD) y aún no se ha autenticado. </br>
      - La variable `mvpds` es una matriz de proveedores disponibles para el usuario.
   - `setAuthenticationStatus(status, errorcode)` </br>
      - Activado por `checkAuthentication()` cada vez.  </br>
      - Activado por [`getAuthentication()`](#$getAuthN) solo si el usuario ya está autenticado y ha seleccionado un proveedor. </br>
      - El estado devuelto es correcto o falla, el código de error describe el tipo de error.
   - [`navigateToUrl(url)`](#$nav2url) </br>
      - Activado por [`getAuthentication()`](#$getAuthN) después de que el usuario seleccione un MVPD.  La variable `url` proporciona la ubicación de la página de inicio de sesión de MVPD.
   - `sendTrackingData(event, data)` </br>
      - Activado por `checkAuthentication()`, [`getAuthentication()`](#$getAuthN), `checkAuthorization()`, [`getAuthorization()`](#$getAuthZ), `setSelectedProvider()`.
      - La variable `event` indica qué evento de asignación de derechos se ha producido; el `data` es una lista de valores relacionados con el evento. 
   - `setToken(token, resource)`

      - Activado por [checkAuthorization()](#checkAuthZ) y [getAuthorization()](#$getAuthZ) después de una autorización correcta para ver un recurso.
      - La variable `token` es el token de contenido breve; el `resource` es el contenido que el usuario está autorizado a ver.
   - `tokenRequestFailed(resource, code, description)` </br>
      - Activado por [checkAuthorization()](#checkAuthZ) y [getAuthorization()](#$getAuthZ) después de una autorización incorrecta.
      - La variable `resource` es el contenido que el usuario estaba intentando ver; el `code` es el código de error que indica qué tipo de error se ha producido; el `description` describe el error asociado al código de error.
   - `selectedProvider(mvpd)` </br>
      - Activado por [`getSelectedProvider()`](#getSelProv).
      - La variable `mvpd` proporciona información sobre el proveedor seleccionado por el usuario.
   - `setMetadataStatus(metadata, key, arguments)`
      - Activado por `getMetadata().`
      - La variable `metadata` proporciona los datos específicos solicitados; el
         `key` es la clave utilizada en la variable [getMetadata()](#getMeta)
solicitud; y 
`arguments` es el mismo diccionario que se pasó a [getMetadata()](#getMeta).
   - [`preauthorizedResources(authorizedResources)`](#preauthResources)

      - Activado por [`checkPreauthorizedResources()`](#checkPreauth).
      - La variable `authorizedResources` presenta los recursos que el usuario está autorizado a ver.
   - [`currentTvProviderDialog(viewController)`](#presentTvDialog)
      - Activado por [getAuthentication()](#getAuthN) cuando el solicitante actual admita al menos en MVPD que tenga soporte para SSO.
      - El parámetro viewController es el cuadro de diálogo SSO de Apple y debe presentarse en el controlador de vista principal.
   - [`dismissTvProviderDialog(viewController)`](#dismissTvDialog)
      - Se activa mediante una acción del usuario (seleccionando &quot;Cancelar&quot; u &quot;Otros proveedores de TV&quot; en el cuadro de diálogo SSO de Apple).
      - El parámetro viewController es el cuadro de diálogo SSO de Apple y debe descartarse del controlador de vista principal.












</br>


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOS_flows\(1\).png)\
 

### B. Flujo de inicio {#startup_flow}

1. Inicie la aplicación de nivel superior.</br>
1. Iniciar la autenticación de Adobe Primetime </br></br>
a. La llamada [`init`](#$init) para crear una instancia única de AccessEnabler de autenticación de Adobe Primetime.
   - **Dependencia:** Autenticación de Adobe Primetime Biblioteca nativa iOS/tvOS (AccessEnabler)
   b. La llamada `setRequestor()` establecer la identidad del programador; pase en el `requestorID` y (opcionalmente) una matriz de extremos de autenticación de Adobe Primetime. Para tvOS también deberá proporcionar la clave pública y el secreto. Consulte [Documentación sin cliente](#create_dev) para obtener más información.
   - **Dependencia:** RequestorID de autenticación válida de Adobe Primetime\
      (Póngase en contacto con el administrador de cuentas de autenticación de Adobe Primetime para solucionarlo).
   - **Déclencheur:**

      [setRequestorComplete()](#$setReqComplete) callback
   >[!NOTE]
   >
   > **NOTA:** No se puede completar ninguna solicitud de asignación de derechos hasta que la identidad del solicitante esté completamente establecida. Esto significa que mientras que [`setRequestor()`](#$setReq)  sigue en ejecución, todas las solicitudes de asignación de derechos posteriores (por ejemplo, [`checkAuthentication()`](#checkAuthN) están bloqueados.

   Tiene dos opciones de implementación: Una vez que la información de identificación del solicitante se envía al servidor back-end, la capa de la aplicación de interfaz de usuario puede elegir uno de los dos enfoques siguientes: </br>
   1. Espere a que se active la variable [`setRequestorComplete()`](#setReqComplete) llamada de retorno (parte del delegado AccessEnabler).  Esta opción proporciona la mayor certeza de que [`setRequestor()`](#$setReq) completado, por lo que se recomienda para la mayoría de las implementaciones.
   1. Continuar sin esperar a que se active la variable [`setRequestorComplete()`](#setReqComplete) llamada de retorno y empiece a emitir solicitudes de asignación de derechos. Estas llamadas (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) están en cola en la biblioteca AccessEnabler, que hará las llamadas de red reales después de la [`setRequestor()`](#$setReq). Esta opción se puede interrumpir ocasionalmente si, por ejemplo, la conexión de red es inestable.



1. La llamada `checkAuthentication()` para comprobar si hay una autenticación existente sin iniciar el flujo de autenticación completo.  Si esta llamada se realiza correctamente, puede continuar directamente con el flujo de autorización.  Si no es así, continúe con el flujo de autenticación.

   - **Dependencia:** Una llamada correcta a [setRequestor()](#$setReq)
(esta dependencia también se aplica a todas las llamadas posteriores).

   - **Déclencheur:** [setAuthenticationStatus()](#$setAuthNStatus) callback

 

### C. Flujo de autenticación sin Apple SSO {#authn_flow_wo_applesso}

1. La llamada [`getAuthentication()`](#$getAuthN) para iniciar el flujo de autenticación o para obtener confirmación de que el usuario ya está autenticado. \
   **Déclencheur:**  

   - La variable [setAuthenticationStatus()](#$setAuthNStatus) llamada de retorno, si el usuario ya está autenticado.  En este caso, diríjase directamente al [Flujo de autorización](#authz_flow).
   - La variable [displayProviderDialog()](#$dispProvDialog) llamada de retorno, si el usuario aún no está autenticado.  

1. Presentar al usuario la lista de proveedores enviados a
   [`displayProviderDialog()`](#dispProvDialog).

1. Una vez que el usuario seleccione un proveedor, obtenga la URL del MVPD del usuario desde la `navigateToUrl:` o `navigateToUrl:useSVC:` llamada de retorno y abra una `UIWebView/WKWebView` o `SFSafariViewController` y dirigir el controlador a la dirección URL.   

1. A través de `UIWebView/WKWebView` o `SFSafariViewController` creada en el paso anterior, el usuario aterriza en la página de inicio de sesión de MVPD y accede a las credenciales de inicio de sesión. Dentro del controlador se realizan varias operaciones de redireccionamiento.</br></br>
   **NOTA** - En este punto, el usuario tiene la oportunidad de cancelar el flujo de autenticación. Si esto sucede, la capa de la interfaz de usuario es responsable de informar a AccessEnabler sobre este evento llamando a [setSelectedProvider()](#setSelProv) con `null` como parámetro. Esto permite que AccessEnabler limpie su estado interno y restablezca el flujo de autenticación.

1. Cuando el usuario inicia sesión correctamente, la capa de la aplicación detecta la carga de una URL personalizada específica. Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue realmente. Su aplicación solo debe interpretarla como una señal de que el flujo de autenticación se ha completado y de que es seguro cerrar el `UIWebView/WKWebView` o `SFSafariViewController` controlador. En caso de que `SFSafariViewController `es necesario que use el controlador para que la URL personalizada específica la defina el **`application's custom scheme`** (p. ej.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta URL personalizada específica la define el **`ADOBEPASS_REDIRECT_URL`** constante (p. ej. `adobepass://ios.app`).

1. Cierre el controlador UIWebView/WKWebView o SFSafariViewController e invoque el `handleExternalURL:url `método de API`,` que indica a AccessEnabler que recupere el token de autenticación del servidor back-end. 

1. [Opcional] La llamada    [`checkPreauthorizedResources(resources)`](#$checkPreauth) para comprobar los recursos que el usuario está autorizado a ver.  La variable `resources` es una matriz de recursos protegidos asociada al token de autenticación del usuario.  Un uso de la información de autorización obtenida del MVPD del usuario es decorar su interfaz de usuario (por ejemplo, símbolos bloqueados/desbloqueados junto al contenido protegido).

   - **Déclencheur:** [`preauthorizedResources()`](#preauthResources) callback
   - **Punto de ejecución:** Después del flujo de autenticación completado

1. Si la autenticación se ha realizado correctamente, continúe con el flujo de autorización.

 

### D. Flujo de autenticación con Apple SSO en iOS {#authn_flow_with_applesso}

1. La llamada [`getAuthentication()`](#$getAuthN) para iniciar el flujo de autenticación o para obtener confirmación de que el usuario ya está autenticado. \
   **Déclencheur:**  

   - La variable [currentTvProviderDialog()](#presentTvDialog) llamada de retorno, si el usuario no está autenticado y el solicitante actual tiene al menos un MVPD que admita SSO. Si ningún MVPD admite SSO, se utilizará el flujo de autenticación clásico.

1. Una vez que el usuario selecciona un proveedor, la biblioteca AccessEnabler obtendrá un token de autenticación con la información proporcionada por el marco VSA de Apple.

1. La variable [setAuthenticationStatus()](#setAuthNStatus) se activará la rellamada. En este punto, el usuario debe autenticarse con Apple SSO.

1. [Opcional] La llamada [`checkPreauthorizedResources(resources)`](#$checkPreauth) para comprobar los recursos que el usuario está autorizado a ver. La variable `resources` es una matriz de recursos protegidos asociada al token de autenticación del usuario.  Un uso de la información de autorización obtenida del MVPD del usuario es decorar su interfaz de usuario (por ejemplo, símbolos bloqueados/desbloqueados junto al contenido protegido).

   - **Déclencheur:** [`preauthorizedResources()`](#preauthResources) callback
   - **Punto de ejecución:** Después del flujo de autenticación completado

1. Si la autenticación se ha realizado correctamente, continúe con el flujo de autorización.

 

### E. Flujo de autenticación con Apple SSO en tvOS {#authn_flow_with_applesso_tvOS}

1. La llamada [`getAuthentication()`](#$getAuthN) para iniciar el flujo de autenticación o para obtener confirmación de que el usuario ya está autenticado. \
   **Déclencheur:**  
   - La variable [`presentTvProviderDialog()`](#presentTvDialog) llamada de retorno, si el usuario no está autenticado y el solicitante actual tiene al menos un MVPD que admita SSO. Si ningún MVPD admite SSO, se utilizará el flujo de autenticación clásico.

1. Una vez que el usuario selecciona un proveedor, el [`status()`](#status_callback_implementation) se llamará a . Se proporcionará un código de registro y la biblioteca AccessEnabler comenzará a sondear el servidor para obtener una autenticación de segunda pantalla correcta.

1. Si el código de registro proporcionado se utilizó para autenticarse correctamente en la segunda pantalla, la variable [`setAuthenticatiosStatus()`](#setAuthNStatus) se activará la rellamada. En este punto, el usuario debe autenticarse con Apple SSO.
1. [Opcional] La llamada [`checkPreauthorizedResources(resources)`](#$checkPreauth) para comprobar los recursos que el usuario está autorizado a ver. La variable `resources` es una matriz de recursos protegidos asociada al token de autenticación del usuario.  Un uso de la información de autorización obtenida del MVPD del usuario es decorar su interfaz de usuario (por ejemplo, símbolos bloqueados/desbloqueados junto al contenido protegido).
   - **Déclencheur:** [`preauthorizedResources()`](#preauthResources) callback
   - **Punto de ejecución:** Después del flujo de autenticación completado
1. Si la autenticación se ha realizado correctamente, continúe con el flujo de autorización.

 

### F. Flujo de autorización {#authz_flow}

1. La llamada [getAuthorization()](#$getAuthZ) para iniciar el flujo de autorización.
   - **Dependencia:** ResourceID(s) válidos acordados con los MVPD(s).
   - Los ID de recurso deben ser los mismos que los utilizados en otros dispositivos o plataformas, y serán los mismos en todos los MVPD. Para obtener información sobre los ID de recurso, consulte [Identificación de recursos protegidos](https://tve.helpdocsonline.com/4-2-2-3)

1. Valide la autenticación y la autorización.

   - Si la variable [getAuthorization()](#$getAuthZ) llamada correcta: El usuario tiene tokens AuthN y AuthZ válidos (el usuario está autenticado y autorizado para ver el contenido solicitado).
   - If [getAuthorization()](#$getAuthZ) falla: Examine la excepción lanzada para determinar su tipo (AuthN, AuthZ u otro):
      - Si se trata de un error de autenticación (AuthN), vuelva a iniciar el flujo de autenticación.
      - Si se trata de un error de autorización (AuthZ), el usuario no está autorizado a ver el contenido solicitado y se debe mostrar algún tipo de mensaje de error al usuario.
      - Si hay algún otro tipo de error (error de conexión, error de red, etc.) a continuación, muestre un mensaje de error apropiado al usuario.

1. Valide el token de medios corto.\
   Utilice la biblioteca del verificador de tokens de medios de autenticación de Adobe Primetime para verificar el token de medios de corta duración devuelto por el [getAuthorization()](#$getAuthZ) llamada anterior:

   - Si la validación se realiza correctamente: Reproducir el contenido solicitado para el usuario.
   - Si la validación falla: El token AuthZ no es válido, la solicitud de medios debe rechazarse y se debe mostrar un mensaje de error al usuario.


1. Vuelva al flujo normal de la aplicación.

 

### G. Ver flujo de medios {#media_flow}

1. El usuario selecciona los medios que desea ver.
1. ¿Los medios están protegidos?  La aplicación comprueba si el medio seleccionado está protegido:
   - Si el medio seleccionado está protegido, la aplicación inicia el [Flujo de autorización](#authz_flow) arriba.
   - Si el medio seleccionado no está protegido, reproduzca el contenido para el usuario.

 

### H. Flujo de cierre de sesión sin Apple SSO {#logout_flow_wo_AppleSSO}

1. La llamada [`logout()`](#$logout) para cerrar la sesión del usuario. AccessEnabler elimina todos los valores y tokens en caché. Después de borrar la caché, AccessEnabler realiza una llamada al servidor para limpiar las sesiones del lado del servidor. Tenga en cuenta que, dado que la llamada al servidor podría resultar en una redirección SAML al IdP (esto permite la limpieza de sesión en el lado IdP), esta llamada debe seguir todas las redirecciones. Por este motivo, esta llamada debe gestionarse dentro de un controlador UIWebView/WKWebView o SFSafariViewController.

   - a. Siguiendo el mismo patrón que el flujo de trabajo de autenticación, el dominio AccessEnabler realiza una solicitud a la capa de la aplicación de la interfaz de usuario a través del `navigateToUrl:` o `navigateToUrl:useSVC:` llamada de retorno, para crear un controlador UIWebView/WKWebView o SFSafariViewController e indicar que cargue la URL proporcionada en la llamada de retorno `url` parámetro. Esta es la dirección URL del extremo de cierre de sesión en el servidor back-end.

   - b. La aplicación debe monitorizar la actividad de la variable `UIWebView/WKWebView or SFSafariViewController` controle y detecte el momento en que carga una URL personalizada específica, ya que atraviesa varias redirecciones. Tenga en cuenta que esta dirección URL personalizada específica no es válida y no está pensada para que el controlador la cargue realmente. Su aplicación solo debe interpretarla como una señal de que el flujo de cierre de sesión se ha completado y de que es seguro cerrar el `UIWebView/WKWebView` o `SFSafariViewController` controlador. Cuando el controlador carga esta dirección URL personalizada específica, la aplicación debe cerrar la `UIWebView/WKWebView or SFSafariViewController` y llame a AccessEnabler `handleExternalURL:url`método de API. En caso de que `SFSafariViewController`es necesario que use el controlador para que la URL personalizada específica la defina el **`application's custom scheme`** (p. ej. `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`); de lo contrario, esta URL personalizada específica la define el **`ADOBEPASS_REDIRECT_URL`**  constante (p. ej. `adobepass://ios.app`).

      >[!NOTE]
      >
      > **NOTA:** El flujo de cierre de sesión difiere del flujo de autenticación en que no se requiere que el usuario interactúe con UIWebView/WKWebView o SFSafariViewController de ninguna manera. La capa de la aplicación de interfaz de usuario utiliza un UIWebView/WKWebView o SFSafariViewController para asegurarse de que se siguen todas las redirecciones. Por lo tanto, es posible (y recomendado) hacer que el controlador sea invisible (es decir, oculto) durante el proceso de cierre de sesión.


### I. Flujo de cierre de sesión con Apple SSO {#logout_flow_with_AppleSSO}

1. La llamada [`logout()`](#$logout) para cerrar la sesión del usuario. 
1. La variable [status()](#status_callback_implementation) se llamará a la rellamada con el id VSA203.
1. Se debe indicar al usuario que inicie sesión desde la configuración del sistema. Si no lo hace, se volverá a autenticar cuando se reinicie la aplicación.

</br>

### Información relacionada {#related}

<!---
- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Primetime
  authentication native SDK (Tech Note) ](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->
