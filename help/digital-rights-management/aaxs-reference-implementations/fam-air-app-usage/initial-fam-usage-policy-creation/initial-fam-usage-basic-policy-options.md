---
title: Opciones de directiva básicas
description: Opciones de directiva básicas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Opciones de directiva básicas {#basic-policy-options}

En la tabla siguiente se describen las preferencias de la directiva básica:

| Preferencia | Descripción |
|---|---|
| Duración de directiva | Especifica el período de validez del contenido protegido con esta directiva. |
|  | Comenzar en | Las licencias no pueden utilizarse hasta esta fecha/hora. |
|  | Finalizar en | Las licencias no se pueden usar después de esta fecha/hora. |
|  | Finalizar después de | Especifica la cantidad de tiempo que una licencia es válida (en minutos), a partir del momento en que se empaqueta. |
| Almacenamiento en caché de licencias | Especifica si el cliente puede almacenar en caché las licencias. |
|  | | Las licencias no se pueden usar después de esta fecha/hora. |
|  | Eliminar después de | Especifica la cantidad de tiempo que una licencia es válida (en minutos), a partir del momento en que el servidor de licencias emite la licencia. |
|  | Caché indefinida | La licencia se puede almacenar en caché en el cliente indefinidamente. |
|  | Sin almacenamiento en caché de licencias | El cliente no puede almacenar la licencia en caché. Se debe obtener una nueva licencia del servidor cada vez que el usuario reproduce el contenido. |
| Autenticación | |
|  | Anónimo | No se requiere autenticación para ver el contenido. |
|  | Autenticado | Se requiere autenticación de nombre de usuario y contraseña. |
| Habilitar encadenamiento de licencias | Permite actualizar una licencia mediante una licencia raíz principal para la actualización por lotes de licencias. Una vez que caduca la licencia hoja, el servidor puede emitir al cliente una licencia raíz, que renovará todo el contenido protegido con esta directiva. |
