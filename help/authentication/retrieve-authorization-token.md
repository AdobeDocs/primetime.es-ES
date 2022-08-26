---
title: Recuperar token de autorización
description: Recuperar token de autorización
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Recuperar token de autorización {#retrieve-authorization-token}

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

Recupera el token de autorización (AuthZ).  


| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authz</br></br>Por ejemplo:</br></br>&lt;sp_fqdn>/api/v1/tokens/authz | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. solicitante (obligatorio)</br>2.  deviceId (obligatorio)</br>3.  recurso (obligatorio)</br>4.  device_info/X-Device-Info (obligatorio)</br>5.  _deviceType_</br> 6.  _deviceUser_ (obsoleto)</br>7.  _appId_ (obsoleto) | GET | 1. Éxito</br>2.  Token de autenticación  </br>    no encontrado o caducado:   </br>    Motivo de explicación de XML  </br>    no se encontró el token de autenticación</br>3.  Token de autorización  </br>    no encontrado:  </br>    Explicación XML</br>4.  Token de autorización  </br>    caducado:  </br>    Explicación XML | 200 - Éxito  </br>412 - No AuthN</br></br>404 - Sin AuthZ</br></br>410 - AuthZ caducado |

{style=&quot;table-layout:auto&quot;}

</br>

| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| recurso | Una cadena que contiene un resourceId (o fragmento MRSS), identifica el contenido solicitado por un usuario y es reconocida por los extremos de autorización de MVPD. |
| device_info/</br></br>X-Device-Info | Información del dispositivo de transmisión.</br></br>**Nota**: Esto PUEDE pasarse device_info como parámetro de URL, pero debido al tamaño potencial de este parámetro y a las limitaciones en la longitud de una URL de GET, DEBE pasarse como X-Device-Info en el encabezado http. </br></br>Consulte los detalles completos en [Pasar información de dispositivo y conexión](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | El tipo de dispositivo (por ejemplo, Roku, PC).</br></br>Si este parámetro está configurado correctamente, ESM ofrece métricas que [desglosado por tipo de dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) al usar Clientless, de modo que se puedan realizar diferentes tipos de análisis para, por ejemplo, Roku, Apple TV, Xbox, etc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**Nota**: device_info reemplazará este parámetro. |
| _deviceUser_ | El identificador de usuario del dispositivo. |
| _appId_ | El id/nombre de la aplicación. </br></br>**Nota**: device_info reemplaza este parámetro. |

{style=&quot;table-layout:auto&quot;}


### Respuesta de ejemplo {#response}

 

#### Correcto

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
        <expires>1348148289000</expires>
        <mvpd>sampleMvpdId</mvpd>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <proxyMvpd>sampleProxyMvpdId</proxyMvpd>
    </authorization>
```

 

**JSON:**

```JSON
    {
        "mvpd": "sampleMvpdId",
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348148289000",
        "proxyMvpd": "sampleProxyMvpdId"
    }
```

 </br>


#### Token de autenticación no encontrado o caducado:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>412</status>
        <message>User not authenticated</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 412,
        "message": "User not authenticated",
        "details": null
    }
```

</br>
 

#### No se encontró el token de autorización:

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
        "message": "Not Found",
        "details": null
    }
```

</br>

 

#### Token de autorización expirado:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>410</status>
        <message>Gone</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 410,
        "message": "Gone",
        "details": null
    }
```

[Volver a la referencia de API sin cliente](http://tve.helpdocsonline.com/clientless-api-reference)
