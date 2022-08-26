---
title: Recuperar lista de recursos preautorizados
description: Recuperar lista de recursos preautorizados
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# Recuperar lista de recursos preautorizados {#retrieve-list-of-preauthorized-resources}

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

Existen dos conjuntos de API: un conjunto para la aplicación de flujo continuo o el servicio de programación y otro para la aplicación web de segunda pantalla. En esta página se describe la API para la aplicación de flujo continuo o el servicio de programación.


| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/preauthorization | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. solicitante (obligatorio)</br>2.  deviceId (obligatorio)</br>3.  lista de recursos (obligatorio)</br>4.  device_info/X-Device-Info (obligatorio)</br>5.  _deviceType_</br> 6.  _deviceUser_ (obsoleto)</br>7.  _appId_ (obsoleto) | GET | XML o JSON que contienen decisiones individuales de preautorización o detalles de error. Consulte los ejemplos siguientes. | 200 - Éxito</br></br>400 - Solicitud incorrecta</br></br>401 - No autorizado</br></br>405 - Método no permitido  </br></br>412 - Error en la precondición</br></br>500 - Error interno del servidor |


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| lista de recursos | Cadena que contiene una lista delimitada por comas de resourceIds que identifica el contenido al que podría acceder un usuario y que es reconocido por los puntos finales de autorización de MVPD. |
| device_info/</br></br>X-Device-Info | Información del dispositivo de transmisión.</br></br>**Nota**: Esto PUEDE pasarse device_info como parámetro de URL, pero debido al tamaño potencial de este parámetro y a las limitaciones en la longitud de una URL de GET, DEBE pasarse como X-Device-Info en el encabezado http. </br></br>Consulte los detalles completos en [Pasar información de dispositivo y conexión](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | El tipo de dispositivo (por ejemplo, Roku, PC).</br></br>Si este parámetro está configurado correctamente, ESM ofrece métricas que [desglosado por tipo de dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) al usar Clientless, de modo que se puedan realizar diferentes tipos de análisis para, por ejemplo, Roku, Apple TV, Xbox, etc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**Nota**: device_info reemplazará este parámetro. |
| _deviceUser_ | El identificador de usuario del dispositivo. |
| _appId_ | El id/nombre de la aplicación. </br></br>**Nota**: device_info reemplaza este parámetro. |



### Respuesta de ejemplo {#sample-response}

 

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
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
  </resource>
</resources>
```
 
</br>

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
