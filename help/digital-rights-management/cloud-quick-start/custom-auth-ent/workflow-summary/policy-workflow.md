---
title: Detalles del flujo de trabajo de políticas
description: Detalles del flujo de trabajo de políticas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Flujo de trabajo de BEES {#bees-workflow}

**Resumen:**

* **Política** - Cree una política de reconocimiento de ABEJAS de DRM que indique que se requiere ABEJAS para todo el contenido empaquetado usando esta política.
* **Empaquetando** - Empaquetar contenido utilizando la política DRM según BEES.
* **Autenticación** : autentique el dispositivo cliente y utilice la API de DRM de Primetime o la API de Primetime para asociar este token con Primetime Cloud DRM. Si lo hace, el dispositivo cliente enviará este token de autenticación hasta Primetime Cloud DRM junto con todas las solicitudes de licencia. Primetime Cloud DRM no procesará este token, sino que lo pasará (como un blob opaco) a su extremo BEES para su procesamiento.
* **Licencias** - Solicite una licencia para su contenido protegido. El dispositivo cliente agregará automáticamente el token de autenticación establecido previamente a la llamada.
* **Derecho** : Primetime Cloud DRM determinará que el contenido se ha empaquetado con una política que requiere BEES. Primetime Cloud DRM construirá una solicitud JSON para enviarla al extremo BEES. La respuesta de BEES indicará a Primetime Cloud DRM si debe o no emitir una licencia y, opcionalmente, qué política de DRM utilizar.

## Detalles del flujo de trabajo de políticas {#policy-workflow-details}

Cuando Primetime Cloud DRM procesa una solicitud de licencia, analiza la política de DRM en la solicitud para determinar si se requiere una llamada a un servicio de derechos de back-end antes de que se pueda mostrar el contenido. Si una llamada de BEES *es* Si es necesario, Primetime Cloud DRM creará la solicitud BEES y, a continuación, analizará la directiva DRM para obtener un punto final de URL de BEES especificado para la solicitud BEES.

Aplique la directiva DRM que indica el requisito BEES, especificando las dos propiedades personalizadas siguientes en la directiva:

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Por ejemplo, con el Administrador de directivas DRM de Primetime ( [!DNL AdobePolicyManager.jar]), debe especificar las dos propiedades personalizadas siguientes en la variable [!DNL flashaccesstools.properties] archivo de configuración:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Si ya está utilizando `policy.customProp.1` o `policy.customProp.2` para otra propiedad, simplemente utilice números únicos para las propiedades más recientes.

## Detalles del flujo de trabajo Empaquetar {#package-workflow-details}

Durante el empaquetado de su contenido protegido contra el acceso al Adobe, debe aplicar al contenido una de las políticas DRM que tengan en cuenta BEES.

## Detalles del flujo de trabajo de autenticación {#authentication-workflow-details}

Para que el extremo BEES pueda tomar decisiones de asignación de derechos, el dispositivo cliente debe proporcionar información de autenticación. Para ello, utilice su propio token de autenticación específico del cliente.

Primetime Cloud DRM no tiene que entender este token: simplemente pasa este token a su extremo BEES. El dispositivo cliente es responsable de crear o adquirir este token y configurarlo con `DRMManager.setAuthenticationToken()` API.

Haga lo siguiente para asociar este token con Primetime Cloud DRM y así enviarlo con la solicitud de licencia:

Crear una instancia de `DRMManager` con los metadatos DRM del contenido empaquetado para DRM de Primetime Cloud.

El `setAuthenticationToken()` Este método funciona asociando la matriz de bytes determinada con la URL del servidor de licencias proporcionada en los metadatos DRM utilizados para crear instancias `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

El token se envía con todas las solicitudes de licencia hasta que se borra llamando a `.setAuthenticationToken` con nulo como parámetro.

## Detalles del flujo de trabajo de licencias{#license-workflow-details}

Solicite una licencia de DRM de Primetime Cloud llamando a `mgr.loadVoucher()`.

## Detalles de solicitud y respuesta de derecho{#entitlement-request-and-response-details}

Cuando Primetime Cloud DRM determina que el contenido se ha empaquetado con una directiva DRM según BEES, crea la siguiente solicitud JSON para enviarla al extremo BEES especificado en la directiva DRM:

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}
```

Se espera la siguiente respuesta del extremo BEES:

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}
```

Primetime Cloud DRM utiliza la respuesta para determinar si debe emitir o no una licencia al dispositivo solicitante y si debe sustituir una nueva directiva DRM en el proceso de generación de licencias. If `isAllowed` es `true` y no se proporciona ninguna política en la respuesta, la política DRM original utilizada durante el tiempo de empaquetado del contenido se utilizará para generar la licencia.
