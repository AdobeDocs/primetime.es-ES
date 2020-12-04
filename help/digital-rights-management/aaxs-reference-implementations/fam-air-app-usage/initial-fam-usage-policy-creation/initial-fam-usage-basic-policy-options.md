---
seo-title: Opciones de directiva básicas
title: Opciones de directiva básicas
uuid: b09543b6-26a7-4e4d-8e8f-866b4bf9cc50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Opciones de directiva básicas {#basic-policy-options}

En la tabla siguiente se describen las preferencias de Política básica:

| Preferencia | Descripción |
|---|---|
| Duración de la directiva | Especifica el período de validez del contenido protegido con esta directiva. |
|  | Inicio en | Las licencias no se pueden usar hasta esta fecha y hora. |
|  | Finalizar en | Las licencias no se pueden usar después de esta fecha/hora. |
|  | Finalizar después de | Especifica la cantidad de tiempo que una licencia es válida (en minutos), a partir del momento en que se empaqueta. |
| Almacenamiento en caché de licencias | Especifica si el cliente puede almacenar en caché las licencias. |
|  |  | Las licencias no se pueden usar después de esta fecha/hora. |
|  | Eliminar después de | Especifica la cantidad de tiempo que una licencia es válida (en minutos), a partir del momento en que el servidor de licencias emite la licencia. |
|  | Caché indefinida | La licencia se puede almacenar en caché en el cliente indefinidamente. |
|  | Sin almacenamiento en caché de licencias | El cliente no puede almacenar en caché la licencia. Se debe obtener una nueva licencia del servidor cada vez que el usuario reproduce el contenido. |
| Autenticación |  |
|  | Anónimo | No se requiere autenticación para la vista del contenido. |
|  | Autenticado | Se requiere autenticación de nombre de usuario y contraseña. |
| Habilitar el encadenado de licencias | Permite actualizar una licencia mediante una licencia raíz principal para la actualización por lotes de licencias. Una vez caducada la licencia de hoja, el servidor puede emitir al cliente una licencia de raíz, que renovará todo el contenido protegido con esta directiva. |

