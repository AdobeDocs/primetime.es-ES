---
title: 'Implementación de API sin cliente: códigos de error/mensajes con motivo probable/causa'
description: 'Implementación de API sin cliente: códigos de error/mensajes con motivo probable/causa'
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Implementación de API sin cliente: códigos de error/mensajes con motivo probable/causa {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>


## Error: No autorizado

### Causas:

1. Falta el encabezado de autorización en el POST
1. Problema con el encabezado de autorización: compruebe si el tiempo de solicitud está en milisegundos.

## Error: SC 400 durante la autenticación

### Causas:

1. El servidor no encontró el código de registro, que se creó para un solicitante y un entorno específicos.
1. Puede encontrarse con problemas de scripts entre dominios
1. Se debe agregar la suplantación adecuada al archivo /etc/hosts

## Error: 400 Solicitud incorrecta

### Causas:

1. URL mal formada para POST/GET
1. SAMLAssertionParserException - La afirmación de SAML cifrada no se pudo descifrar al final del Adobe

## Error: 403 prohibido

### Causas:

1. Demasiadas solicitudes rápidas, una función de la administración de API para evitar ataques de DoS.
2. Si utiliza un entorno de preequilibrio, agregue la simulación, de lo contrario, asegúrese de que la simulación se haya eliminado del archivo /etc/hosts

## Error: No se puede iniciar sesión en la página MVPD

### Causas:

1. El nombre de usuario y la contraseña no coinciden 
2. Es posible que el inicio de sesión esté desactivado
3. Compruebe si el inicio de sesión es para producción o ensayo


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->