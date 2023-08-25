---
title: SDK de Amazon FireOS con registro de cliente dinámico
description: SDK de Amazon FireOS con registro de cliente dinámico
exl-id: 27acf3f5-8b7e-4299-b0f0-33dd6782aeda
source-git-commit: bfa2c3d55848dd1e50daa83fb77d040bc7c37045
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# SDK de Amazon FireOS con registro de cliente dinámico {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

</br>

## <span id=""></span>Introducción {#Intro}

El SDK de FireOS AccessEnabler para FireTV se ha modificado para habilitar la autenticación sin usar cookies de sesión. Como cada vez más exploradores restringen el acceso a las cookies, se necesitaba otro método para permitir la autenticación.

**FireOS SDK 3.0.4** reemplaza el mecanismo de registro de la aplicación actual basado en el ID del solicitante firmado y la autenticación de cookie de sesión por [Registro dinámico de clientes](/help/authentication/dynamic-client-registration.md).


## Cambios de API {#API}

### Factory.getInstance

**Descripción:** Crea una instancia del objeto Habilitador de acceso. Debe haber una sola instancia de Access Enabler por cada instancia de aplicación.

| Llamada de API: constructor |
| --- |
| public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        inicia AccessEnablerException |

**Disponibilidad:** v3.0+

**Parámetros:**

- *appContext*: contexto de aplicación de Android
- *softwareStatement*: valor obtenido del tablero de TVE o *null* si &quot;software\_statement&quot; está definido en strings.xml
- *redirectUrl* : para implementaciones de FireTV, este parámetro debe ser nulo. Se ignorará cualquier configuración de este atributo.

**Notas**

- softwareStatement no válida provocará que la aplicación no inicialice AccessEnabler o registre la aplicación para la autenticación y autorización de Adobe Pass
- El SDK establece el parámetro redirectUrl para FireTV en adobepass://android.app, ya que la autenticación la gestiona la instancia única de AccessEnabler.

### setRequestor

**Descripción:** Establece la identidad del canal. A cada canal se le asigna un ID único al registrarse con el Adobe en el sistema de autenticación de Adobe Primetime. Cuando se trata de SSO y tokens remotos, el estado de autenticación puede cambiar cuando la aplicación está en segundo plano. Se puede volver a llamar a setRequestor cuando la aplicación se pone en primer plano para sincronizar con el estado del sistema (recupere un token remoto si está habilitado el SSO o elimine el token local si se ha cerrado la sesión mientras tanto).

La respuesta del servidor contiene una lista de MVPD junto con información de configuración adjunta a la identidad del canal. El código Access Enabler utiliza internamente la respuesta del servidor. Solo el estado de la operación (es decir, SUCCESS/FAIL) se presenta a la aplicación a través de la llamada de retorno setRequestorComplete().

Si la variable *url* no se utiliza, la llamada de red resultante se dirige a la dirección URL del proveedor de servicios predeterminado: el entorno de producción de versiones de Adobe.

Si se proporciona un valor para *url* , la llamada de red resultante se dirige a todas las direcciones URL proporcionadas en el parámetro *url* parámetro. Todas las solicitudes de configuración se activan simultáneamente en subprocesos independientes. El primer respondedor tiene prioridad al compilar la lista de MVPD. Para cada MVPD de la lista, el Habilitador de acceso recuerda la URL del proveedor de servicios asociado. Todas las solicitudes de derechos subsiguientes se dirigen a la URL asociada al proveedor de servicios emparejado con la MVPD de destino durante la fase de configuración.

| Llamada de API: configuración del solicitante |
| --- |
| public void setRequestor(String requestorId) |

**Disponibilidad:** v3.0+

| Llamada de API: configuración del solicitante |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilidad:** v3.0+

**Parámetros:**

- *requestorID*: ID único asociado con el canal. Pase el ID único asignado por el Adobe a su sitio cuando se registre por primera vez en el servicio de autenticación de Adobe Primetime.
- *url*: Parámetro opcional; de forma predeterminada, se utiliza el proveedor de servicios de Adobe (http://sp.auth.adobe.com/). Esta matriz permite especificar extremos para los servicios de autenticación y autorización proporcionados por el Adobe (se pueden utilizar diferentes instancias para la depuración). Puede utilizar esto para especificar varias instancias del proveedor de servicios de autenticación de Adobe Primetime. Al hacerlo, la lista de MVPD se compone de los extremos de todos los proveedores de servicios. Cada MVPD está asociado con el proveedor de servicios más rápido; es decir, el proveedor que respondió primero y que admite ese MVPD.

Obsoleto:

- *signedRequestorID*: una copia del ID del solicitante firmado digitalmente con su clave privada. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**Llamadas activadas:** `setRequestorComplete()`

</br>

### cierre de sesión

**Descripción:** Utilice este método para iniciar el flujo de cierre de sesión. El cierre de sesión es el resultado de una serie de operaciones de redirección HTTP debido al hecho de que el usuario debe cerrar la sesión tanto desde los servidores de autenticación de Adobe Primetime como desde los servidores de MVPD. Como resultado, este flujo abrirá una ventana de Chrome CustomTab para ejecutar el cierre de sesión.

| Llamada de API: iniciar el flujo de cierre de sesión |
| --- |
| public void logout() |

**Disponibilidad:** v3.0+

**Parámetros:** Ninguno

**Llamadas activadas:** `setAuthenticationStatus()`

## Flujo de implementación del programador {#Progr}

### **1. Registrar aplicación**

1. Obtener software\_statement de Adobe Pass ( TVE Dashboard )
1. Existen dos opciones para pasar estos valores al SDK de Adobe Pass:
   - En strings.xml, agregue:

     ```
     <string name>"software\_statement">[softwarestatement value]</string>
     ```

   - Llamar a AccessEnabler.getInstance(appContext,softwareStatement, null)



### **2. Configurar aplicación**

- a. setRequestor(solicitante\_id)

  El SDK realizará las siguientes operaciones:

   - solicitud de registro: utilizando **software\_statement**, el SDK obtendrá una **client\_id, client\_secret, client\_id\_issued\_at, redirect\_uris, grant\_types**. Esta información se almacena en el almacenamiento interno de la aplicación.
   - obtenga un **access\_token** usando client\_id, client\_secret y grant\_type=&quot;client\_credentials&quot; . Este access\_token se usará en cada llamada realizada por el SDK a los servidores de Adobe Pass.

| Respuestas de error de token: |  |  |
|--- | --- | --- |
| HTTP 400 (solicitud incorrecta) | {&quot;error&quot;: &quot;invalid\_request&quot;} | A la solicitud le falta un parámetro requerido, incluye un valor de parámetro no admitido (que no sea el tipo de concesión), repite un parámetro, incluye varias credenciales, utiliza más de un mecanismo para autenticar al cliente o tiene un formato incorrecto. |
| HTTP 400 (solicitud incorrecta) | {&quot;error&quot;: &quot;invalid\_client&quot;} | Error de autenticación del cliente porque se desconocía el cliente. El SDK *MUST* vuelva a registrarse en el servidor de autorización. |
| HTTP 400 (solicitud incorrecta) | {&quot;error&quot;: &quot;unauthorized\_client&quot;} | El cliente autenticado no tiene autorización para utilizar este tipo de concesión de autorización. |

- en caso de que una MVPD requiera autenticación pasiva, se abrirá un WebView para ejecutar pasive con esa MVPD y se cerrará cuando se complete

- b. checkAuthentication()

   - *true* : vaya a Autorización
   - *false* : vaya a Seleccionar MVPD

- c. getAuthentication : el SDK incluye **access_token** en parámetros de llamada

   - mvpd recordó : vaya a setSelectedProvider(mvpd\_id)
   - mvpd no seleccionado: displayProviderDialog
   - mvpd seleccionado: ir a setSelectedProvider(mvpd\_id)

- d. setSelectedProvider

   - La URL de autenticación mvpd\_id se carga en ChromeCustomTabs
   - inicio de sesión correcto : delegate.setAuthenticationStatus ( SUCCESS )
   - inicio de sesión cancelado : restablecer selección de MVPD
   - El esquema URL se establece como &quot;adobepass://android.app&quot; para capturar cuándo se completa la autenticación

- e. get/checkAuthorization : SDK incluirá **access\_token **en el encabezado como Autorización: Portador **access\_token**

- si la autorización se realiza correctamente, se realizará una llamada para obtener el token de medios

- f. cierre de sesión:

   - El SDK eliminará el token válido para el solicitante actual (las autenticaciones obtenidas por otras aplicaciones y no a través de SSO seguirán siendo válidas)
   - El SDK abrirá las fichas personalizadas de Chrome para llegar al extremo de cierre de sesión de mvpd\_id. Una vez finalizado, se cerrarán las fichas personalizadas de Chrome
   - El esquema de URL se establece como &quot;adobepass://logout&quot; para capturar el momento en que se completa el cierre de sesión
   - el cierre de sesión almacenará en déclencheur sendTrackingData(new Event(EVENT\_LOGOUT,USER\_NOT\_AUTHENTICATED\_ERROR) y una llamada de retorno : setAuthenticationStatus(0,&quot;Logout&quot;)



**Nota:** ya que cada llamada requiere un **access_token**, los posibles códigos de error siguientes se gestionan en el SDK.

| Respuestas de error |  |  |
|--- | --- | --- |
| invalid_request | 400 | La solicitud tiene un formato incorrecto. El SDK debe dejar de realizar llamadas al servidor. |
| invalid_client | 403 | El ID de cliente ya no tiene permiso para realizar solicitudes. El SDK DEBE volver a realizar el registro de cliente. |
| access_denied | 401 | El access_token no es válido. El SDK DEBE solicitar un nuevo access_token. |
