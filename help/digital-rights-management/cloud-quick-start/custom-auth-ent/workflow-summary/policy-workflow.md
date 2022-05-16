---
title: Detalles del flujo de trabajo de directivas
description: Detalles del flujo de trabajo de directivas
copied-description: true
exl-id: e3daf7a9-def0-48a9-8190-adb25eec7b59
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Flujo de trabajo BEES {#bees-workflow}

**Resumen:**

* **Política** - Cree una directiva DRM con conocimiento de BEES que indique que BEES es necesaria para todo el contenido empaquetado con esta directiva.
* **Envase** - Empaquete contenido utilizando la directiva DRM con conocimiento de BEES.
* **Autenticación** : autentique el dispositivo cliente y utilice la API de DRM de Primetime o la API de Primetime para asociar este token a DRM de Primetime Cloud. Si lo hace, el dispositivo cliente enviará este token de autenticación a Primetime Cloud DRM junto con todas las solicitudes de licencia. El DRM de Primetime Cloud no procesará este token, sino que lo transmitirá (como un blob opaco) a su punto final de BEES para su procesamiento.
* **Licencias** - Solicite una licencia para su contenido protegido. El dispositivo cliente anexará automáticamente el token de autenticación establecido anteriormente a la llamada.
* **Derecho** : Primetime Cloud DRM determinará que el contenido se empaquetó con una política que requiere BEES. Primetime Cloud DRM construirá una solicitud JSON para enviar al extremo BEES. La respuesta de BEES indicará a Primetime Cloud DRM si emitir o no una licencia y, opcionalmente, qué política de DRM utilizar.

## Detalles del flujo de trabajo de directivas {#policy-workflow-details}

Cuando Primetime Cloud DRM procesa una solicitud de licencia, analiza la política DRM en la solicitud para determinar si se requiere una llamada a un servicio de asignación de derechos backend para poder mostrar el contenido. Si una llamada a BEES *es* Si es necesario, el DRM de Primetime Cloud creará la solicitud de BEES y, a continuación, analizará la política de DRM para obtener un extremo de URL de BEES especificado para la solicitud de BEES.

Aplique su política de DRM que indique el requisito de BEES, especificando las dos siguientes propiedades personalizadas en la directiva:

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Por ejemplo, con el Administrador de políticas de DRM de Primetime ( [!DNL AdobePolicyManager.jar]), debe especificar las dos propiedades personalizadas siguientes en la variable [!DNL flashaccesstools.properties] archivo de configuración:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Si ya está utilizando `policy.customProp.1` o `policy.customProp.2` para otra propiedad, simplemente utilice números únicos para las propiedades más recientes.

## Detalles del flujo de trabajo del paquete {#package-workflow-details}

Durante el empaquetado del contenido protegido por Access en el Adobe, debe aplicar al contenido una de sus políticas DRM con conocimiento de BEES.

## Detalles del flujo de trabajo de autenticación {#authentication-workflow-details}

Para que el punto final de BEES tome decisiones de asignación de derechos, el dispositivo cliente debe proporcionar información de autenticación. Esto se logra mediante el uso de su propio token de autenticación específico del cliente.

El DRM de Primetime Cloud no tiene que comprender este token: simplemente pasa este token a su extremo BEES. El dispositivo cliente es responsable de crear o adquirir este token y de configurarlo mediante la variable `DRMManager.setAuthenticationToken()` API.

Haga lo siguiente para asociar este token a Primetime Cloud DRM para que se envíe con la solicitud de licencia:

Cree una instancia de `DRMManager` con los metadatos DRM del contenido empaquetado para DRM de Primetime Cloud.

La variable `setAuthenticationToken()` funciona asociando la matriz de bytes dada con la URL del servidor de licencias proporcionada en los metadatos DRM que se utilizaron para crear instancias `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

El token se envía con todas las solicitudes de licencia hasta que se borra el token llamando a `.setAuthenticationToken` con null como parámetro.

## Detalles del flujo de trabajo de la licencia{#license-workflow-details}

Solicite una licencia de Primetime Cloud DRM llamando a `mgr.loadVoucher()`.

## Detalles de solicitud y respuesta de derecho{#entitlement-request-and-response-details}

Cuando el DRM de Primetime Cloud determina que el contenido se empaquetó con una directiva DRM según BEES, construye la siguiente solicitud JSON para enviarla al extremo BEES especificado en la directiva DRM:

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

Se espera la siguiente respuesta del punto final de BEES:

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

Primetime Cloud DRM utiliza la respuesta para determinar si debe emitir o no una licencia en el dispositivo solicitante y si debe sustituir una nueva directiva DRM en el proceso de generación de licencias. If `isAllowed` es `true` y no se proporciona ninguna directiva en la respuesta, entonces la directiva DRM original utilizada durante el tiempo de empaquetado de contenido se utilizará para generar la licencia.
