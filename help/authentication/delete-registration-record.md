---
title: Eliminar registro
description: Eliminar registro
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Eliminar registro {#delete-registration-record}

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


## Descripción {#delete-record}

Elimina el registro de código reg y libera el código reg para su reutilización. 

| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>Por ejemplo:</br></br>&lt;reggie_fqdn>/reggie/v1/regcode/ER45RTY | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. ID del solicitante  </br>    (Componente Ruta)</br>2.  Código de registro  </br>    (Componente Ruta) | DELETE | Ninguna | 204 |

{style="table-layout:auto"}

</br>

| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| código de registro | El valor del código de registro que se mostraría en el dispositivo de transmisión (que se introduciría en el flujo de autenticación). |

{style="table-layout:auto"}

</br>

### [Volver a la referencia de la API de REST](/help/authentication/rest-api-reference.md)
