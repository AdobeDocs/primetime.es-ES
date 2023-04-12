---
title: Flujo de API sin cliente en ausencia de ID de dispositivo
description: Flujo de API sin cliente en ausencia de ID de dispositivo
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Flujo de API sin cliente en ausencia de ID de dispositivo {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>


## Problema

No todas las aplicaciones de dispositivos inteligentes podrán proporcionar un ID de dispositivo único.  Como deviceId es un parámetro obligatorio, el servicio devuelve un error 400 si no se pasa.


## Solución temporal/solución alternativa

Para clientes sin ID de dispositivo:

1. Llame al servicio de códigos de registro por primera vez con `deviceId=dummy`
1. De la respuesta, extraiga el UUID. El UUID está disponible en el elemento &quot;id&quot; de la respuesta del código de registro (formatos de respuesta XML y JSON).
1. Llame al servicio de registro por segunda vez. Esta vez, pase `deviceId=<uuid obtained in step #2>`
1. Mostrar el código de registro obtenido en el paso 3 de la interfaz de usuario de la consola


Una vez realizados estos pasos, la autenticación de Adobe Primetime utilizará el UUID como ID de dispositivo. Almacene este ID de dispositivo (UUID) en el almacenamiento local del dispositivo. En el caso de que el usuario genere un nuevo código de registro, debe volver a ejecutar los pasos del 1 al 4 y, a continuación, reemplazar el ID del dispositivo (UUID) almacenado anteriormente por el nuevo.



## Solución permanente

Adobe lo cambiará en una versión futura, realizando `deviceId` una carga útil opcional al crear el código reg y utilizar UUID como clave de token en lugar de `deviceId`, cuando `deviceId` no está presente.

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->