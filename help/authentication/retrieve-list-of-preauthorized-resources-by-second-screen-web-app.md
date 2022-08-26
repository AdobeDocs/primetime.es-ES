---
title: Recuperar lista de recursos preautorizados por aplicación web de segunda pantalla
description: Recuperar lista de recursos preautorizados por aplicación web de segunda pantalla
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Recuperar lista de recursos preautorizados por aplicación web de segunda pantalla {#retrieve-list-of-preauthorized-resources-by-second-screen-web-app}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Puntos finales de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descripción {#description}

Una solicitud de autenticación de Adobe Primetime para obtener la lista de recursos preautorizados.

Existen dos conjuntos de API: un conjunto para la aplicación de flujo continuo o el servicio de programación y otro para la aplicación web de segunda pantalla. Esta página describe la API para la aplicación AuthN.

 \
| Punto final | Llamado  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta | | — | — | — | — | — | — | | &lt;sp_fqdn>/api/v1/preauthorization/{código de registro} | Módulo AuthN | 1.  código de registro  </br>    (Componente Ruta)</br>2.  solicitante (obligatorio)</br>3.  lista de recursos (obligatorio) | GET | XML o JSON que contienen decisiones individuales de preautorización o detalles de error. Consulte los ejemplos siguientes. | 200 - Éxito</br></br>400 - Solicitud incorrecta</br></br>401 - No autorizado</br></br>405 - Método no permitido  </br></br>412 - Error en la precondición</br></br>500 - Error interno del servidor |



| Parámetro de entrada | Descripción |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| código de registro | El valor del código de registro proporcionado por el usuario al principio del flujo de autenticación. |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| lista de recursos | Cadena que contiene una lista delimitada por comas de resourceIds que identifica el contenido al que podría acceder un usuario y que es reconocido por los puntos finales de autorización de MVPD. |


### Respuesta de ejemplo {#sample-response}

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4`
Adobe-Response-Confidence : full
Content-Type: application/xml; charset=utf-8

<resources>
    <resource>
        <id>TestStream1</id>
        <authorized>true</authorized>
    </resource>
    <resource>
        <id>TestStream2</id>
        <authorized>false</authorized>  
        <error>
            <status>403</status>
            <code>authorization_denied_by_mvpd</code>
            <message>User not authorized</message>
            <details>Your subscription package does not include the "TestStream3" channel.</details>
            <helpUrl>https://tve.helpdocsonline.com/errors/preauthorization_denied</helpUrl>
            <trace>0453f8c8-167a-4429-8784-cd32cfeaee58</trace>
            <action>none</action>
        </error>
    <resource>
</resources>
```

**JSON:**

```JSON
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/json; charset=utf-8
 
{
   "resources" : [
        {
            "id" : "TestStream1",
            "authorized" : true
        },
        {
            "id" : "TestStream3",
            "authorized" : false,
            "error" : {
               "status" : 403,
               "code" : "authorization_denied_by_mvpd",
               "message" : "User not authorized",
               "details" : "Your subscription package does not include the "TestStream3" channel.",
               "helpUrl" : "https://tve.helpdocsonline.com/errors/preauthorization_denied",
               "trace" : "0453f8c8-167a-4429-8784-cd32cfeaee58",
               "action" : "none"
            }
        } 
    ]
}
```
 

### [Volver a la referencia de la API de REST](http://tve.helpdocsonline.com/rest-api-reference)
