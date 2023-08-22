---
title: Comprobar flujo de autenticación por aplicación web en segunda pantalla
description: Comprobar flujo de autenticación por aplicación web en segunda pantalla
exl-id: 5807f372-a520-4069-b837-67ae41b7f79b
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Comprobar flujo de autenticación por aplicación web en segunda pantalla {#check-authentication-flow-by-second-screen-web-app}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Extremos de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descripción {#description}

Esta API debe ser consumida por la aplicación web de inicio de sesión en la segunda pantalla para confirmar que la autenticación de Adobe Primetime ha reconocido que el inicio de sesión se ha realizado correctamente desde MVPD. Se recomienda llamar a esta API antes de mostrar un mensaje de éxito al usuario final que le indique que continúe con los flujos de trabajo en la consola del dispositivo.


| Extremo | Llamado  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{código de registro} | Iniciar sesión en aplicación web | 1. código de registro  </br>    (Componente Ruta)</br>2.  solicitante  </br>    (Obligatorio) | GET | XML o JSON con detalles de error si no se ha realizado correctamente. | 200 - Éxito   </br>403 - Prohibido |

</br>

| Parámetro de entrada | Descripción |
| ----------------- | --------------------------------------------------------------------------------------------- |
| código de registro | El valor del código de registro proporcionado por el usuario al principio del flujo de autenticación. |
| solicitante | Identificador de solicitante del programador para el que es válida esta operación. |


### Respuesta de ejemplo (en caso de error) {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [Volver a la referencia de la API de REST](/help/authentication/rest-api-reference.md)
