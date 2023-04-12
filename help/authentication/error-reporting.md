---
title: Informes de errores
description: Informes de errores
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# Informes de errores {#error-reporting}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Información general {#overview}

Los informes de errores en la autenticación de Adobe Primetime se implementan actualmente de dos maneras diferentes:

* **Informes de errores avanzados** El implementador registra una llamada de retorno de error en caso de que el [SDK de JavaScript de AccessEnabler](#accessenabler-javascript-sdk) o implementa un método de interfaz denominado &quot;`status`&quot; en el caso de que [SDK de AccessEnabler iOS/tvOS](#accessenabler-ios-tvos-sdk) y [SDK para Android de AccessEnabler](#accessenabler-android-sdk), para recibir informes de errores avanzados. Los errores se clasifican en **Información**, **Advertencia** y **Error** tipos. Este sistema de informes es **asincrónico** en el **no hay garantía de orden en el que se activarán varios errores**.  Para obtener más información sobre el sistema avanzado de informes de errores, consulte [Informes de errores avanzados](#advanced-error-reporting) para obtener más información.

* **Informe de errores original -** Sistema de informes estático en el que se pasan mensajes de error a funciones de llamada de retorno específicas cuando falla una solicitud específica. Los errores se agrupan en tipos genéricos, de autenticación y de autorización. Para obtener la lista de errores notificados en el sistema original, consulte la [Informe de errores original](#original-error-reporting) para obtener más información.


## Informes de errores avanzados {#advanced-error-reporting}

* [SDK de JavaScript de AccessEnabler](#accessenabler-javascript-sdk)
* [SDK de AccessEnabler iOS/tvOS](#accessenabler-ios-tvos-sdk)
* [SDK para Android de AccessEnabler](#accessenabler-android-sdk)
* [SDK de AccessEnabler FireOS](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>El viejo [Informe de errores original](#original-error-reporting) La API seguirá funcionando como hasta ahora, el informe de errores avanzado no interrumpe la funcionalidad, pero el informe de errores original NO recibirá más actualizaciones. Todos los nuevos errores y actualizaciones se producirán en el sistema avanzado de informes de errores.

### SDK de JavaScript de AccessEnabler {#accessenabler-javascript-sdk}

El nuevo sistema de informes de errores se deja opcional, por lo que el implementador puede registrar explícitamente una llamada de retorno del controlador de errores para recibir informes de errores avanzados. El sistema incluye la posibilidad de registrar y cancelar el registro de varias llamadas de retorno de errores de forma dinámica. Además, puede registrar cualquier llamada de retorno de error nueva en cuanto se cargue el SDK de JavaScript de AccessEnabler, sin necesidad de realizar ninguna otra inicialización (antes de llamar a `setRequestor()`), lo que significa que puede recibir informes avanzados sobre errores de inicialización y configuración.


#### Implementación {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


La función de llamada de retorno del controlador de error recibirá un solo objeto (un mapa) con la siguiente estructura:

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

### 1. Enlace {#bind}

**`.bind(eventType:String, handlerName:String):void`**

Adjunta un controlador para un evento.

**`eventType`** - SOLO el`errorEvent`&quot; hace que el SDK de JavaScript de AccessEnabler active las llamadas de retorno de informes de error avanzados.

**`handlerName`** - una cadena que especifica el nombre de la función del controlador de errores.\
 

Ambos parámetros de enlace solo deben utilizar caracteres del siguiente conjunto: `[0-9a-zA-Z][-._a-zA-Z0-9]`; es decir, los parámetros deben comenzar con un número o letra y, a continuación, solo pueden incluir guiones, puntos, guiones bajos y caracteres alfanuméricos.  Además, los parámetros no pueden superar los 1024 caracteres.  

**Ejemplo** de controladores de errores de enlace:

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

Debido a limitaciones técnicas, no se puede enlazar un cierre o una función anónima. Debe especificar el nombre del método en el segundo parámetro.

 
### 2. Desenlazar {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

Quita un controlador de eventos adjunto anteriormente.

**`eventType`** - SOLO el`errorEvent`El valor &#39; hace que el SDK de JavaScript de AccessEnabler active las llamadas de retorno de informes de error avanzados.

**`handlerName`** - una cadena que especifica el nombre de la función del controlador de errores, si es nulo o si faltan todos los controladores adjuntos para el `eventType` se eliminará.

Ambos parámetros de enlace solo deben utilizar caracteres del siguiente conjunto: `[0-9a-zA-Z][-._a-zA-Z0-9]`; es decir, los parámetros deben comenzar con un número o letra y, a continuación, solo pueden incluir guiones, puntos, guiones bajos y caracteres alfanuméricos.  Además, los parámetros no pueden superar los 1024 caracteres.  

**Ejemplo** de quitar un único controlador de error:

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**Ejemplo** quitar todos los controladores de errores:

`accessEnabler.unbind('errorEvent');`


### SDK de AccessEnabler iOS/tvOS {#accessenabler-ios-tvos-sdk}

El nuevo sistema de informes de errores es obligatorio, por lo tanto el implementador debe cumplir explícitamente el nuevo protocolo Objective C &quot;EntitlementStatus&quot;. Este nuevo enfoque permite a los programadores recibir informes de errores avanzados.

#### Implementación {#accessenab-ios-tvossdk-imp}

Un implementador debe cumplir lo siguiente **EntitlementStatus** protocolo:

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

Su **status** recibirá un único objeto (un `NSDictionary`) con la siguiente estructura:

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. Declaración**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. Implementación**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### SDK para Android de AccessEnabler {#accessenabler-android-sdk}

El nuevo sistema de informes de errores es obligatorio, ya que el implementador debe cumplir de forma explícita con la función `IAccessEnablerDelegate` protocolo definido por la interfaz. Este nuevo enfoque permite a los programadores recibir informes de errores avanzados.

#### Implementación {#access-enablr-androidsdk-imp}

Un implementador debe gestionar el nuevo `status` método de la interfaz`IAccessEnablerDelegate`. La variable **`status`** recibirá una sola función **`AdvancedStatus`** que tengan el siguiente modelo:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Ejemplo**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### SDK de AccessEnabler FireOS {#accessenabler-fireos-sdk}


El nuevo sistema de informes de errores es obligatorio, ya que el implementador debe cumplir de forma explícita con la función `IAccessEnablerDelegate` protocolo definido por la interfaz. Este nuevo enfoque permite a los programadores recibir informes de errores avanzados.

#### Implementación {#access-enab-fireos-sdk-}

Un implementador debe gestionar el nuevo `status`método de la interfaz`IAccessEnablerDelegate`. La variable **`status`** recibirá una sola función **`AdvancedStatus`** que tengan el siguiente modelo:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Ejemplo**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## Referencia de códigos de error avanzados {#advanced-error-codes-reference}

En la tabla siguiente se enumeran y describen los códigos de error expuestos por la API de error más reciente, así como las acciones sugeridas que se deben llevar a cabo para corregirlos:

| ID | Nivel | Descripción | Acciones de desarrollador | Acciones del usuario | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL y AAPL_ERROR | Error | Error SSO de Apple genérico | El error contiene un campo de detalles con el error original de VSA. | n.a | n.a | Sí | n.a |
| VSA203 | Información | El usuario decidió cerrar la sesión de la aplicación mientras la autenticación se producía como resultado de un inicio de sesión a través del SSO de la plataforma. | Indique o solicite al usuario que cierre la sesión explícitamente desde Configuración -> Cuentas -> Proveedor de TV en tvOS. <br><br> Indique o solicite al usuario que cierre la sesión explícitamente desde Configuración -> Proveedor de TV en iOS/iPadOS. | Cierre sesión explícitamente desde Configuración -> Cuentas -> Proveedor de TV en tvOS. <br> <br> Cerrar sesión explícitamente desde Configuración -> Proveedor de TV en iOS/iPadOS | n.a | Sí | n.a |
| VSA404 | Información | El permiso de la cuenta del suscriptor de vídeo de la aplicación es indeterminado. | Invite a los usuarios que se nieguen a conceder permiso para acceder a la información de suscripción explicando las ventajas de la experiencia de usuario del inicio de sesión único (SSO). | El usuario puede cambiar su decisión accediendo a la configuración de la aplicación (acceso del proveedor de TV) o a la sección desde Configuración -> Proveedor de TV en iOS/iPadOS o Configuración -> Cuentas -> Proveedor de TV en tvOS. | n.a | Sí | n.a |
| VSA503 | Información | Error en la solicitud de metadatos de la cuenta del suscriptor de vídeo de la aplicación. | El punto final de MVPD no responde. La aplicación podría devolver al flujo de autenticación normal. | n.a | n.a | Sí | n.a |
| 500 | Error | Error interno | Utilice AccessEnablerDebug e inspeccione los registros de depuración (salida console.log) para determinar qué ha fallado. | n.a | Sí | Sí | n.a |
| SEC403 | Error | Error de seguridad del dominio. El solicitante está utilizando un dominio no válido. Todos los dominios utilizados por un ID de solicitante en particular deben incluirse en la lista blanca de Adobes. | - Cargar AccessEnabler solo desde la lista de dominios permitidos <br> <br> - Adobe de contacto para administrar la lista de dominios admitidos para el ID del solicitante utilizado <br> <br> - iOS: compruebe que está utilizando el certificado correcto y que la firma se ha creado correctamente | n.a | n.a | Sí | n.a |
| SEC412 | Advertencia | [ Disponible en la versión 2.5 ] El ID del dispositivo no coincide. Esto puede suceder siempre que la plataforma subyacente cambie su ID de dispositivo. En este caso, los tokens existentes se borrarán y el usuario ya no se autenticará. Tenga en cuenta que esto sucede legítimamente cuando el usuario utiliza el SDK de JS y está en itinerancia (en JS, la IP del cliente forma parte del ID del dispositivo). De lo contrario, esto podría indicar un intento de fraude: un intento de copiar tokens desde un dispositivo diferente. | - Monitorice el número de advertencias. Si se disparan sin ninguna razón aparente (sin actualizaciones recientes del explorador; nuevos sistemas operativos) que podrían ser un indicador de intentos de fraude.  <br> <br>- De forma opcional, informe al usuario de que debe iniciar sesión de nuevo. | Inicie sesión de nuevo. | Sí | Sí | Sí, de 3,2 |
| SEC420 | Error | Error de seguridad HTTP al comunicarse con los servidores de autenticación de Adobe Primetime. Este error suele producirse cuando se configuran suplantación o proxies. | - Carga `[https://]{SP_FQDN\}` en el explorador y acepte manualmente los certificados SSL, por ejemplo, **https://api.auth.adobe.com** o **https://api.auth-staging.adobe.com** <br> <br>- Marcar los certificados de proxy como de confianza | Si esto ocurre para un usuario normal, es una indicación de un posible ataque de intermediario. | Sí | Sí | Sí, de 3,2 |
| CFG100 | Advertencia | La fecha/hora/zona horaria del equipo cliente no está configurada correctamente. Esto probablemente lleve a errores de autenticación/autorización. | - Informar al usuario para que establezca la hora correcta. <br> <br> Realice acciones para evitar flujos de derechos, ya que es probable que fallen. | Establezca la fecha y hora correctas. | Sí | Sí | Sí, de 3,2 |
| CFG400 | Error | Se ha proporcionado un ID de solicitante no válido. | El desarrollador DEBE especificar un ID de solicitante válido. | n.a | Sí | Sí | Sí, de 3,2 |
| CFG404 | Error | No se encontraron los servidores de autenticación de Adobe Primetime. Esto puede suceder en 3 casos: <br><br> - El desarrollador tiene una suplantación de identidad no válida. <br><br> -El usuario tiene problemas de red y no puede acceder a los dominios de autenticación de Adobe Primetime. <br><br> -Los servidores de autenticación de Adobe Primetime están mal configurados. <br><br>  **Nota:** En Firefox, aparecerá CFG400 en lugar de CFG404 (limitación del navegador) | - Compruebe la falsificación. <br><br> -Compruebe la configuración de red/DNS. <br><br> -Informar al Adobe. | Compruebe la configuración de red/DNS. | Sí | Sí | Sí, de 3,2 |
| CFG410 | Error | AccessEnabler es demasiado antiguo. | Informar al usuario para que borre las cachés. | Borre la caché del explorador. | Sí | n.a | Sí, de 3,2 |
| CFG5xx | Error | Los servidores de autenticación de Adobe Primetime están experimentando errores internos. xx puede ser cualquier número. | : Informe al usuario de la falta de disponibilidad de la autenticación de Adobe Primetime. <br><br> - Omitir la autenticación de Adobe Primetime. <br> <br> - Adobe de información. | Inténtelo más tarde. | Sí | Sí | Sí, de 3,2 |
| N000 | Información | El usuario no está autenticado. | n.a | Inicie sesión. | Sí | Sí | Sí, de 3,2 |
| N001 | Información | Se inició un intento de autenticación pasiva en segundo plano. Esto sucede con los MVPD configurados con &quot;Autenticación por solicitante&quot;. Aunque es de esperar que el usuario se autentique automáticamente, esto conlleva una penalización del rendimiento en la inicialización. | Si lo desea, informe al usuario o presente la interfaz de usuario que alerta al usuario de que &quot;el trabajo está en curso&quot;. | Espera. | Sí | Sí | Sí, de 3,2 |
| N003 | Información | El usuario selecciona la opción &quot;Otro proveedor de TV&quot; del selector de MVPD de Apple. | La variable *displayProviderDialog* se llamará a la rellamada y la aplicación podría devolver al flujo de autenticación normal. | Seleccione MVPD normal y continúe con la pantalla de inicio de sesión. | n.a | Sí | n.a |
| N004 | Información | El usuario selecciona un proveedor de TV no compatible con el solicitante actual. | La variable *displayProviderDialog* se llamará a la rellamada y la aplicación podría devolver al flujo de autenticación normal. | Seleccione MVPD normal y continúe con la pantalla de inicio de sesión. | n.a | Sí | n.a |
| N005 | Información | Se canceló el selector de MVPD. | n.a | n.a | Sí | Sí | Sí, de 3,2 |
| N010 | Advertencia | El usuario se autenticó mientras la regla de degradación autenticar todo estaba establecida para el MVPD seleccionado. | Opcionalmente, informen al usuario que está recibiendo acceso gratuito &quot;gratuito&quot; debido a las dificultades de MVPD. | n.a | Sí | Sí | Sí, de 3,2 |
| N011 | Información | El usuario se autenticó usando TempPass. | - Informar al usuario. <br> <br> - Opcionalmente, presentar una lista de MVPD normales. | Opcionalmente, inicie sesión con su MVPD normal. | Sí | Sí | Sí, de 3,2 |
| N111 | Advertencia | Expiró TempPass. | - Informar al usuario. <br> <br> - Presente una lista de MVPD normales. <br> <br> - Ocultar la opción TempPass. | Inicie sesión con su MVPD normal. | Sí | Sí | Sí, de 3,2 |
| N130 | Error | **Token de autenticación no encontrado en la sesión.**  Esto puede deberse a uno de los siguientes motivos: <br> <br> 1. El explorador tiene deshabilitadas las cookies (de terceros) (no aplicable al SDK de JavaScript de AccessEnabler versión 4.x) <br> <br> 2. El explorador tiene habilitado el seguimiento entre sitios (Safari 11+) <br> <br> 3. La sesión ha caducado <br> <br> 4. El programador llama a las API de autenticación en sucesión incorrecta <br> <br> NOTA: Este código de error no está disponible para flujos de autenticación de redireccionamiento de página completa. | 1. Solicitar al usuario que habilite las cookies (de terceros) <br> <br> 2. Recomendar al usuario que deshabilite el seguimiento entre sitios <br> <br> 3. Solicitar al usuario que vuelva a autenticarse <br> <br> 4. Llame a las API en el orden correcto | 1. Habilitar cookies (de terceros) <br> <br> 2. Deshabilitar el seguimiento entre sitios <br> <br> 3. Volver a autenticar <br> <br> 4. N/D | Sí | Sí | Sí, de 3,2 |
| N500 | Error | Error interno. <br> <br> Nota: Este es el error original del sistema de errores &quot;Error de autenticación genérico&quot; y &quot;Error de autenticación interna&quot;. Este error se eliminará gradualmente. | Utilice AccessEnablerDebug e inspeccione los registros de depuración (salida console.log) para determinar qué ha fallado. | n.a | Sí | Sí | n.a |
| R401 | Error | Error al intentar obtener un token de acceso. <br> <br> Nota: Este es un error irrecuperable. Informe al usuario de que la aplicación no está disponible. | - iOS: Compruebe la declaración de software y los esquemas personalizados en su aplicación. <br> <br> - JavaScript: Compruebe la declaración de software en la aplicación de sitio web. <br> <br> Abra un ticket con Zendesk e informe al usuario de que el sistema no está disponible temporalmente | n.a | Sí Desde la versión 4.0 | Sí Desde v3.0 | Sí, de 3,2 |
| R400 | Error | La aplicación no está registrada. La instrucción de software no es válida o se ha revocado. <br> <br> Nota: Este es un error irrecuperable. Informe al usuario de que la aplicación no está disponible. | - iOS: Compruebe la declaración de software y los esquemas personalizados en su aplicación. <br> <br> - JavaScript: Compruebe la declaración de software en la aplicación de sitio web. <br> <br> Abra un ticket con Zendesk e informe al usuario de que el sistema no está disponible temporalmente | n.a | Sí Desde la versión 4.0 | Sí Desde v3.0 | Sí, de 3,2 |
| REG500 | Error | No se pudo recuperar el código de registro del servidor. <br> <br> Nota: Este es un error irrecuperable. Informe al usuario de que la aplicación no está disponible. | Abra un ticket con Zendesk e informe al usuario de que el sistema no está disponible temporalmente. | n.a | Sí Desde la versión 4.0 | Sí Desde v3.0 | Sí, de 3,2 |
| REGCODE | Correcto | La aplicación denominada API setSelectedProvider en la plataforma tvOS. | Indique o solicite al usuario que utilice un segundo dispositivo (pantalla) para iniciar sesión con el código de registro proporcionado. | Utilice el regcode en un segundo dispositivo (pantalla) para iniciar la autenticación. | n.a | Sí Solo para tvOS | n.a |
| Z010 | Advertencia | El usuario fue autorizado mientras la regla de degradación autenticar-todo o autorizar-todo estaba establecida para el MVPD seleccionado. | Opcionalmente, informen al usuario que está recibiendo acceso gratuito &quot;gratuito&quot; debido a las dificultades de MVPD. | n.a | Sí | Sí | Sí, de 3,2 |
| Z011 | Información | El usuario estaba autorizado mediante TempPass | Informar al usuario de forma opcional | n.a | Sí | Sí | Sí, de 3,2 |
| Z100 | Error | Error de autorización porque el usuario no tiene suscripción para el recurso solicitado o por otros motivos que se originan en el MVPD, por ejemplo, el vídeo no coincide con la configuración de Control parental de la cuenta de usuario | - No permitir la reproducción. <br> <br> - Informar al usuario. <br> <br> - La clave &quot;message&quot; del mensaje de error PUEDE contener un mensaje más detallado proporcionado por el MVPD. | n.a | Sí | Sí | Sí, de 3,2 |
| Z110 | Error | Autorización denegada debido a denegaciones repetidas de MVPD. Posible intento de fraude o DOS. | - No permitir la reproducción. <br> <br> - Informar al usuario. | n.a | Sí | Sí | Sí, de 3,2 |
| Z120 | Error | Autorización denegada por razones técnicas para comunicarse con el MVPD. Posible error de red. | - No permitir la reproducción. <br> <br> - Informar al usuario de que el MVPD experimentó dificultades y que debe intentarlo más tarde. | Inténtelo más tarde. | Sí | Sí | Sí, de 3,2 |
| Z130 | Error | Autorización denegada porque se usó un recurso no válido/con formato incorrecto. | Compruebe la cadena del recurso y corríjala. Generalmente, este error se debe a un MRSS mal formado o al uso de una cadena sin formato en lugar de MRSS. | n.a | Sí | Sí | Sí, de 3,2 |
| Z169 | Error | Autorización denegada porque se ha aplicado la regla de degradación authzNone al recurso especificado. | Informar al usuario | n.a | Sí | Sí | Sí, de 3,2 |
| Z500 | Error | Error interno. <br> <br>  Nota: este es el heredado &quot;Error de autenticación genérico&quot; y &quot;Error de autenticación interna&quot;. Este error se eliminará gradualmente. | Utilice AccessEnablerDebug e inspeccione los registros de depuración (salida console.log) para determinar qué ha fallado. | n.a | Sí | Sí | Sí, de 3,2 |
| P100 | Error | Error de preautorización. Lo más probable es que esto se deba a la solicitud de autorización para demasiados recursos. | - NO utilice más del número máximo de recursos permitidos. <br> <br> - Póngase en contacto con el soporte de autenticación de Adobe Primetime para encontrar o configurar el número máximo de recursos permitidos. | n.a | Sí Desde v3.0 | Sí | Sí, de 3,2 |
| IS2XX | Error | Estos códigos de error se devuelven cuando los datos de respuesta de extremo del servidor de individualización tienen un formato no válido o no tienen la información de individualización necesaria. | Abra un ticket con Zendesk e informe al usuario de que el sistema no está disponible temporalmente | n.a | Sí Desde v3.0 | n.a | n.a |
| IS4XX | Error | Estos códigos de error se devuelven en caso de error 4XX del extremo del servidor de individualización: es el código de estado HTTP de la respuesta. | Abra un ticket con Zendesk e informe al usuario de que el sistema no está disponible temporalmente | n.a | Sí Desde v3.0 | n.a | n.a |
| IS5XX | Error | Estos códigos de error se devuelven en caso de error 5XX del extremo del servidor de individualización: es el código de estado HTTP de la respuesta. | Abra un ticket con Zendesk e informe al usuario de que el sistema no está disponible temporalmente | n.a | Sí Desde v3.0 | n.a | n.a |
| IS0 | Error | Este código se devuelve cuando el extremo del servidor de individualización no responde en absoluto, por lo que se ha agotado el tiempo de espera de la conexión | Abra un ticket con Zendesk e informe al usuario de que el sistema no está disponible temporalmente | n.a | Sí Desde v3.0 | n.a | n.a |
| LS011 | Advertencia | AccessEnabler está usando un almacenamiento de información volátil debido a problemas de LSO/LocalStorage y WebStorage (o falta de disponibilidad). <br> <br> La autenticación/autorización no persiste más allá de la página actual. Cada carga de página resultará en que el usuario necesite autenticarse. Los TTL configurados no se aplican a todas las recargas de página. | - Informar al usuario de las limitaciones. <br> <br> - Informar al usuario sobre cómo aumentar el espacio de almacenamiento disponible. <br> <br> - Alternativamente cierre de sesión para borrar el almacenamiento. | - Aumente el almacenamiento de información. <br> <br> - Cierre la sesión para borrar el almacenamiento. | Sí | n.a | n.a |

<br>

## Informe de errores original {#original-error-reporting}

En esta sección se describe el sistema original de informes de errores, junto con los códigos de error originales. En el sistema original de informes de errores, AccessEnabler pasa errores a estas dos funciones de llamada de retorno: `setAuthenticationStatus()` después de una llamada a `checkAuthentication()`; `tokenRequestFailed()`, después del error de una llamada a `checkAuthorization()` o `getAuthorization()`.

Los informes de errores originales y las API de estado siguen funcionando exactamente como antes. Sin embargo, en adelante, las API de informes de errores originales no se actualizarán. Todos los nuevos informes de errores y las actualizaciones de los errores antiguos se reflejarán SOLO en la nueva [Sistema de informes de errores avanzado](#advanced-error-reporting).


Para ver ejemplos sobre el uso del sistema original de informes de errores, consulte la [Referencia de la API de JavaScript](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) y [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) funciones, [Referencia de la API de iOS/tvOS](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)y [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Referencia de la API de Android](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) y [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### Códigos de error de devolución de llamada originales {#original-callback-error-codes}

| **Errores genéricos** |  |
|---|---|
| Error interno | Error del sistema al intentar procesar la solicitud. |
| Error de proveedor no seleccionado | Se produce cuando el cliente cancela en el cuadro de diálogo de selección del proveedor. |
| Error de proveedor no disponible | Se produce cuando no hay proveedores disponibles. |
|  |  |
| **Errores de autenticación** |  |
| Error de autenticación genérico | Se devuelve cuando el motivo no se conoce o no se puede publicar. |
| Error de autenticación interna | Error del sistema al intentar la autenticación. |
| Error autenticado del usuario | El usuario no está autenticado. |
|  |  |
| **Errores de autorización** |  |
| Error de autorización genérico | Se devuelve cuando el motivo no se conoce o no se puede publicar. |
| Error de autorización interna | Error del sistema al intentar autorizar. |
| Error de usuario no autorizado | El cliente no está autorizado a ver el contenido solicitado. |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->