---
title: Comprobar token de autenticación
description: Comprobar token de autenticación
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Comprobar token de autenticación {#check-authentication-token}

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

Indica si el dispositivo tiene un token de autenticación no caducado.

| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/checkauthn | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. solicitante (obligatorio)</br>2.  deviceId (obligatorio)</br>3.  device_info/X-Device-Info (obligatorio)</br>4.  _deviceType_ </br>5.  _deviceUser_ (obsoleto)</br>6.  _appId_ (obsoleto) | GET | XML o JSON que contienen detalles de error si no se realiza correctamente. | 200 - Éxito   </br>403 - Sin éxito |

{style=&quot;table-layout:auto&quot;}


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| device_info/</br></br>X-Device-Info | Información del dispositivo de transmisión.</br></br>**Nota**: Esto PUEDE pasarse device_info como parámetro de URL, pero debido al tamaño potencial de este parámetro y a las limitaciones en la longitud de una URL de GET, DEBE pasarse como X-Device-Info en el encabezado http. </br></br>Consulte los detalles completos en [Pasar información de dispositivo y conexión](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | El tipo de dispositivo (por ejemplo, Roku, PC).</br></br>Si este parámetro está configurado correctamente, ESM ofrece métricas que [desglosado por tipo de dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) al usar Clientless, de modo que se puedan realizar diferentes tipos de análisis para, por ejemplo, Roku, Apple TV, Xbox, etc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**Nota**: device_info reemplazará este parámetro. |
| _deviceUser_ | El identificador de usuario del dispositivo. |
| _appId_ | El id/nombre de la aplicación.</br>**Nota**: device_info reemplaza este parámetro. |

{style=&quot;table-layout:auto&quot;}


## Respuesta (si no se ha realizado correctamente) {#response}

```JSON
    <error>
      <status>403</status>
      <message>Authentication token expired</message>
    </error>
```

### [Volver a la referencia de la API de REST](http://tve.helpdocsonline.com/rest-api-reference)
