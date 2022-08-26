---
title: Metadatos de usuario
description: Metadatos de usuario
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Metadatos de usuario {#user-metadata}

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

Recupere metadatos que MVPD compartió sobre el usuario autenticado.

<div>


| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/usermetadata | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. requestor</br>2.  deviceId (obligatorio)</br>3.  device_info/X-Device-Info (obligatorio)</br>4.  deviceType</br>5.  deviceUser (desaprobada)</br>6.  appId (obsoleto) | GET | XML o JSON que contienen metadatos de usuario o detalles de error si no se realiza correctamente. | 200 - Éxito</br></br>404 - No se encontraron metadatos</br></br>412 - Token AuthN no válido (por ejemplo, token caducado) |


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| device_info/</br></br>X-Device-Info | Información del dispositivo de transmisión.</br></br>**Nota**: Esto PUEDE pasarse device_info como parámetro de URL, pero debido al tamaño potencial de este parámetro y a las limitaciones en la longitud de una URL de GET, DEBE pasarse como X-Device-Info en el encabezado http. </br></br>Consulte los detalles completos en [Pasar información de dispositivo y conexión](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | El tipo de dispositivo (por ejemplo, Roku, PC).</br></br>Si este parámetro está configurado correctamente, ESM ofrece métricas que [desglosado por tipo de dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) al usar Clientless, de modo que se puedan realizar diferentes tipos de análisis para, por ejemplo, Roku, Apple TV, Xbox, etc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**Nota**: device_info reemplazará este parámetro. |
| _deviceUser_ | El identificador de usuario del dispositivo.</br></br>**Nota**: Si se utiliza, deviceUser debe tener los mismos valores que en la variable [Crear código de registro](http://tve.helpdocsonline.com/registration-code-request) solicitud. |
| _appId_ | El id/nombre de la aplicación. </br></br>**Nota**: device_info reemplaza este parámetro. Si se usa, `appId` debe tener los mismos valores que en la variable [Crear código de registro](http://tve.helpdocsonline.com/create-registration-page-/-login-uri) solicitud. |

>[!NOTE]
> 
>La información de metadatos del usuario debe estar disponible una vez finalizado el flujo de autenticación, pero puede actualizarse en el flujo de autorización, según el MVPD y el tipo de metadatos.

</br>

## Respuesta de ejemplo {#sample-response}

Después de una llamada correcta, el servidor responderá con un objeto XML (predeterminado) o JSON con una estructura similar a la que se muestra a continuación:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
              },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
    }
```

 

En la raíz del objeto habrá tres nodos:

* *actualizado*: especifica una marca de tiempo UNIX que representa la última vez que se actualizaron los metadatos. Esta propiedad la establecerá inicialmente el servidor al generar los metadatos durante la fase de autenticación. Las llamadas posteriores (una vez actualizados los metadatos) resultarán en un aumento de la marca de tiempo.

* *data*: contiene los valores de metadatos reales. 

* *cifrados*: una matriz que enumera las propiedades cifradas. Para descifrar un valor de metadatos específico, el programador debe realizar un decodificador Base64 en los metadatos y, a continuación, aplicar un descifrado RSA en el valor resultante, utilizando su propia clave privada (el Adobe cifra los metadatos en el servidor utilizando el certificado público del programador).

En caso de error, el servidor devolverá un objeto XML o JSON que especifica un mensaje de error detallado.

**Más información:** [Metadatos de usuario](http://tve.helpdocsonline.com/user-metadata-v2)


### [Volver a la referencia de la API de REST](http://tve.helpdocsonline.com/rest-api-reference)
