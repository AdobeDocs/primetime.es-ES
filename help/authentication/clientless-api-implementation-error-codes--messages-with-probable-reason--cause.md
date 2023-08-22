---
title: 'Implementación de API sin cliente: códigos de Error y mensajes con la razón y causa probables'
description: 'Implementación de API sin cliente: códigos de Error y mensajes con la razón y causa probables'
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Implementación de API sin cliente: códigos de Error y mensajes con la razón y causa probables {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>La contenido en esta Página se ofrece únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe Systems. No se permite el uso no autorizado.

</br>


## Error: no autorizado

### Causas:

1. Falta el encabezado de autorización en el POST
1. Problema con el encabezado de autorización: Compruebe si solicitud tiempo está en milisegundos.

## Error: SC 400 durante la autenticación

### Causas:

1. El servidor no encontró el código de registro, que se creó para un solicitante específico y entorno.
1. Podría estar ejecutando problemas de script entre dominios
1. Se debe añadir una imitación adecuada al archivo/etc/hosts

## Error: 400 solicitud errónea

### Causas:

1. URL con formato incorrecto para POST/GET
1. SAMLAssertionParserException: no se pudo descifrar la aserción SAML cifrada al final de Adobe Systems

## Error: 403 prohibido

### Causas:

1. Demasiadas solicitudes rápidas: una característica de la administración de API para evitar ataques DoS.
2. Si utiliza prequal entorno, a continuación, agregue la suplantación, asegúrese de que la imitación se haya eliminado del archivo/etc/hosts

## Error: no se puede iniciar sesión en MVPD Página

### Causas:

1. Nombre de usuario y contraseña no coinciden
2. Es posible que el inicio de sesión esté desactivado
3. Compruebe si el inicio de sesión es para producción o ensayo


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
