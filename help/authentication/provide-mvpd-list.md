---
title: Proporcionar lista MVPD
description: Proporcionar lista MVPD
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Proporcionar lista MVPD {#provide-mvpd-list}

## Puntos finales de API de REST {#clientless-endpoints}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## Descripción {#description}

Devuelve la lista de MVPD configurados para el solicitante.

| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestorId}</br></br>Por ejemplo:</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | Autenticación de Primetime | 1. Solicitante</br>    (Componente Ruta)</br>_2.  deviceType (desaprobada)_ | GET | XML o JSON que contienen una lista de MVPD. | 200 |

{style=&quot;table-layout:auto&quot;}


| Parámetro de entrada | Descripción |
| --------------- | ------------------------------------------------------------- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| *deviceType* | Tipo de dispositivo. |

{style=&quot;table-layout:auto&quot;}

### Respuesta de ejemplo {#sample-response}

Igual que la respuesta XML MVPD existente al servlet /config

Nota: Todos los MVPD configurados para utilizar el SSO de plataforma tendrán las siguientes propiedades adicionales dentro de su nodo correspondiente (JSON/XML):

* **enablePlatformServices (booleano):** indicador que indica si este MVPD se integra mediante Platform SSO
* **boardingStatus (cadena):** Indicador que indica si el MVPD es totalmente compatible con el SSO de plataforma (compatible) o si el MVPD solo aparece en el selector de plataformas (PICKER)
* **displayInPlatformPicker (booleano):** si este MVPD aparece en el selector de plataformas
* **platformMappingId (cadena):** el identificador de este MVPD conocido por la plataforma
* **requiredMetadataFields (matriz de cadenas):** los campos de metadatos de usuario que se espera que estén disponibles en un inicio de sesión exitoso


[Volver a la referencia de API sin cliente](http://tve.helpdocsonline.com/clientless-api-reference)
