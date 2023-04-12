---
title: Referencia de la API del cliente nativo de Amazon FireOS
description: Referencia de la API del cliente nativo de Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---


# Referencia de la API del cliente nativo de Amazon FireOS {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Introducción {#intro}

Este documento detalla los métodos y las llamadas de retorno expuestos por el SDK de Amazon FireOS para la autenticación de Adobe Primetime, compatibles con la autenticación de Adobe Primetime.</span> Los métodos y las funciones de llamada de retorno que se describen aquí se definen en los archivos de encabezado AccessEnabler.h y EntitlementDelegate.h .

Consulte <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> para el último SDK de Amazon FireOS AccessEnabler. 

**Nota:** El equipo de autenticación de Adobe Primetime le anima a utilizar solo la autenticación de Adobe Primetime *public* API:

- Las API públicas están disponibles *y* en todos los tipos de cliente admitidos. Para cualquier función pública, nos aseguramos de que cada tipo de cliente tenga una versión correspondiente de los métodos asociados.
- Las API públicas deben ser lo más estables posible, para admitir la compatibilidad con versiones anteriores y garantizar que las integraciones de socios no se rompan. Sin embargo, para *non*-API públicas, nos reservamos el derecho de cambiar su firma en cualquier momento futuro. Si se encuentra con un flujo particular que no se puede admitir mediante una combinación de las llamadas a la API de autenticación de Adobe Primetime pública actuales, el mejor enfoque es informarnos. Teniendo en cuenta sus necesidades, podemos modificar las API públicas y proporcionar una solución estable para el futuro.

## API del SDK de Amazon FireOS {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navegarToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [preauthorizedResources](#preauthResources)
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [cierre de sesión](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [selectedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**Descripción:** Crea una instancia del objeto Access Enabler. Debe haber una sola instancia de Access Enabler por instancia de aplicación.

| Llamada de API: constructor |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**Disponibilidad:** v3.0+


**Parámetros:**

- *appContext*: Contexto de la aplicación del sistema operativo Amazon Fire.
- softwareStatement
- redirectUrl : en el caso de FireOS, el valor del parámetro se ignorará y se establecerá en default : adobepass://android.app
- env_url: para realizar pruebas con el entorno de ensayo de Adobe, env\_url se puede establecer en &quot;sp.auth-staging.adobe.com&quot;

**Obsoleto:**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**Descripción:** Establece la identidad del programador. A cada programador se le asigna un ID único al registrarse con Adobe para el sistema de autenticación de Adobe Primetime. Esta configuración debe realizarse solo una vez durante el ciclo de vida de la aplicación.

La respuesta del servidor contiene una lista de MVPD junto con información de configuración adjunta a la identidad del Programador. El código Access Enabler utiliza internamente la respuesta del servidor. Solo el estado de la operación (es decir, SUCCESS/FAIL) se presenta a la aplicación a través de la llamada de retorno setRequestorComplete() .

Si la variable *url* no se usa, la llamada de red resultante se dirige a la dirección URL predeterminada del proveedor de servicios: el entorno de producción/lanzamiento de Adobe.

Si se proporciona un valor para la variable *url* , la llamada de red resultante se dirige a todas las direcciones URL proporcionadas en la variable *url* parámetro. Todas las solicitudes de configuración se activan simultáneamente en subprocesos separados. El primer encuestado tiene prioridad al compilar la lista de MVPD. Para cada MVPD de la lista, Access Enabler recuerda la URL del proveedor de servicios asociado. Todas las solicitudes de asignación de derechos subsiguientes se dirigen a la URL asociada al proveedor de servicios que estaba emparejado con el MVPD de destino durante la fase de configuración.

| Llamada de API: configuración del solicitante |
| --- |
| ```public void setRequestor(String requestorId)``` |


**Disponibilidad:**v 3.0+


| Llamada de API: configuración del solicitante |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilidad:** v3.0+


**Parámetros:**

- *requestorID*: ID exclusivo asociado al programador. Pase el ID exclusivo asignado por Adobe a su sitio cuando se registre por primera vez con el servicio de autenticación de Adobe Primetime.
- *url*: Parámetro opcional; de forma predeterminada, se utiliza el proveedor de servicios de Adobe (http://sp.auth.adobe.com/). Esta matriz le permite especificar puntos finales para los servicios de autenticación y autorización proporcionados por Adobe (se pueden utilizar diferentes instancias para la depuración). Puede usarlo para especificar varias instancias del proveedor de servicios de autenticación de Adobe Primetime. Al hacerlo, la lista de MVPD está compuesta por los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD.

**Llamadas de retorno activadas:** `setRequestorComplete()`

 

**Obsoleto:**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**Descripción:** Llamada de retorno activada por Access Enabler que informa a su aplicación de que la fase de configuración ha finalizado. Esto es una señal de que la aplicación puede empezar a emitir solicitudes de asignación de derechos. La aplicación no puede emitir solicitudes de asignación de derechos hasta que se complete la fase de configuración.

| Llamada de retorno: configuración del solicitante completada |
| --- |
| ```public void setRequestorComplete(int status)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *status*: Puede tomar uno de los siguientes valores:
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` : la fase de configuración se completó correctamente
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` : error en la fase de configuración

**Activado por:** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**Descripción:** Configura las opciones globales del SDK. Acepta un **Mapa\&lt;string string=&quot;&quot;>** como argumento. Los valores del mapa se pasarán al servidor junto con cada llamada de red que realice el SDK.

Los valores se pasarán al servidor independientemente del flujo actual (autenticación/autorización). Si desea cambiar los valores, puede llamar a este método en cualquier momento.

 

| Llamada de API: setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**Disponibilidad:** v3.0+

**Parámetros:**

- *opciones*: Un mapa\&lt;string string=&quot;&quot;> que contiene opciones globales de SDK. Actualmente están disponibles las siguientes opciones:
   - **applicationProfile** - Se puede utilizar para realizar configuraciones de servidor basadas en este valor.
   - **ap\_vi** - El Marketing Cloud visitorID. Este valor se puede usar posteriormente para informes de análisis avanzados.
   - **device\_info** - Información del dispositivo tal como se describe en **Transferencia de la guía de información del dispositivo**

</br>

### checkAuthentication {#checkAuthN}

**Descripción:** Comprueba el estado de autenticación. Para ello, busca un token de autenticación válido en el espacio de almacenamiento del token local. Llamar a este método no realiza llamadas de red. La aplicación lo utiliza para consultar el estado de autenticación del usuario y actualizar la IU en consecuencia (es decir, actualizar la IU de inicio de sesión / cierre de sesión). El estado de autenticación se comunica a la aplicación a través del [*setAuthenticationStatus()*](#setAuthNStatus) llamada de retorno.

Si un MVPD admite la función &quot;Autenticación por solicitante&quot;, se pueden almacenar varios tokens de autenticación en un dispositivo. 

| Llamada de API: comprobar el estado de autenticación |
| --- |
| ```public void checkAuthentication()``` |

**Disponibilidad:** v1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** `setAuthenticationStatus()`

</br>

### getAuthentication {#getAuthN}

**Descripción:** Inicia el flujo de trabajo de autenticación completo. Se inicia comprobando el estado de autenticación. Si aún no se ha autenticado, se inicia el flujo de autenticación state-machine:

- Si el último intento de autenticación fue exitoso, la fase de selección de MVPD se omite y un control WebView presentará al usuario la página de inicio de sesión de MVPD.
- Si el último intento de autenticación no se realizó correctamente o si el usuario cerró la sesión de forma explícita, se muestra la [*displayProviderDialog()*](#displayProviderDialog) se activa la rellamada. Su aplicación utiliza esta llamada de retorno para mostrar la IU de selección de MVPD. Además, se requiere que la aplicación reanude el flujo de autenticación informando a la biblioteca de Access Enabler sobre la selección de MVPD del usuario a través del [setSelectedProvider()](#setSelectedProvider) método.

Si un MVPD admite la función &quot;Autenticación por solicitante&quot;, se pueden almacenar varios tokens de autenticación en un dispositivo (uno por programador).

Finalmente, el estado de autenticación se comunica a la aplicación a través de la variable *setAuthenticationStatus()* llamada de retorno.

| Llamada de API: inicia el flujo de autenticación |
| --- |
| ```public void getAuthentication()``` |

**Disponibilidad:** v1.0+

| Llamada de API: inicia el flujo de autenticación |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *forceAuthn*: Un indicador que especifica si se debe iniciar el flujo de autenticación, independientemente de si el usuario ya está autenticado o no.
- *data*: Mapa que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK.

**Llamadas de retorno activadas:** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**Descripción** Llamada de retorno activada por el activador de acceso para informar a la aplicación de que es necesario crear una instancia de los elementos de la interfaz de usuario correspondientes para permitir al usuario seleccionar el MVPD deseado. La rellamada proporciona una lista de objetos MVPD con información adicional que puede ayudar a crear correctamente el panel de la interfaz de usuario de selección (como la URL que señala al logotipo de MVPD, el nombre descriptivo, etc.)

Una vez que el usuario ha seleccionado el MVPD deseado, la aplicación de la capa superior es necesaria para reanudar el flujo de autenticación llamando a *setSelectedProvider()* y transmitirle el ID del MVPD correspondiente a la selección del usuario.\
 

| **Llamada de retorno: mostrar la IU de selección de MVPD** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**Disponibilidad:** v1.0+

**Parámetros**:

- *mvpds*: Lista de objetos MVPD que contienen información relacionada con MVPD que la aplicación puede utilizar para crear los elementos de la interfaz de usuario de selección de MVPD.

**Activado por:** `getAuthentication(), getAuthorization()`

</br>

### setSelectedProvider {#setSelectedProvider}

**Descripción:** Su aplicación llama a este método para informar al habilitador de acceso de la selección de MVPD del usuario. Al pasar *null* como parámetro, Access Enabler restablece el MVPD actual a un valor nulo.

| **Llamada de API: establecer el proveedor seleccionado actualmente** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**Disponibilidad:**v 1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** `setAuthenticationStatus(), sendTrackingData()`
</br>

### navegarToUrl {#navigagteToUrl}

**Descripción:** Llamada de retorno activada por Access Enabler en el SDK para Android. Debe ignorarse en el SDK de Amazon FireOS.

| **Llamada de retorno: mostrar página de inicio de sesión de MVPD** |
| --- |
| ```public void navigateToUrl(String url)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *url*: Dirección URL que señala a la página de inicio de sesión de MVPD

**Activado por:** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**Descripción:** Completa el flujo de autenticación al solicitar el token de autenticación del servidor back-end. 

| **Llamada de API: recuperar el token de autenticación** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *cookies*: Cookies establecidas en el dominio de destino (consulte la aplicación de demostración en el SDK para obtener una implementación de referencia).

**Llamadas de retorno activadas:** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**Descripción:** Llamada de retorno activada por Access Enabler que informa a la aplicación del estado de la autenticación. Hay muchos lugares en los que el flujo de autenticación puede fallar, ya sea como resultado de la interacción del usuario o debido a otros escenarios imprevistos (por ejemplo, problemas de conectividad de red, etc.). Esta rellamada informa a la aplicación del estado de éxito/error de la autenticación, al tiempo que proporciona información adicional sobre el motivo del error, cuando es necesario.

Esta llamada de retorno también indica cuando se completa el flujo de cierre de sesión.

| **Llamada de retorno: informar del estado del flujo de autenticación** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *status*: Puede tomar uno de los siguientes valores:
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - el flujo de autenticación se completó correctamente
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - error en el flujo de autenticación
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT` - cierre de sesión
- *code*: Motivo del estado presentado. If *status* es `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`, luego *code* es una cadena vacía (es decir, definida por la variable `AccessEnabler.USER_AUTHENTICATED` constante). Si no se autentica, este parámetro puede tomar uno de los siguientes valores:
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR` - El usuario no está autenticado. En respuesta a la *checkAuthentication()* llamada de método cuando no hay ningún token de autenticación válido en la caché de token local.
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler ha restablecido el estado-máquina de autenticación después de pasar la aplicación de capa superior *null* a `setSelectedProvider()` para anular el flujo de autenticación.  Presumiblemente, el usuario ha cancelado el flujo de autenticación (es decir, ha presionado el botón &quot;Atrás&quot;).
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR` : el flujo de autenticación falló debido a motivos como la falta de disponibilidad de la red o el usuario canceló el flujo de autenticación explícitamente.
   - `AccessEnabler.LOGOUT` : el usuario no está autenticado debido a una acción de cierre de sesión. 

**Activado por:** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**Descripción:** La aplicación utiliza este método para determinar si el usuario ya está autorizado a ver recursos protegidos específicos. El objetivo principal de este método es recuperar información para utilizarla al decorar la interfaz de usuario (por ejemplo, indicar el estado de acceso con los iconos de bloqueo y desbloqueo).

| **Llamada de API: establecer el proveedor seleccionado actualmente** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Disponibilidad:** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> La variable `resources` es una matriz de recursos para los que se debe comprobar la autorización.** Cada elemento de la lista debe ser una cadena que represente el ID del recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso en la variable `getAuthorization()` , es decir, debe ser un valor acordado establecido entre el Programador y el MVPD o un fragmento RSS de medios.

**Llamada de retorno activada:** `preauthorizedResources()`

</br>

### preauthorizedResources {#preauthResources}

**Descripción:** Llamada de retorno activada por checkPreauthorizedResources(). Proporciona una lista de los recursos que el usuario ya está autorizado a ver.

| **Llamada de API: establecer el proveedor seleccionado actualmente** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Disponibilidad:**v 1.0+

**Parámetros:** La variable `resources` es una matriz de recursos para los que el usuario ya está autorizado a ver.

**Activado por:** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**Descripción:** La aplicación utiliza este método para comprobar el estado de autorización. Se inicia comprobando primero el estado de autenticación. Si no se autentica, la variable *setTokenRequestFailed()* se activa la rellamada y el método se cierra. Si el usuario está autenticado, también déclencheur el flujo de autorización. Consulte los detalles sobre *getAuthorization()* método.

| **Llamada de API: comprobar el estado de autorización** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**Disponibilidad:** v1.0+

| **Llamada de API: comprobar el estado de autorización** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *resourceId*: El ID del recurso para el que el usuario solicita la autorización.
- *data*: Mapa que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK.

**Llamadas de retorno activadas:** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**Descripción:** La aplicación utiliza este método para iniciar el flujo de autorización. Si el usuario no está autenticado, también inicia el flujo de autenticación. Si el usuario se autentica, Access Enabler procede a enviar solicitudes para el token de autorización (si no hay ningún token de autorización válido en la caché de token local) y para el token de medios de corta duración. Una vez obtenido el token de contenido corto, el flujo de autorización se considera completo. La variable *setToken()* se activa la rellamada de y el token de contenido corto se envía como parámetro a la aplicación. Si, por cualquier razón, la autorización falla, la variable *tokenRequestFailed()* se activa la llamada de retorno y se proporcionan el código de error y los detalles.

| **Llamada de API: iniciar el flujo de autorización** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**Disponibilidad:** v1.0+

| **Llamada de API: iniciar el flujo de autorización** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *resourceId*: El ID del recurso para el que el usuario solicita la autorización.
- *data*: Mapa que consiste en pares de clave-valor que se enviarán al servicio de pases de Pay-TV. Adobe puede utilizar estos datos para habilitar futuras funciones sin cambiar el SDK. 

**Llamadas de retorno activadas:** `tokenRequestFailed(), setToken(), sendTrackingData()`

|  |  |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **Llamadas adicionales activadas**  <br>Este método también puede almacenar en déclencheur las siguientes llamadas de retorno (si también se inicia el flujo de autenticación): _setAuthenticationStatus()_, _displayProviderDialog()_ |

**NOTA: Utilice checkAuthorization() en lugar de getAuthorization() siempre que sea posible. El método getAuthorization() iniciará un flujo de autenticación completo (si el usuario no está autenticado) y esto podría llevar a una implementación complicada por parte del programador.**

</br>

### setToken {#setToken}

**Descripción:** Llamada de retorno activada por Access Enabler que informa a su aplicación de que el flujo de autorización se completó correctamente. El token de contenido de corta duración también se entrega como parámetro.

| **Llamada de retorno: el flujo de autorización se completó correctamente** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**Disponibilidad:**v 1.0+

**Parámetros:**

- *token*: El testigo breve de los medios de comunicación
- *resourceId*: El recurso para el que se obtuvo la autorización

**Activado por:** `checkAuthorization(), getAuthorization()`

<br>

### tokenRequestFailed {#tokenRequestFailed}

**Descripción:** Llamada de retorno activada por Access Enabler que informa a la aplicación de capa superior de que el flujo de autorización ha fallado.

| **Llamada de retorno: error en el flujo de autorización** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *resourceId*: El recurso para el que se obtuvo la autorización
- *errorCode*: Código de error asociado al escenario de error. Valores posibles:
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR` - El usuario no pudo autorizar para el recurso dado
- *errorDescription*: Detalles adicionales sobre el escenario de error. Si esta cadena descriptiva no está disponible por ningún motivo, la autenticación de Adobe Primetime envía una cadena vacía >**(&quot;&quot;&quot;)**.  Una MVPD puede utilizar esta cadena para pasar mensajes de error personalizados o mensajes relacionados con las ventas. Por ejemplo, si a un suscriptor se le niega la autorización para un recurso, el MVPD podría enviar un mensaje como: &quot;Actualmente no tiene acceso a este canal en su paquete. Si desea actualizar su paquete haga clic aquí&quot;. La autenticación de Adobe Primetime pasa el mensaje a través de esta llamada de retorno al programador, que tiene la opción de mostrarlo o ignorarlo. La autenticación de Adobe Primetime también puede utilizar este parámetro para notificar la condición que podría haber provocado un error. Por ejemplo, &quot;Se produjo un error de red al comunicarse con el servicio de autorización del proveedor&quot;.

**Activado por:** `checkAuthorization(), getAuthorization()`

</br>

### cierre de sesión {#logout}

**Descripción:** Utilice este método para iniciar el flujo de cierre de sesión. El cierre de sesión es el resultado de una serie de operaciones de redireccionamiento HTTP debido al hecho de que el usuario necesita cerrar la sesión tanto desde los servidores de autenticación de Adobe Primetime como desde los servidores de MVPD. 

| **Llamada de API: iniciar el flujo de cierre de sesión** |
| --- |
| ```public void logout()``` |

**Disponibilidad:** v1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** Ninguna

</br>

### getSelectedProvider {#getSelectedProvider}

**Descripción:** Utilice este método para determinar el proveedor seleccionado actualmente.

| **Llamada de API: determinar el MVPD seleccionado actualmente** |
| --- |
| ```public void getSelectedProvider()``` |

**Disponibilidad:** v1.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** `selectedProvider()`

</br>

### selectedProvider {#selectedProvider}

**Descripción:** Llamada de retorno activada por Access Enabler que proporciona información sobre el MVPD seleccionado actualmente a la aplicación.

| **Llamada de retorno: información sobre el MVPD seleccionado actualmente** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *mvpd*: Objeto que contiene información sobre el MVPD seleccionado actualmente

**Activado por:** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**Descripción:** Utilice este método para recuperar información expuesta como metadatos por la biblioteca Access Enabler. La aplicación puede acceder a esta información proporcionando un objeto MetadataKey compuesto.

| **Llamada de API: consulta de AccessEnabler para metadatos** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**Disponibilidad:** v1.0+

Hay dos tipos de metadatos disponibles para los programadores:

- Metadatos estáticos (TTL token de autenticación, TTL token de autorización e ID de dispositivo) 
- Metadatos de usuario (información específica del usuario, como ID de usuario y código postal; pasados de un MVPD al dispositivo de un usuario durante los flujos de autenticación y/o autorización)

**Parámetros:**

- *metadataKey*: Estructura de datos que encapsula una clave y una variable args, con el siguiente significado:
   - Si la clave es `METADATA_KEY_TTL_AUTHN` a continuación, la consulta se realiza para obtener el tiempo de caducidad del token de autenticación.
   - Si la clave es `METADATA_KEY_TTL_AUTHZ` y args contiene un objeto SerializableNameValuePair con el nombre = `METADATA_ARG_RESOURCE_ID` y valor = `[resource_id]`, se realiza la consulta para obtener el tiempo de caducidad del token de autorización asociado al recurso especificado.
   - Si la clave es `METADATA_KEY_DEVICE_ID` a continuación, la consulta se realiza para obtener el id del dispositivo actual. Tenga en cuenta que esta función está deshabilitada de forma predeterminada y los programadores deben ponerse en contacto con Adobe para obtener información sobre la habilitación y las tarifas.
   - Si la clave es `METADATA_KEY_USER_META` y args contiene un objeto SerializableNameValuePair con el nombre = `METADATA_KEY_USER_META` y valor = `[metadata_name]`, luego la consulta se realiza para los metadatos del usuario. La lista actual de tipos de metadatos de usuario disponibles:
      - `zip` - Código postal
      - `householdID` - Identificador del hogar. Si un MVPD no admite subcuentas, será idéntico a `userID`.
      - `maxRating` - Clasificación parental máxima para el usuario
      - `userID` - El identificador de usuario. Si un MVPD admite subcuentas y el usuario no es la cuenta principal,
      - `channelID` - Una lista de canales que el usuario puede ver

Los metadatos de usuario disponibles para un programador dependen de lo que un MVPD ponga a disposición.  Esta lista se ampliará aún más a medida que los nuevos metadatos estén disponibles y se añadan al sistema de autenticación de Adobe Primetime.

**Llamadas de retorno activadas:** [`setMetadataStatus()`](#setMetadaStatus)

**Más información:** [Metadatos de usuario](#setmetadatastatus)

</br>

### setMetadataStatus {#setMetadaStatus}

**Descripción:** Llamada de retorno activada por Access Enabler que envía los metadatos solicitados mediante un *getMetadata()* llamada a .

| **Llamada de retorno: resultado de la solicitud de recuperación de metadatos** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *key*: El objeto MetadataKey que contiene la clave para la que se solicita el valor de los metadatos y los parámetros asociados (consulte aplicación de demostración para una implementación de referencia).
- *result*: Un objeto compuesto que contiene los metadatos solicitados. El objeto tiene los siguientes campos:
   - *simpleResult*: una cadena que representa el valor de los metadatos cuando se realizó la solicitud de autenticación TTL, autorización TTL o ID del dispositivo. Este valor es nulo si la solicitud se realizó para los metadatos de usuario.

   - *userMetadataResult*: un objeto que contiene la representación Java de una carga útil de metadatos de usuario JSON. Por ejemplo:

      ```json
      {
      "street": "Main Avenue",
      "buildings": ["150", "320"]
      }
      ```

      se traduce a Java como: 

      ```java
      Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
      ```

      **La estructura real de los objetos de metadatos de usuario es similar a la siguiente:**

      ```json
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
      }
      ```
 

Este valor es nulo cuando la solicitud se realizó para metadatos simples (TTL de autenticación, TTL de autorización o ID de dispositivo).

- *cifrados*: Valor booleano que especifica si los metadatos recuperados están cifrados o no. Este parámetro es significativo solo para solicitudes de metadatos de usuario, no tiene significado para metadatos estáticos (por ejemplo, TTL de autenticación) que siempre se reciben sin encriptar. Si este parámetro se establece en True, corresponde al programador obtener el valor de los metadatos de usuario sin encriptar realizando un descifrado RSA utilizando la clave privada de lista blanca (la misma clave privada que se usa para firmar el id de solicitante en la variable [`setRequestor`](#setRequestor) ).

**Activado por:** [`getMetadata()`](#getMetadata)

**Más información:** [Metadatos de usuario](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**Descripción:** Utilice este método para recuperar la versión actual de AccessEnabler  

| **Llamada de API: obtener la versión de AccessEnabler** |
| --- |
| ```public static String getVersion()``` |

## Seguimiento de eventos {#tracking}

Access Enabler déclencheur una llamada de retorno adicional que no está necesariamente relacionada con los flujos de derechos. Implementación de la función de llamada de retorno de seguimiento de eventos denominada *sendTrackingData()* es opcional, pero permite a la aplicación rastrear eventos específicos y compilar estadísticas como el número de intentos de autenticación/autorización correctos/fallidos. A continuación se muestra la especificación para la variable *sendTrackingData()* llamada de retorno:

### sendTrackingData {#sendTrackingData}

**Descripción:** Llamada de retorno activada por el activador de acceso que indica a la aplicación la ocurrencia de varios eventos, como la finalización/fallo de los flujos de autenticación/autorización. El tipo de dispositivo, el tipo de cliente Access Enabler y el sistema operativo también se incluyen en los informes mediante sendTrackingData().

>[!WARNING]
>
> El tipo de dispositivo y el sistema operativo se derivan del uso de una biblioteca Java pública (http://java.net/projects/user-agent-utils) y la cadena del agente de usuario. Tenga en cuenta que esta información se proporciona solamente como una forma granular de desglosar las métricas operativas en categorías de dispositivos, pero ese Adobe no puede asumir ninguna responsabilidad por los resultados incorrectos. Utilice la nueva funcionalidad en consecuencia.

- Valores posibles para el tipo de dispositivo:
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`

- Valores posibles del tipo de cliente Access Enabler:
   - `flash`
   - `html5`
   - `ios`
   - `tvos`
   - `android`
   - `firetv`

| Llamada de retorno: seguimiento de eventos |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**Disponibilidad:** v1.0+

**Parámetros:**

- *evento*: el evento que se está rastreando. Existen tres tipos de eventos de seguimiento posibles:
   - **authorizationDetection:** cada vez que se devuelve una solicitud de token de autorización (el tipo de evento es `EVENT_AUTHZ_DETECTION`)
   - **authenticationDetection:** cada vez que se produce una comprobación de autenticación (el tipo de evento es `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** cuando el usuario selecciona un MVPD en el formulario de selección de MVPD (el tipo de evento es `EVENT_MVPD_SELECTION`)
- *data*: datos adicionales asociados al evento registrado. Estos datos se presentan en forma de una lista de valores.

A continuación se indican las instrucciones para interpretar los valores de la variable *data* matriz:

- Para el tipo de evento *`EVENT_AUTHN_DETECTION`:*
   - **0** - Si la solicitud del token se ha realizado correctamente (true/false) y si el valor anterior es verdadero:
   - **1** - Cadena de ID de MVPD
   - **2** - GUID (con hash md5)
   - **3** - Token ya en la caché (true/false)
   - **4** - Tipo de dispositivo
   - **5** - Tipo de cliente Access Enabler
   - **6** - Tipo de sistema operativo

- Para el tipo de evento `EVENT_AUTHZ_DETECTION`
   - **0** - Si la solicitud del token se ha realizado correctamente (true/false) y si se ha realizado correctamente:
   - **1** - ID de MVPD
   - **2** - GUID (con hash md5)
   - **3** - Token ya en la caché (true/false)
   - **4** - Error
   - **5** - Detalles
   - **6** - Tipo de dispositivo
   - **7** - Tipo de cliente Access Enabler
   - **8** - Tipo de sistema operativo

- Para el tipo de evento `EVENT_MVPD_SELECTION`
   - **0** - ID del MVPD seleccionado actualmente
   - **1** - Tipo de dispositivo
   - **2** - Tipo de cliente Access Enabler
   - **3** - Tipo de sistema operativo

**Activado por:** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
