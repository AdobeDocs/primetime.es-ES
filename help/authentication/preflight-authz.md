---
title: Autorización de comprobación previa
description: Autorización de comprobación previa
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---



# Autorización de comprobación previa {#preflight-authorization}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Información general {#overview}

Esta función proporciona una comprobación de autorización ligera para varios recursos. El propósito de esta comprobación ligera es decorar la interfaz de usuario (por ejemplo, indicar el estado de acceso con los iconos de bloqueo y desbloqueo). La autorización previa a la comprobación es lo más ligera y eficaz posible, de modo que una sola llamada a la API arroja el estado de autorización de una lista de recursos. Tenga en cuenta que esta función no es autorizada en lo que respecta a la autorización de un recurso.

A `getAuthorization(resource)` o `checkAuthorization(resource)` debe realizarse antes de permitir la reproducción.

La autorización de comprobación preliminar también es compatible con un caso de uso diferente, en el que el programador debe solicitar autorización para varios ID de recurso para permitir la reproducción de un elemento de contenido multimedia. El Programador puede realizar una comprobación preliminar inicial de los recursos necesarios y, dependiendo de la respuesta, podría fallar pronto si no se cumplen las condiciones comerciales.

Para obtener una lista de MVPD que admiten autorización de comprobación previa, consulte la [Autorización de comprobación preliminar de MVPD](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) página. 

>[!NOTE]
>
> Tenga en cuenta que el uso de esta función para los MVPD que no cuentan con soporte de autorización previa completa debe acordarse previamente con Adobe y MVPD. El uso de la autorización de comprobación preliminar en estos MVPD caerá en el &quot;peor de los casos&quot; descrito [here](/help/authentication/mvpd-preflight-authz.md#intro) y pueden provocar problemas de rendimiento y tiempos de respuesta lentos. </br>
> Además, tenga en cuenta que el uso de la autorización de comprobación previa con **más de 5 recursos deben ser acordados explícitamente por Adobe**.

## API de comprobación previa de AccessEnabler {#AE_pre_api}

AccessEnabler expone un par de funciones API/llamada de retorno para implementar la autorización de comprobación previa. La llamada de API toma un solo parámetro que consiste en una lista de recursos. La función de llamada de retorno toma un solo parámetro que representa los recursos autorizados reales. Los siguientes ejemplos están en ActionScript, pero las llamadas están disponibles en todos los sabores de AccessEnabler.

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

Llame a esta función en el objeto AccessEnabler para solicitar el estado de autorización de una lista de recursos.

El parámetro resources es la lista de recursos para los que se debe comprobar la autorización. Cada elemento de la lista debe ser una cadena que represente el ID del recurso. El ID de recurso está sujeto a las mismas limitaciones que el ID de recurso en la variable `getAuthorization()` , es decir, se acuerda sobre el valor establecido entre el Programador y el MVPD, o un fragmento RSS de medios. Tenga en cuenta que la autenticación de Adobe Primetime no administra los recursos de ninguna manera, excepto por una capa de mediación delgada que puede transformar los formatos de recursos en función de lo que admita realmente el MVPD.

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

Esta es una función de llamada de retorno que debe implementarse en la aplicación de capa superior del programador. AccessEnabler llamará a esta función después de calcular la lista de recursos autorizados.


### Ejemplo de JS

```javascript
    checkPreauthorizedResources(["CNBC","MSNBC"]);
    ...
    preauthorizedResources() {
        var resource = arguments[0];
        for(i in resources) {
            // Do things with resource list
            // such as decorate UI
            ...
        }
    }
```

## Información de implementación {#details}

- [Comprobación previa mediante ChannelID](#preflight_using_channelID)
- [POST/preautorización](#post)
- [Almacenamiento](#storage)

La llamada de API intenta encontrar una lista en caché de recursos autorizados para el usuario actual en el almacenamiento local del cliente. Si no hay lista en caché, se realiza una llamada HTTPS a los servidores de AdobePass para recuperar la lista.

El mecanismo de almacenamiento en caché mejora los tiempos de rendimiento en llamadas subsiguientes al omitir por completo la llamada de red. Además, la lista en caché se puede rellenar de antemano como parte del proceso de autenticación.  (Para obtener información sobre la configuración de este escenario, consulte [Integración de autorizaciones de comprobación previa](/help/authentication/authz-usecase.md#preflight_authz_int) en la sección Autorización de la Guía de integración de MVPD).

Además, la lista almacenada en caché de recursos puede utilizarse potencialmente para optimizar el flujo de autorización, en el sentido de que si existe una lista almacenada en caché de recursos, `checkAuthorization()` puede comprobarlo antes de realizar una llamada de red. Si el recurso no está en la lista de recursos preautorizados, la comprobación puede fallar sin necesidad de llamar a los servidores de autenticación de Primetime.


### Comprobación previa mediante ChannelID {#preflight_using_channelID}

A partir de la versión 2.4.1 de la autenticación Primetime, el flujo de comprobación previa funciona de la siguiente manera:

1. Durante la autenticación, la autenticación de Primetime lee la variable `channelIID` de la respuesta SAML de MVPD, y utiliza este valor para establecer la variable `authorizedResources` en el token de autenticación.
1. Dentro de `checkPreauthorizedResources()` función de API, la autenticación de Primetime comprueba si la variable `authorizedResources` está configurado.
1. Si la variable `authorizedResources` está establecido, la autenticación de Primetime lee ese valor y realiza una intersección entre la lista de recursos de la `authorizedResources` y la lista de recursos recibidos de `checkPreauthorizedResources()` parámetro.  El resultado de esta intersección es la lista final de recursos preautorizados.
1. Si la variable `authorizedResources` no está establecido, ejecute el flujo implementado anteriormente, en el que la lista de recursos recibidos de `checkPreauthorizedResources()` se pasa al PreAuthorizationServlet. Este servlet realiza las llamadas de autorización a los extremos de MVPD y devuelve la lista de recursos preautorizados.

### Ejemplo de comprobación previa con ChannelID

El ejemplo siguiente muestra una línea de canales de ejemplo. Tenga en cuenta que el nombre del atributo utilizado para enviar la lista de canales puede diferir de un MVPD a otro:

```XML
    <saml:Attribute Name="visible_channels" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">MSNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FBN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FNC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TNT</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TBS</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TRUTV</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TOON</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">HBO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">MAX</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">EPIXHD</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">BTN-BTN2GO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">SPEED-SPEED2</saml:AttributeValue>
    </saml:Attribute>
```
 

La variable `authorizedResources` del elemento de autenticación aparece de la siguiente manera:

```JSON
    <authorizedResources>
        <authorizedResource resourceID="MSNBC"/>
        <authorizedResource resourceID="CNBC"/>
        <authorizedResource resourceID="FBN"/>
        <authorizedResource resourceID="FNC"/>
        <authorizedResource resourceID="TNT"/>
        <authorizedResource resourceID="TBS"/>
        <authorizedResource resourceID="CNN"/>
        <authorizedResource resourceID="TRUTV"/>
        <authorizedResource resourceID="TOON"/>
        <authorizedResource resourceID="HBO"/>
        <authorizedResource resourceID="MAX"/>
        <authorizedResource resourceID="EPIXHD"/>
        <authorizedResource resourceID="BTN-BTN2GO"/>
        <authorizedResource resourceID="SPEED-SPEED2"/>
    </authorizedResources>
```

El programador ejecuta el `checkPreauthorizedResources()` Llamada de API, pasando la siguiente lista de parámetros:</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- &quot;TruTV&quot;
- &quot;fbc-fox&quot;

La implementación actual de Preflight realiza la intersección con la lista de recursos de la `authorizedResources` y devuelve esta lista:

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- &quot;TruTV&quot;

 

**Nota:** Tenga en cuenta que la intersección no distingue entre mayúsculas y minúsculas.

 

### POST/preautorización {#post}

AccessEnabler realizará automáticamente esta llamada cuando no exista ninguna lista de recursos en caché, autorizada y en caché. 


#### Solicitud {#req}

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `authentication_token` | string | SÍ | El token de autenticación. |
| `resource_id` | string | SÍ | Un solo recurso. Esto se puede especificar varias veces, una vez para cada elemento de la matriz de recursos suministrada en la variable `checkPreauthorizedResources()` Llamada de API. |


**Nota:** El número máximo de recursos solicitados es configurable.
**El valor predeterminado máximo es 5.**


#### Respuesta {#resp}

La respuesta que devuelve el servlet preauthorization tiene el siguiente formato:

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <resources>
      <resource>
        <id>TNT</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>TBS</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>CNN</id>
        <authorized>false</authorized>
      </resource>
    </resources>
```

### Almacenamiento {#storage}

Una lista de recursos preautorizados que AccessEnabler obtiene del proveedor de servicios. Esta lista de recursos:

- Se almacena junto con los tokens AuthN y AuthZ
- Es válido siempre que el usuario esté en el mismo sitio web o hasta que caduque el token de AuthN
- Se recupera cada vez que el usuario aterriza en un nuevo sitio web integrado de autenticación de Primetime

Cada entrada contiene el ID de recurso para el que el usuario está autorizado previamente.

Por ejemplo:


| ID de recurso | Autorizado |
| ----------- | ---------- |
| CNN | true |
| TNT | false |
| ... | ... |


Esta lista se denomina &quot;caché de preautorización&quot;.

#### Flujo {#flow}

1. La aplicación/sitio del programador hace un `checkPreauthorizedResources(resourceList)` llamada a .
1. AccessEnabler verifica el token de autenticación para los recursos autorizados:
   1. Si el token de autenticación contiene recursos autorizados, esta lista es autoritaria y no se debe realizar ninguna llamada para obtener esta información. Los recursos de resourceList se buscan dentro de la lista de recursos autorizados en el token de autenticación y solo los que se encontraron son devueltos por el `preauthorizedResources()` llamada de retorno.
   1. Si el token de autenticación NO contiene recursos autorizados - `resourceList` se compara con la lista de recursos de la caché de preautorización.
      1. Si la lista contiene los mismos recursos : esto significa que ya se realizó una llamada al servidor y que la respuesta ya está en la caché de preautorización. Solo los recursos autorizados serán devueltos por el `preauthorizedResources()` llamada de retorno.
      1. Si la lista NO contiene los mismos recursos, el cliente debe realizar una llamada al servidor para obtener el estado de autorización de los recursos en resourceList. La respuesta se recuperará y almacenará en la caché de preautorización, reemplazando por completo los recursos antiguos. Solo los recursos autorizados serán devueltos por el `preauthorizedResources()` llamada de retorno.


#### Recuperación de lista {#listRetrieve}

Siempre que `checkPreauthorizedResources()` , la lista de recursos para verificar la autorización se compara con la caché de preautorización. Si la lista contiene el mismo conjunto de recursos, no se realiza ninguna llamada al proveedor de servicios, ya que todos los recursos necesarios para activar la variable `preauthorizedResources()` la rellamada ya está en la caché.


#### logout() {#logout}

La caché de preautorización está vacía al cerrar la sesión.


## Dependencias {#depends}

El rendimiento de la API de comprobación previa depende de implementaciones específicas de MVPD.  Para ver las opciones de implementación, consulte [Integración de autorizaciones de comprobación previa](/help/authentication/authz-usecase.md#preflight_authz_int) en la sección Autorización de la Guía de integración de MVPD.


## Seguridad {#security}

Las API de cliente están disponibles para todos los programadores.

La implementación utiliza HTTPS como transporte, pero para tener una llamada más ligera, no se emplean medidas de seguridad adicionales (sin firmar, sin FAXS).

**Atención:** NO utilice esta API de forma autorizada para determinar si se debe conceder acceso a un usuario a un recurso protegido. El propósito de esta API es la decoración de la interfaz de usuario y/o la predefinición de las decisiones comerciales. La variable `getAuthorization()` y `checkAuthorization()` las llamadas siempre deben realizarse antes de permitir la reproducción.


## Compatibilidad {#compat}

Esta función es compatible con todos los sabores de AccessEnabler: AS, JS, AIR, iOS, Android, Xbox (en flujo AuthN de segunda pantalla).

La autorización de comprobación previa no admite recursos de preautorización que contengan secciones CDATA. El enfoque del sistema de comprobación previa actual es admitir el filtrado a nivel de canal. Los recursos con secciones CDATA son probablemente recursos de nivel de recurso. La comprobación previa es sencilla `mrss` recursos para preautorización a nivel de canal, siempre que no contengan CDATA. 

## Integración Con Otras Funciones {#integ_w_other_features}

Puede producirse una posible optimización en el flujo de autorización para que falle rápidamente si el recurso no está en la lista de recursos preautorizados.

En esta optimización, el extremo de comprobación previa del servidor se integra con el mecanismo de degradación.  

Si se establece una regla &quot;AuthN All&quot; para el MVPD y el solicitante, el extremo de comprobación previa solo reflejará todos los recursos recibidos en la solicitud.

Lo mismo ocurre si &quot;AuthZ All&quot; está habilitado para al menos uno de los recursos presentes en la solicitud.

<!--
## Related Information

  - `checkPreauthorizedResources()`
      - [iOS](#checkPreauth)
      - [Android](#checkPreauth)
      - [JavaScript](#checkPreauthRes)
      - [ActionScript](#checkPreauthRes)
  - [Xbox](#2nd%20Screen%20Authentication)
  - [MVPD Integration Guide: Preflight AuthZ](#)
-->
