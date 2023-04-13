---
title: Iniciar autorización
description: Iniciar autorización
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Iniciar autorización {#initiate-authorization}

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

Obtiene la respuesta de autorización. 

| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authorization | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. solicitante (obligatorio)</br>2.  deviceId (obligatorio)</br>3.  recurso (obligatorio)</br>4.  device_info/X-Device-Info (obligatorio)</br>5.  _deviceType_</br> 6.  _deviceUser_ (obsoleto)</br>7.  _appId_ (obsoleto)</br>8.  parámetros adicionales (opcional) | GET | XML o JSON que contienen detalles de autorización o detalles de error si no se realiza correctamente. Consulte los ejemplos siguientes. | 200 - Éxito  </br>403 - Sin éxito |

{style="table-layout:auto"}

</br>


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| recurso | Una cadena que contiene un resourceId (o fragmento MRSS), identifica el contenido solicitado por un usuario y es reconocida por los extremos de autorización de MVPD. |
| device_info/</br></br>X-Device-Info | Información del dispositivo de transmisión.</br></br>**Nota**: Esto PUEDE pasarse device_info como parámetro de URL, pero debido al tamaño potencial de este parámetro y a las limitaciones en la longitud de una URL de GET, DEBE pasarse como X-Device-Info en el encabezado http. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | El tipo de dispositivo (por ejemplo, Roku, PC).</br></br>Si este parámetro está configurado correctamente, ESM ofrece métricas que [desglosado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) al usar Clientless, de modo que se puedan realizar diferentes tipos de análisis para, por ejemplo, Roku, Apple TV, Xbox, etc.</br></br>Consulte [Ventajas del parámetro de tipo de dispositivo sin cliente en las métricas de pase ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Nota**: device_info reemplazará este parámetro. |
| _deviceUser_ | El identificador de usuario del dispositivo. |
| _appId_ | El id/nombre de la aplicación. </br></br>**Nota**: device_info reemplaza este parámetro. |
| parámetros adicionales | La llamada también puede contener parámetros opcionales que habilitan otras funcionalidades como:</br></br>* generic_data - habilita el uso de [Paso temporal promocional](/help/authentication/promotional-temp-pass.md)</br></br>Ejemplo: `generic_data=("email":"email@domain.com")` |

{style="table-layout:auto"}

>[!CAUTION]
>
>**Dirección IP del dispositivo de transmisión**</br>
>En implementaciones de cliente a servidor, la dirección IP del dispositivo de transmisión se envía implícitamente con esta llamada.  Para implementaciones de servidor a servidor, donde la variable **regcode** es realizada por el servicio de programación y no por el dispositivo de transmisión, se requiere el siguiente encabezado para pasar la dirección IP del dispositivo de transmisión:</br></br>
>
>
```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>donde `<streaming\_device\_ip>` es la dirección IP pública del dispositivo de transmisión.</br></br>
>Ejemplo :</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```


### Respuesta de ejemplo {#sample-response}

* **Caso 1: Correcto**

</br>
  * **XML:**
  </br>
    ```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
    <expires>1348148289000</expires>
    <mvpd>sampleMvpdId</mvpd>
    <requestor>sampleRequestorId</requestor>
    <resource>sampleResourceId</resource>
    </authorization>
    ```



* **JSON:**

   ```JSON
   {
     "mvpd": "sampleMvpdId",
     "resource": "sampleResourceId",
     "requestor": "sampleRequestorId",
     "expires": "1348148289000"
   }
   ```

>[!IMPORTANT]
>
>Cuando la respuesta proviene de un MVPD de proxy, puede incluir un elemento adicional denominado `proxyMvpd`. 

 

* **Caso 2: Autorización denegada**


   ```JSON
   <error>
     <status>403</status>
     <message>User not authorized</message>
     <details>Your subscription package does not include the "ASFAFD" channel.
     Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
   </error>
   ```

