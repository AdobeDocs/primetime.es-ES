---
title: Guía de integración de Amazon FireOS
description: Guía de integración de Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---


# Guía de integración de Amazon FireOS {#amazon-fireos-integration-cookbook}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>


## Introducción {#intro}

En este documento se describen los flujos de trabajo de derechos que la aplicación de nivel superior de un programador puede implementar a través de las API expuestas por la biblioteca Amazon FireOS AccessEnabler.

La solución de derechos de autenticación de Adobe Primetime para Amazon FireOS se divide en dos dominios:

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

La actividad de red de AccessEnabler se realiza en un subproceso diferente, por lo que el subproceso de interfaz de usuario nunca se bloquea. Como resultado, el canal de comunicación bidireccional entre los dos dominios de aplicación debe seguir un patrón completamente asincrónico:

- La capa de aplicación de interfaz de usuario envía mensajes al dominio AccessEnabler mediante las llamadas de API expuestas por la biblioteca AccessEnabler.
- AccessEnabler responde a la capa de la interfaz de usuario mediante los métodos de rellamada incluidos en el protocolo AccessEnabler que la capa de la interfaz de usuario registra con la biblioteca AccessEnabler.

## Flujos de derechos {#entitlement}

1. [Requisitos previos](#prereqs)
1. [Flujo de inicio](#startup_flow)
1. [Flujo de autenticación](#authn_flow)
1. [Flujo de autorización](#authz_flow)
1. [Ver flujo de medios](#media_flow)
1. [Flujo de cierre de sesión](#logout_flow)

 

### A. Requisitos previos {#prereqs}

1. Cree sus funciones de llamada de retorno:
   - [`setRequestorComplete()`](#$setRequestorComplete)

      - Activado por `setRequestor()`, devuelve el éxito o el error.     Correcto indica que puede continuar con las llamadas de asignación de derechos.
   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

      - Activado por `getAuthentication()` solo si el usuario no ha seleccionado un proveedor (MVPD) y aún no se ha autenticado. La variable `mvpds` es una matriz de proveedores disponibles para el usuario.
   - [`setAuthenticationStatus(status, reason)`](#$setAuthNStatus)

      - Activado por `checkAuthentication()` cada vez. Activado por `getAuthentication()` solo si el usuario ya está autenticado y ha seleccionado un proveedor.

      - El estado devuelto está autenticado o no está autenticado, el motivo describe un error de autenticación o una acción de cierre de sesión.
   - [navegarToUrl(url)](#$navigateToUrl)

      - Ignorado en el SDK de AmazonFireOS, el método se utiliza en plataformas Android donde se activa mediante `getAuthentication()` después de que el usuario seleccione un MVPD.  La variable `url` proporciona la ubicación de la página de inicio de sesión de MVPD.
   - [`sendTrackingData(event, data)`](#$sendTrackingData)

      - Activado por `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.
La variable `event` indica qué evento de asignación de derechos se ha producido;la variable `data` es una lista de valores relacionados con el evento. 
   - [`setToken(token, recurso)`](#$setToken)

      - Activado por `checkAuthorization()` y `getAuthorization()` después de una autorización correcta para ver un recurso.
      - La variable `token` es el token de medio de corta duración;la variable `resource` es el contenido que el usuario está autorizado a ver.
   - [`tokenRequestFailed(recurso, código, descripción)`](#$tokenRequestFailed)

      - Activado por `checkAuthorization()` y `getAuthorization()` después de una autorización incorrecta.
      - La variable `resource` es el contenido que el usuario estaba intentando ver; el `code` es el código de error que indica qué tipo de error se ha producido; el `description` describe el error asociado al código de error.
   - [`selectedProvider(mvpd)`](#$selectedProvider)

      - Activado por `getSelectedProvider()`.
      - La variable `mvpd` proporciona información sobre el proveedor seleccionado por el usuario.
   - [`setMetadataStatus(metadata, key, discussions)`](#$setMetadataStatus)

      - Activado por `getMetadata().`
      - La variable `metadata` proporciona los datos específicos solicitados; el `key` es la clave utilizada en la variable `getMetadata()` solicitud; y `arguments` es el mismo diccionario que se pasó a `getMetadata()`.
   - [`preauthorizedResources(resources)`](#$preauthResources)

      - Activado por `checkPreauthorizedResources()`.
      - La variable `authorizedResources` presenta los recursos que el usuario está autorizado a ver.\
          










![](assets/android-entitlement-flows.png)\
 

### B. Flujo de inicio {#startup_flow}

1. Inicie la aplicación de nivel superior.
1. Iniciar la autenticación de Adobe Primetime
   1. La llamada [`getInstance`](#$getInstance) para crear una instancia única de AccessEnabler de autenticación de Adobe Primetime.

      - **Dependencia:** Autenticación de Adobe Primetime Biblioteca FireOS nativa de Amazon (AccessEnabler)
   2. La llamada` setRequestor()` establecer la identificación del programador; pase en el `requestorID` y (opcionalmente) una matriz de extremos de autenticación de Adobe Primetime.

      - **Dependencia:** RequestorID de autenticación válida de Adobe Primetime (trabaje con el administrador de cuentas de autenticación de Adobe Primetime para solucionarlo).

      - **Déclencheur:** devolución de llamada setRequestorComplete()

   No se puede completar ninguna solicitud de asignación de derechos hasta que la identidad del solicitante esté completamente establecida. Esto significa que mientras setRequestor() sigue en ejecución, todas las solicitudes de asignación de derechos posteriores (por ejemplo,`checkAuthentication()`) están bloqueados.

   Tiene dos opciones de implementación: Una vez que la información de identificación del solicitante se envía al servidor back-end, la capa de la aplicación de interfaz de usuario puede elegir uno de los dos enfoques siguientes:</p>

   1. Espere a que se active la variable `setRequestorComplete()` llamada de retorno (parte del delegado AccessEnabler).  Esta opción proporciona la mayor certeza de que `setRequestor()` completado, por lo que se recomienda para la mayoría de las implementaciones.

   1. Continuar sin esperar a que se active la variable `setRequestorComplete()` llamada de retorno y empiece a emitir solicitudes de asignación de derechos. Estas llamadas (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) están en cola en la biblioteca AccessEnabler, que hará las llamadas de red reales después de la `setRequestor()`. Esta opción se puede interrumpir ocasionalmente si, por ejemplo, la conexión de red es inestable.




1. La llamada [checkAuthentication()](#$checkAuthN) para comprobar si hay una autenticación existente sin iniciar el flujo de autenticación completo.  Si esta llamada se realiza correctamente, puede continuar directamente con el flujo de autorización.  Si no es así, continúe con el flujo de autenticación.

- **Dependencia:** Una llamada correcta a `setRequestor()` (esta dependencia también se aplica a todas las llamadas posteriores).

- **Déclencheur:** Llamada de retorno setAuthenticationStatus()

### C. Flujo de autenticación {#authn_flow}

1. La llamada [`getAuthentication()`](#$getAuthN) para iniciar el flujo de autenticación o para obtener confirmación de que el usuario ya está autenticado. 

   **Déclencheur:**  

   - La llamada de retorno setAuthenticationStatus(), si el usuario ya está autenticado.  En este caso, diríjase directamente al [Flujo de autorización](#authz_flow).
   - La llamada de retorno displayProviderDialog(), si el usuario aún no está autenticado.  

1. Presentar al usuario la lista de proveedores enviados a `displayProviderDialog()`.

1. Una vez que el usuario selecciona un proveedor, WebView abre la página del proveedor para que el usuario inicie sesión

   **Nota:** En este punto, el usuario tiene la oportunidad de cancelar el flujo de autenticación. Si esto ocurre, AccessEnabler limpiará su estado interno y restablecerá el flujo de autenticación.

1. Cuando el usuario inicie sesión correctamente, WebView se cerrará.

1. llamada `getAuthenticationToken(),` que indica a AccessEnabler que recupere el token de autenticación del servidor back-end. 

1. [Opcional] La llamada [`checkPreauthorizedResources(resources)`](#$checkPreauth) para comprobar los recursos que el usuario está autorizado a ver. La variable `resources` es una matriz de recursos protegidos asociada al token de autenticación del usuario.\
   **Déclencheur:** `preAuthorizedResources()` callback\
   **Punto de ejecución:** Después del flujo de autenticación completado

1. Si la autenticación se ha realizado correctamente, continúe con el flujo de autorización.

 

### D. Flujo de autorización {#authz_flow}

1. La llamada [`getAuthorization()`](#$getAuthZ) para iniciar el flujo de autorización.

   Dependencia: ResourceID(s) válidos acordados con los MVPD(s).

   **Nota:** ResourceIDs debe ser el mismo que se usa en cualquier otro dispositivo o plataforma, y será el mismo en todos los MVPD.

1. Valide la autenticación y la autorización.

   - Si la variable `getAuthorization()` llamada correcta: El usuario tiene tokens AuthN y AuthZ válidos (el usuario está autenticado y autorizado para ver el contenido solicitado).
   - If `getAuthorization()` falla: Examine la excepción lanzada para determinar su tipo (AuthN, AuthZ u otro):
      - Si se trata de un error de autenticación (AuthN), vuelva a iniciar el flujo de autenticación.
      - Si se trata de un error de autorización (AuthZ), el usuario no está autorizado a ver el contenido solicitado y se debe mostrar algún tipo de mensaje de error al usuario.
      - Si hay algún otro tipo de error (error de conexión, error de red, etc.) a continuación, muestre un mensaje de error apropiado al usuario.

1. Valide el token de medios corto.

   Utilice la biblioteca del verificador de tokens de medios de autenticación de Adobe Primetime para verificar el token de medios de corta duración devuelto por el `getAuthorization()` llamada anterior:

   - Si la validación se realiza correctamente: Reproducir el contenido solicitado para el usuario.
   - Si la validación falla: El token AuthZ no es válido, la solicitud de medios debe rechazarse y se debe mostrar un mensaje de error al usuario.

1. Vuelva al flujo normal de la aplicación.

### E. Ver flujo de medios {#media_flow}

1. El usuario selecciona los medios que desea ver.
1.  ¿Los medios están protegidos?  La aplicación comprueba si el medio seleccionado está protegido:
   - Si el medio seleccionado está protegido, la aplicación inicia el [Flujo de autorización](#authz_flow) arriba.
   - Si el medio seleccionado no está protegido, reproduzca el contenido para el usuario.

### F. Flujo de cierre de sesión {#logout_flow}

1. La llamada [`logout()`](#$logout) para cerrar la sesión del usuario. \
   AccessEnabler borra todos los valores en caché y tokens obtenidos por el usuario para el MVPD actual en todos los solicitantes que comparten el inicio de sesión mediante el inicio de sesión único. Después de borrar la caché, AccessEnabler realiza una llamada al servidor para limpiar las sesiones del lado del servidor.  Tenga en cuenta que, dado que la llamada al servidor podría resultar en una redirección SAML al IdP (esto permite la limpieza de sesión en el lado IdP), esta llamada debe seguir todas las redirecciones. Por este motivo, esta llamada se gestionará dentro de un control WebView, invisible para el usuario.

   **Nota:** El flujo de cierre de sesión difiere del flujo de autenticación en que no se requiere que el usuario interactúe con WebView de ninguna manera. Por lo tanto, es posible (y recomendado) hacer invisible el control WebView (es decir: oculto) durante el proceso de cierre de sesión.

