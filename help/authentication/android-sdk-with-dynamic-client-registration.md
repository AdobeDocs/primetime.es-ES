---
title: SDK para Android con registro de cliente dinámico
description: SDK para Android con registro de cliente dinámico
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---



# SDK para Android con registro de cliente dinámico {#android-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#Intro}

El SDK de Android AccessEnabler para Android se ha modificado para habilitar la autenticación sin usar cookies de sesión. Dado que cada vez más exploradores restringen el acceso a las cookies, es necesario utilizar otro método para permitir la autenticación.

Para Android, el uso de Pestañas personalizadas de Chrome restringe el acceso a las cookies de otras aplicaciones.

>**SDK para Android 3.0.0** introduce:

- el registro de cliente dinámico reemplaza el mecanismo de registro de aplicación actual basado en la autenticación de ID de solicitante y cookie de sesión firmadas
- Pestañas personalizadas de Chrome para flujos de autenticación

>[!NOTE]
>
>Para versiones anteriores de Android sin compatibilidad con Pestañas personalizadas de Chrome, se utilizará la autenticación WebView similar a la de versiones anteriores de AccessEnabler SDK.


## Registro de cliente dinámico {#DCR}

Android SDK v3.0+ utilizará el procedimiento de registro de cliente dinámico definido en [Registro de cliente dinámico](/help/authentication/dynamic-client-registration.md).


## Demostración de la función {#Demo}

Por favor, mire [este seminario web](https://my.adobeconnect.com/pzkp8ujrigg1/) que proporciona más contexto de la función y contiene una demostración de cómo administrar las instrucciones de software mediante el panel de control de Televisión y cómo probar las generadas mediante una aplicación de demostración proporcionada por Adobe como parte del SDK para Android.

## Cambios en la API {#API}


### Factory.getInstance

**Descripción:** Crea una instancia del objeto Access Enabler. Debe haber una sola instancia de Access Enabler por instancia de aplicación.

| Llamada de API: constructor |
| --- |
| public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        lanza AccessEnablerException |


**Disponibilidad:** v3.0+

**Parámetros:**

- *appContext*: Contexto de la aplicación de Android
- SoftwareStatement: valor obtenido del TVE Dashboard o *null* si &quot;software\_statement&quot; está configurado en strings.xml
- redirectUrl : url única, uno de los dominios en orden inverso que se agregó explícitamente en el panel de control de Televisión o *null* si &quot;redirect\_uri&quot; se configura en strings.xml

Nota : softwareStatement o redirectUrl no válidos harán que la aplicación no inicialice AccessEnabler o registre la aplicación para la autenticación y autorización de Adobe Pass
</br>
Nota : El parámetro redirectUrl o redirect\_uri en strings.xml debe ser el valor del dominio añadido en el panel de control de Televisión para la aplicación en orden inverso ( por ejemplo: para el dominio &quot;adobe.com&quot; añadido en TVE Dashboard, redirectUrl debe ser &quot;com.adobe&quot;.
 

### setRequestor

**Descripción:** Establece la identidad del canal. A cada canal se le asigna un ID único tras registrarse con Adobe para el sistema de autenticación de Adobe Primetime. Cuando se trata de SSO y tokens remotos, el estado de autenticación puede cambiar cuando la aplicación está en segundo plano, se puede volver a llamar a setRequestor cuando la aplicación se ponga en primer plano para sincronizar con el estado del sistema (obtenga un token remoto si SSO está habilitado o elimine el token local si se ha producido un cierre de sesión mientras tanto).

La respuesta del servidor contiene una lista de MVPD junto con información de configuración adjunta a la identidad del Canal. El código Access Enabler utiliza internamente la respuesta del servidor. Solo el estado de la operación (es decir, SUCCESS/FAIL) se presenta a la aplicación a través de la llamada de retorno setRequestorComplete() .

Si la variable *url* no se usa, la llamada de red resultante se dirige a la dirección URL predeterminada del proveedor de servicios: el entorno de producción/lanzamiento de Adobe.

Si se proporciona un valor para la variable *url* , la llamada de red resultante se dirige a todas las direcciones URL proporcionadas en la variable *url* parámetro. Todas las solicitudes de configuración se activan simultáneamente en subprocesos separados. El primer encuestado tiene prioridad al compilar la lista de MVPD. Para cada MVPD de la lista, Access Enabler recuerda la URL del proveedor de servicios asociado. Todas las solicitudes de asignación de derechos subsiguientes se dirigen a la URL asociada al proveedor de servicios que estaba emparejado con el MVPD de destino durante la fase de configuración.

| Llamada de API: configuración del solicitante |
| --- |
| ```public void setRequestor(String requestorId)``` |

**Disponibilidad:** v3.0+

| Llamada de API: configuración del solicitante |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilidad:** v3.0+

**Parámetros:**

- *requestorID*: ID exclusivo asociado al canal. Pase el ID exclusivo asignado por Adobe a su sitio cuando se registre por primera vez con el servicio de autenticación de Adobe Primetime.
- *url*: Parámetro opcional; de forma predeterminada, se utiliza el proveedor de servicios de Adobe [http://sp.auth.adobe.com/](http://sp.auth.adobe.com/). Esta matriz le permite especificar puntos finales para los servicios de autenticación y autorización proporcionados por Adobe (se pueden utilizar diferentes instancias para la depuración). Puede usarlo para especificar varias instancias del proveedor de servicios de autenticación de Adobe Primetime. Al hacerlo, la lista de MVPD está compuesta por los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD.

Obsoleto:

- *signedRequestorID*: Una copia del ID del solicitante que se firma digitalmente con su clave privada. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**Llamadas de retorno activadas:** `setRequestorComplete()`

### cierre de sesión

**Descripción:** Utilice este método para iniciar el flujo de cierre de sesión. El cierre de sesión es el resultado de una serie de operaciones de redireccionamiento HTTP debido al hecho de que el usuario necesita cerrar la sesión tanto desde los servidores de autenticación de Adobe Primetime como desde los servidores de MVPD. Como resultado, este flujo abrirá una ventana ChromeCustomTab para ejecutar el cierre de sesión.

| Llamada de API: iniciar el flujo de cierre de sesión |
| --- |
| public void logout() |

**Disponibilidad:** v3.0+

**Parámetros:** Ninguna

**Llamadas de retorno activadas:** `setAuthenticationStatus()`
</br></br>

## Flujo de implementación del programador {#Progr}

### **1. Registrar aplicación** 

a. Obtenga software\_statement y redireccionamiento\_uri desde Adobe Pass ( Tablero TVE )

b. Existen dos opciones para pasar estos valores al SDK de Adobe Pass :

En strings.xml agregue : 

```XML
<string name="software_statement">[softwarestatement value]</string>
<string name="redirect_uri">application_url.com</string>
```

Llame a AccessEnabler.getInstance(appContext,softwareStatement, redirectUrl)


### 2. Configurar aplicación

a. setRequestor(requestor\_id) 

El SDK realizará las siguientes operaciones: 

- solicitud de registro: using **software\_statement**, el SDK obtendrá un **client\_id, client\_secret, client\_id\_issued\_at, redirect\_uris, grant\_types**. Esta información se almacena en el almacenamiento interno de la aplicación.

- obtenga un **access\_token** utilizando client\_id, client\_secret y grant\_type=&quot;client\_credentials&quot; . Este access\_token se utilizará en cada llamada realizada por el SDK a los servidores de Adobe Pass 

**Respuestas de error de token :**

| Respuestas de error |  |  |
| --- | --- | --- |
| HTTP 400 (solicitud incorrecta) | {&quot;error&quot;: &quot;no válido\_request&quot;} | A la solicitud le falta un parámetro requerido, incluye un valor de parámetro no admitido (que no sea el tipo de concesión), repite un parámetro, incluye varias credenciales, utiliza más de un mecanismo para autenticar al cliente o tiene un formato incorrecto. |
| HTTP 400 (solicitud incorrecta) | {&quot;error&quot;: &quot;no válido\_client&quot;} | Error de autenticación de cliente porque se desconoce el cliente. El SDK DEBE registrarse de nuevo con el servidor de autorización. |
| HTTP 400 (solicitud incorrecta) | {&quot;error&quot;: &quot;no autorizado\_client&quot;} | El cliente autenticado no está autorizado a utilizar este tipo de concesión de autorización. |

- en caso de que un MVPD requiera autenticación pasiva, se abrirá una pestaña personalizada de Chrome para ejecutar pasivamente con ese MVPD y se cerrará cuando se complete

b. checkAuthentication()

- true : vaya a Autorización
- false : vaya a Seleccionar MVPD

c. getAuthentication : El SDK incluirá **access_token** en los parámetros de llamada 

- mvpd recordó : vaya a setSelectedProvider(mvpd_id)
- mvpd no seleccionado: displayProviderDialog
- mvpd seleccionado: vaya a setSelectedProvider(mvpd_id)

d. setSelectedProvider

- La dirección url de autenticación mvpd\_id se carga en ChromeCustomTabs
- inicio de sesión correcto : delegate.setAuthenticationStatus ( SUCCESS )
- inicio de sesión cancelado : restablecer selección de MVPD
- El esquema de URL se establece como &quot;adobepass://redirect_uri&quot; para capturar cuándo se completa la autenticación

e. get/checkAuthorization : El SDK incluirá **access_token** en el encabezado como Autorización: Portador **access_token**

- si la autorización se realiza correctamente, se llama a para obtener el token de medios

f. cierre de sesión : 

- El SDK eliminará un token válido para el solicitante actual (las autenticaciones obtenidas por otras aplicaciones y no a través de SSO seguirán siendo válidas)
- El SDK abrirá las Pestañas personalizadas de Chrome para alcanzar el punto final de cierre de sesión mvpd_id. Una vez finalizadas, las fichas personalizadas de Chrome se cerrarán
- El esquema de URL se establece como &quot;adobepass://logout&quot; para capturar el momento en que se completa el cierre de sesión
- El cierre de sesión déclencheur un sendTrackingData(new Event(EVENT_LOGOUT,USER_NOT_AUTHENTICATED_ERROR) y una devolución de llamada : setAuthenticationStatus(0,&quot;Logout&quot;)

**Nota:** ya que cada llamada requiere un **access_token,** los posibles códigos de error siguientes se gestionan en el SDK. 


| Respuestas de error |  |  |
| --- | ---|--- |
| invalid_request | 400 | El formato de la solicitud es incorrecto. El SDK debe dejar de realizar llamadas al servidor. |
| invalid_client | 403 | Ya no se permite que el ID de cliente realice solicitudes. El sdk DEBE realizar de nuevo el registro del cliente. |
| access_deny | 401 | El access\_token no es válido. El sdk DEBE solicitar un access_token nuevo. |
