---
title: Vista previa gratuita para pase temporal y pase temporal promocional
description: Vista previa gratuita para pase temporal y pase temporal promocional
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# Vista previa gratuita para pase temporal y pase temporal promocional {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

Permite la creación de un token de autenticación para Temp Pass y Promotional Temp Pass sin necesidad de una segunda pantalla.


| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authentication/freepreview | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. requestor_id (obligatorio)</br>    </br>2.  deviceId (obligatorio)</br>    </br>3.  mso_id (obligatorio)</br>    </br>4.  domain_name (obligatorio)</br>    </br>5.  device_info/X-Device-Info (obligatorio)</br>6.  deviceType</br>    </br>7.  deviceUser (desaprobada)</br>    </br>8.  appId (obsoleto)</br>    </br>9.  generic_data (opcional) | POST | La respuesta correcta será 204 Sin contenido, indicando que el token se creó correctamente y está listo para utilizarse para los flujos de autenticación. | 204 - Sin contenido   </br>400 - Solicitud incorrecta |

<div>


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor_id | El RequestorId del programador para el que esta operación es válida. |
| deviceId | Los bytes de identificación del dispositivo. |
| mso_id | El Id. de MVPD para el que es válida esta operación. |
| domain_name | El nombre de dominio para el que se otorgará un token. Esto se compara con los dominios del proveedor de servicios cuando se concede un token de autorización. |
| device_info/</br></br>X-Device-Info | Información del dispositivo de transmisión.</br></br>**Nota**: Esto PUEDE pasarse device_info como parámetro de URL, pero debido al tamaño potencial de este parámetro y a las limitaciones en la longitud de una URL de GET, DEBE pasarse como X-Device-Info en el encabezado http. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | El tipo de dispositivo (por ejemplo, Roku, PC).</br></br>Si este parámetro está configurado correctamente, ESM ofrece métricas que [desglosado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) al usar Clientless, de modo que se puedan realizar diferentes tipos de análisis para, por ejemplo, Roku, Apple TV, Xbox, etc.</br></br>Consulte [Ventajas del uso de parámetros de tipo de dispositivo sin cliente ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Nota**: device_info reemplazará este parámetro. |
| _deviceUser_ | El identificador de usuario del dispositivo.</br></br>**Nota**: Si se utiliza, deviceUser debe tener los mismos valores que en la variable [Crear código de registro](/help/authentication/registration-code-request.md) solicitud. |
| _appId_ | El id/nombre de la aplicación. </br></br>**Nota**: device_info reemplaza este parámetro. Si se usa, `appId` debe tener los mismos valores que en la variable [Crear código de registro](/help/authentication/registration-code-request.md) solicitud. |
| generic_data | Se utiliza para limitar el alcance del token para el pase temporal promocional. |


### [Volver a la referencia de la API de REST](/help/authentication/rest-api-reference.md)
