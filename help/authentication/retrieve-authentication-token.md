---
title: Recuperar token de autenticación
description: Recuperar token de autenticación
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Recuperar token de autenticación {#retrieve-authentication-token}

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

Recupera el token de autenticación (AuthN).  

| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn</br></br>Por ejemplo:</br></br>&lt;sp_fqdn>/api/v1/tokens/authn | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. solicitante (obligatorio)</br>2.  deviceId (obligatorio)</br>3.  device_info/X-Device-Info (obligatorio)</br>4.  _deviceType_ (obsoleto)</br>5.  _deviceUser_ (obsoleto)</br>6.  _appId_ (obsoleto) | GET | XML o JSON que contienen información de autenticación o detalles de error si no se realiza correctamente. | 200 - Éxito.  </br>404 - Token no encontrado  </br>410 - Token caducado |

{style=&quot;table-layout:auto&quot;}


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| device_info/</br></br>X-Device-Info | Información del dispositivo de transmisión.</br></br>**Nota**: Esto PUEDE pasarse device_info como parámetro de URL, pero debido al tamaño potencial de este parámetro y a las limitaciones en la longitud de una URL de GET, DEBE pasarse como X-Device-Info en el encabezado http. </br></br>Consulte los detalles completos en [Pasar información de dispositivo y conexión](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | El tipo de dispositivo (por ejemplo, Roku, PC).</br></br>**Nota**: device_info reemplaza este parámetro. |
| _deviceUser_ | El identificador de usuario del dispositivo.</br></br>**Nota**: Si se utiliza, deviceUser debe tener los mismos valores que en la variable [Crear código de registro](http://tve.helpdocsonline.com/registration-code-request) solicitud. |
| _appId_ | El id/nombre de la aplicación. </br></br>**Nota**: device_info reemplaza este parámetro. Si se usa, `appId` debe tener los mismos valores que en la variable [Crear código de registro](http://tve.helpdocsonline.com/registration-code-request) solicitud. |

{style=&quot;table-layout:auto&quot;}

</br>

### Respuesta de ejemplo {#response}

 

#### Correcto

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authentication>
         <expires>1601114932000</expires>
         <userId>sampleUserId</userId>
         <mvpd>sampleMvpdId</mvpd>
         <requestor>sampleRequestor</requestor>
    </authentication>
```


**JSON:**

```JSON
    {
         "requestor": "sampleRequestor",
         "mvpd": "sampleMvpdId",
         "userId": "sampleUserId",
         "expires": "1601114932000"
    }
```

 

 

#### No se encontró el token de autenticación:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>404</status>
        <message>Not found</message>
    </error>
```

 
**JSON:**

```JSON
    {
        "status": 404,
        "message": "Not Found"
    }
```

[Volver a la referencia de API sin cliente](http://tve.helpdocsonline.com/clientless-api-reference)
