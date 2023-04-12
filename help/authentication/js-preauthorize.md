---
title: Preautorizar
description: Preautorización de JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# Preautorizar {#js-preauthorize}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#preauth-overview}

Las aplicaciones deben utilizar el método de API de preautorización para obtener decisiones de preautorización para uno o varios recursos. La solicitud de API de preautorización debe utilizarse para sugerencias de interfaz de usuario o filtrado de contenido. Se debe realizar una solicitud de API de autorización real antes de permitir que el usuario acceda a los recursos especificados.

Si se produce un error inesperado (por ejemplo, un problema de red y un extremo de autorización de MVPD no disponible) cuando los servicios de autenticación de Adobe Primetime procesan una solicitud de API de preautorización, se incluirá una o varias informaciones de error independientes para los recursos afectados como parte del resultado de respuesta de API de preautorización.

### public preauthorization(request: PreauthorizationRequest, llamada de retorno: AccessEnablerCallback&lt;any>): void {#preauth-method}

**Descripción:** Este método lo utilizarán las aplicaciones para obtener decisiones de preautorización (informativas) del usuario autenticado del servicio de autenticación de Adobe Primetime para ver recursos protegidos específicos, con el propósito principal de decorar la interfaz de usuario de la aplicación (por ejemplo, indicar el estado de acceso con los iconos de bloqueo y desbloqueo).

**Disponibilidad:** v4.4.0+

**Parámetros:**

* `PreauthorizeRequest`: Objeto de Generador utilizado para definir la solicitud
* `AccessEnablerCallback`: llamada de retorno utilizada para devolver la respuesta de API
* `PreauthorizeResponse`: Objeto utilizado para devolver el contenido de respuesta de la API

### clase PreauthorizedRequestBuilder {#preath-req-builder-class}

#### setResources(resources: string[]): PreauthorizationRequestBuilder {#set-res-preath-req-buildr}

* Establece la lista de recursos para los que desea obtener decisiones de preautorización.
* Es obligatorio configurarlo para el uso de la API de preautorización.
* Cada elemento de la lista debe ser una cadena que represente el valor de ID de recurso o el fragmento RSS de medios que debe acordarse con el MVPD.
* Este método establece la información solo en el contexto de la `PreauthorizeRequestBuilder` instancia de objeto, que es el receptor de esta llamada de método.

* Para generar un `PreauthorizeRequest` puede echar un vistazo a `PreauthorizeRequestBuilder`método de :

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` recursos. Lista de recursos para los que desea obtener decisiones de preautorización.
* `@returns {PreauthorizeRequestBuilder}` La referencia a la misma `PreauthorizeRequestBuilder` instancia de objeto, que es el receptor de la llamada de método.
* Esto permite la creación de encadenamientos de métodos.

#### disableFeatures(...características: string[]): PreauthorizationRequestBuilder {#disabl-featres-preauth-req-buildr}

* Establece las funciones que desea que se desactiven al obtener las decisiones de preautorización.
* Esta función establece la información solo en el contexto de la `PreauthorizeRequestBuilder` instancia de objeto, que es el receptor de esta llamada de función.
* Para generar un `PreauthorizeRequest` puede echar un vistazo a `PreauthorizeRequestBuilder`función de :

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` características. Conjunto de funciones que desea que se deshabiliten.
* `@returns` La referencia a la misma `PreauthorizeRequestBuilder` instancia de objeto, que es el receptor de la llamada de función.
* Esto se hace para permitir la creación de encadenamiento de funciones.

#### build(): PreauthorizationRequest {#preauth-req}

* Crea y recupera la referencia de una nueva `PreauthorizeRequest` instancia de objeto.
* Este método crea una instancia de `PreauthorizeRequest` cada vez que se llama a .
* Este método utiliza los valores configurados de antemano en el contexto de la `PreauthorizeRequestBuilder` instancia de objeto, que es el receptor de esta llamada de método.
* Tenga en cuenta que este método no produce efectos secundarios,
* por lo tanto, no altera el estado del SDK ni el estado del `PreauthorizeRequestBuilder` instancia de objeto, que es el receptor de esta llamada de método.
* Significa que las llamadas sucesivas de este método para el mismo receptor crearán nuevas `PreauthorizeRequest` instancias de objeto, pero con la misma información, en caso de que los valores se establezcan en la variable `PreauthorizeRequestBuilder` cuando no se haya modificado entre las llamadas.
* En caso de que no necesite actualizar ninguna de las informaciones proporcionadas (recursos y almacenamiento en caché), puede reutilizar la instancia de PreauthorizedRequest para varios usos de la API de preautorización.
* `@returns {PreauthorizeRequest}`

### interfaz AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(result: T); {#on-response-result}

* La llamada de retorno de respuesta que invoca el SDK cuando se completó la solicitud de API de preautorización.
* El resultado es un resultado correcto o un resultado de error que contiene un estado .
* `@param {T} result`

#### onFailure(result: T); {#on-failure-result}

* La llamada de retorno de error invocada por el SDK cuando no se pudo atender la solicitud de API de preautorización.
* El resultado es un resultado de error que contiene un estado .
* `@param {T} result`

### class PreauthorizedResponse {#preauth-response-class}

#### estado público: Estado; {#public-status}

* Devuelve: Información de estado (estado) adicional en caso de error.
* Podría contener un `null` valor.

#### decisiones públicas: Decisión[]; {#public-decisions}

* Devuelve: Lista de decisiones de preautorización. Una decisión para cada recurso.
* La lista puede estar vacía en caso de error.

### estado de la clase {#class-status}

#### estado público: número; {#public-status-numbr}

* El código de estado de respuesta HTTP como se documenta en RFC 7231.
* Puede ser 0 en caso de que la variable `Status` procede del SDK en lugar de los servicios de autenticación de Adobe Primetime.

#### código público: número; {#public-code-numbr}

* El código de error estándar de los servicios de autenticación de Adobe Primetime.
* Puede contener una cadena vacía o una `null` valor.

#### mensaje público: string; {#public-msg-string}

* El mensaje detallado que en algunos casos es proporcionado por los extremos de autorización de MVPD o por las reglas de degradación del programador.
* Puede contener una cadena vacía o una `null` valor.

#### detalles públicos: string; {#public-details-strng}

* Mantiene un mensaje detallado que en algunos casos es proporcionado por los extremos de autorización de MVPD o por las reglas de degradación del programador.
* Puede contener una cadena vacía o una `null` valor.


#### public helpUrl: string; {#public-help-url-string}

* La URL que vincula a más información sobre por qué se produjo este estado/error y posibles soluciones.
* Puede contener una cadena vacía o una `null` valor.

#### seguimiento público: string; {#public-trace-string}

* El identificador único para esta respuesta, que se puede utilizar al ponerse en contacto con el servicio de asistencia para identificar problemas específicos en escenarios más complejos.
* Puede contener una cadena vacía o una `null` valor.

#### acción pública: string; {#public-action-string}

* La medida recomendada para remediar la situación.
   * **ninguno**: Desafortunadamente no hay ninguna acción predefinida para remediar este problema. Esto podría indicar una invocación incorrecta de la API pública
   * **configuración**: Se necesita un cambio de configuración a través del panel TVE o poniéndose en contacto con el servicio de asistencia técnica.
   * **registro de solicitudes**: La solicitud debe registrarse de nuevo.
   * **autenticación**: El usuario debe autenticarse o volver a autenticarse.
   * **autorización**: El usuario debe obtener autorización para el recurso específico.
   * **degradación**: Debe aplicarse alguna forma de degradación.
   * **reintento**: Volver a intentar la solicitud podría resolver el problema
   * **retry-after**: Volver a intentar la solicitud después del periodo de tiempo indicado podría resolver el problema.
* Puede contener una cadena vacía o una `null` valor.

### decisión de clase {#class-decision}

#### id pública: string; {#public-id-string}

* ID del recurso para el que se obtuvo la decisión.

#### público autorizado: booleano; {#public-auth-boolean}

* El valor del indicador que indica si la decisión es correcta o no.

#### error público: Estado; {#public-error-status}

* Información de estado (estado) adicional en caso de que se produzca algún error. Podría contener un `null` valor.

## Ejemplo de implementación de cliente {#client-imp-example}

```JavaScript
let accessEnablerApi = new window.AccessEnabler.AccessEnabler("software statement");
let accessEnablerModels = window.AccessEnabler.models;



// Build request
let requestBuilder = new accessEnablerModels.PreauthorizeRequest.getBuilder();
let request = requestBuilder
    .setResources(["RES01", "RES02", "RES03"])
    .disableFeatures("LOCAL_CACHE")
    .build();



// Create callback
let callback = {
    onResponse(response) {
        // Handle onResponse
    },
    onFailure(response) {
        // Handle onFailure
    }
};

// Invoke call
accessEnablerApi.preauthorize(request, callback);
```


## Ejemplos de escenario {#scenario-examples}

### Escenario 1: Se autorizaron todos los recursos solicitados {#all-req-res-auth}

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Desactivado</td>
    <td>

```JavaScript
        {
    "decisions": [
        {
        "id": "RES01",
        "authorized": true
        },
        {
        "id": "RES02",
        "authorized": true
        },
        {
        "id": "RES03",
        "authorized": true
        }
    ]
    }    
```

</td>
  </tr>
</tbody>


### Escenario 2: Se autorizaron algunos recursos solicitados. {#sm-req-res-auth}

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Desactivado</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;decisiones&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizado&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizado&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizado&quot;: true
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>Habilitado</td>
    <td>

    &quot;JavaScript
    {
    &quot;decisiones&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizado&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_deny_by_mvpd&quot;,
    &quot;mensaje&quot;: &quot;El MVPD ha devuelto una decisión de \&quot;Denegar\&quot; al solicitar la preautorización para el recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizado&quot;: true
    },
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Escenario 3: No se autorizó ninguno de los recursos solicitados. {#none-req-res-auth}

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Desactivado</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;decisiones&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizado&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizado&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizado&quot;: false
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>Habilitado</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;decisiones&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_deny_by_mvpd&quot;,
    &quot;mensaje&quot;: &quot;El MVPD ha devuelto una decisión de \&quot;Denegar\&quot; al solicitar la preautorización para el recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_deny_by_mvpd&quot;,
    &quot;mensaje&quot;: &quot;El MVPD ha devuelto una decisión de \&quot;Denegar\&quot; al solicitar la preautorización para el recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;maximum_execution_time_expanded&quot;,
    &quot;mensaje&quot;: &quot;La solicitud no se completó en el tiempo máximo permitido. Volver a intentar la solicitud podría resolver el problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;reintento&quot;
    }
    }
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Escenario 4: Solicitud de cliente incorrecta: no se han especificado recursos. {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Deshabilitado/Habilitado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 400,
    &quot;code&quot;: &quot;internal_error&quot;,
    &quot;mensaje&quot;: &quot;La solicitud falló debido a un error interno.&quot;,
    &quot;detalles&quot;: &quot;El parámetro String[] requerido &#39;resource&#39; no está presente&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;none&quot;
    },
    &quot;decisiones&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Escenario 5: Solicitud de cliente incorrecta: se han especificado recursos vacíos. {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Deshabilitado/Habilitado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 412,
    &quot;code&quot;: &quot;missing_resource&quot;,
    &quot;mensaje&quot;: &quot;Falta el parámetro de recurso&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;none&quot;
    },
    &quot;decisiones&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Escenario 6: Error de red. {#ntwrk-error}

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Habilitado</td>
    <td>

    &quot;JavaScript
    {
    &quot;decisiones&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_received_error&quot;,
    &quot;mensaje&quot;: &quot;Error de lectura al recuperar la respuesta del servicio asociado. Volver a intentar la solicitud podría resolver el problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;reintento&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_received_error&quot;,
    &quot;mensaje&quot;: &quot;Error de lectura al recuperar la respuesta del servicio asociado. Volver a intentar la solicitud podría resolver el problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;acción&quot;: &quot;reintento&quot;
    }
    }
    ]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Escenario 7: El flujo de preautorización se invocó sin una sesión de AuthN válida.

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Deshabilitado/Habilitado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;authentication_session_missing&quot;,
    &quot;mensaje&quot;: &quot;No se pudo recuperar la sesión de autenticación asociada con esta solicitud. El usuario debe volver a autenticarse con un MVPD compatible para poder continuar.&quot;,
    &quot;acción&quot;: &quot;autenticación&quot;
    },
    &quot;decisiones&quot;: []
    }
    
    &quot;

</td>
  </tr>
</tbody>
</table>



### Escenario 8: El flujo de preautorización se invocó antes de que se completara la llamada a setRequestor

<table>
<thead>
  <tr>
    <th>Indicador de código de error mejorado</th>
    <th>Respuesta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Deshabilitado/Habilitado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;requestor_not_configured&quot;,
    &quot;mensaje&quot;: &quot;El solicitante aún no está configurado, lo que es un requisito previo para usar cualquier API aparte de la API setRequestor.&quot;,
    &quot;acción&quot;: &quot;reintento&quot;
    },
    &quot;decisiones&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

