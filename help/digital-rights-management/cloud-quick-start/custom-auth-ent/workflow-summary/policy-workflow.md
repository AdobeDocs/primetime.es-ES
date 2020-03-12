---
seo-title: Detalles del flujo de trabajo de directivas
title: Detalles del flujo de trabajo de directivas
uuid: b355fcf6-3416-440f-9b30-a155e20f9f74
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Flujo de trabajo de BEES {#bees-workflow}

**Resumen:**

* **Política** : cree una directiva DRM para BEES que indique que BEES es necesaria para todo el contenido empaquetado con esta directiva.
* **Empaquetado** : empaquete contenido con la directiva DRM compatible con BEES.
* **Autenticación** : autentique el dispositivo cliente y utilice la API de DRM de Primetime, o la API de Primetime, para asociar este token a DRM de Primetime Cloud. Si lo hace, el dispositivo cliente enviará este autentificador a Primetime Cloud DRM junto con todas las solicitudes de licencia. Primetime Cloud DRM no procesará el listado, sino que lo transmitirá (como un blob opaco) a su extremo BEES para su procesamiento.
* **Licencias** : solicite una licencia para el contenido protegido. El dispositivo cliente anexará automáticamente el autentificador establecido anteriormente a la llamada.
* **Asignación de derechos** : Primetime Cloud DRM determinará que el contenido se empaquetó con una política que requiere BEES. Primetime Cloud DRM construirá una solicitud JSON para enviar al extremo BEES. La respuesta de BEES indicará a Primetime Cloud DRM si desea o no emitir una licencia y, opcionalmente, qué política de DRM utilizar.

## Detalles del flujo de trabajo de directivas {#policy-workflow-details}

Cuando Primetime Cloud DRM procesa una solicitud de licencia, analiza la directiva DRM en la solicitud para determinar si se requiere una llamada a un servicio de asignación de derechos back-end para poder mostrar el contenido. Si *se requiere* una llamada BEES, Primetime Cloud DRM creará la solicitud BEES y, a continuación, analizará la directiva DRM para obtener un extremo de URL BEES especificado para la solicitud BEES.

Aplique la directiva DRM que indica el requisito BEES, especificando las dos siguientes propiedades personalizadas en la directiva:

    * `policy.customProp.1=bees.required=&lt;true| false>`
    * `policy.customProp.2=bees.url=&lt;url a su extremo BEES>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Por ejemplo, con el Administrador de directivas de DRM de Primetime ( [!DNL AdobePolicyManager.jar]), especificaría las dos propiedades personalizadas siguientes en el archivo de configuración [!DNL flashaccesstools.properties] :

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Si ya está utilizando `policy.customProp.1` o `policy.customProp.2` para otra propiedad, simplemente utilice números únicos para las propiedades más nuevas.

## Detalles del flujo de trabajo del paquete {#package-workflow-details}

Durante el empaquetado del contenido protegido con Adobe Access, debe aplicar al contenido una de las directivas DRM compatibles con BEES.

## Detalles del flujo de trabajo de autenticación {#authentication-workflow-details}

Para que el extremo BEES pueda tomar decisiones de asignación de derechos, el dispositivo cliente debe proporcionar información de autenticación. Esto se logra mediante el uso de su propio autentificador específico del cliente.

Primetime Cloud DRM no tiene que entender este token: simplemente pasa este token a su extremo BEES. El dispositivo cliente es responsable de crear o adquirir este token y de configurarlo mediante la `DRMManager.setAuthenticationToken()` API.

Para asociar este token con Primetime Cloud DRM, haga lo siguiente para que se envíe con la solicitud de licencia:

Cree una instancia del `DRMManager` objeto con los metadatos DRM del contenido empaquetado para DRM de Primetime Cloud.

El `setAuthenticationToken()` método funciona asociando la matriz de bytes dada con la URL del servidor de licencias proporcionada en los metadatos DRM que se utilizaron para crear instancias `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

El token se envía con todas las solicitudes de licencia hasta que se borra el token llamando `.setAuthenticationToken` con null como parámetro.

## Detalles del flujo de trabajo de licencias{#license-workflow-details}

Solicite una licencia de Primetime Cloud DRM llamando `mgr.loadVoucher()`.

## Detalles de solicitud y respuesta de asignación de derechos{#entitlement-request-and-response-details}

Cuando Primetime Cloud DRM determina que el contenido se empaquetó con una directiva DRM compatible con BEES, crea la siguiente solicitud JSON para enviarla al extremo BEES especificado en la directiva DRM:

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

Se espera la siguiente respuesta del criterio de valoración de BEES:

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

Primetime Cloud DRM utiliza la respuesta para determinar si debe o no emitir una licencia al dispositivo solicitante y si debe sustituir una nueva directiva DRM en el proceso de generación de licencias. Si `isAllowed` se proporciona `true` y no se proporciona ninguna política en la respuesta, se utilizará la directiva DRM original utilizada durante el tiempo de empaquetado de contenido para generar la licencia.