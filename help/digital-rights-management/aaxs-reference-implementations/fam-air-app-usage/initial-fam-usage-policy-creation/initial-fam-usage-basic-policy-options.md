---
title: Opciones de directiva básicas
description: Opciones de directiva básicas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Opciones de directiva básicas {#basic-policy-options}

En la tabla siguiente se describen las preferencias de Política básica:

| Preferencia | Descripción |
|---|---|
| Duración de la política | Especifica el periodo de validez del contenido protegido con esta directiva. |
|  | Iniciar en | Las licencias no se pueden usar hasta esta fecha/hora. |
|  | Finalizar en | Las licencias no se pueden usar después de esta fecha/hora. |
|  | Finalizar después de | Especifica la cantidad de tiempo que una licencia es válida (en minutos), a partir del momento en que se empaqueta. |
| Almacenamiento en caché de licencias | Especifica si el cliente puede almacenar en caché las licencias. |
|  |  | Las licencias no se pueden usar después de esta fecha/hora. |
|  | Eliminar después de | Especifica la cantidad de tiempo que una licencia es válida (en minutos), a partir del momento en que el servidor de licencias emite la licencia. |
|  | Caché indefinida | La licencia se puede almacenar en caché en el cliente indefinidamente. |
|  | Sin almacenamiento en caché de licencias | El cliente no puede almacenar en caché la licencia. Se debe obtener una licencia nueva del servidor cada vez que el usuario reproduce el contenido. |
| Autenticación |  |
|  | Anonymous | No se requiere autenticación para ver el contenido. |
|  | Autenticado | Se requiere autenticación de nombre de usuario/contraseña. |
| Habilitar encadenado de licencias | Permite actualizar una licencia utilizando una licencia raíz principal para la actualización por lotes de licencias. Una vez que la licencia de hoja caduca, el servidor puede emitir al cliente una licencia de raíz, que renovará todo el contenido protegido con esta directiva. |

