---
title: Comprobar el flujo de autenticación por aplicación web de segunda pantalla
description: Comprobar el flujo de autenticación por aplicación web de segunda pantalla
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Comprobar el flujo de autenticación por aplicación web de segunda pantalla {#check-authentication-flow-by-second-screen-web-app}

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

Esta API debe ser consumida por la segunda aplicación web de inicio de sesión en pantalla para confirmar que la autenticación de Adobe Primetime ha reconocido el inicio de sesión correcto desde MVPD. Recomendamos llamar a esta API antes de mostrar un mensaje de éxito al usuario final que le indique que vaya a la consola del dispositivo para continuar con los flujos de trabajo.


| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{código de registro} | Aplicación web de inicio de sesión | 1. código de registro  </br>    (Componente Ruta)</br>2.  requestor  </br>    (Obligatorio) | GET | XML o JSON que contienen detalles de error si no se realiza correctamente. | 200 - Éxito   </br>403 - Prohibido |

</br>

| Parámetro de entrada | Descripción |
| ----------------- | --------------------------------------------------------------------------------------------- |
| código de registro | El valor del código de registro proporcionado por el usuario al principio del flujo de autenticación. |
| requestor | El RequestorId del programador para el que esta operación es válida. |


### Respuesta de ejemplo (en caso de error) {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [Volver a la referencia de la API de REST](/help/authentication/rest-api-reference.md)
