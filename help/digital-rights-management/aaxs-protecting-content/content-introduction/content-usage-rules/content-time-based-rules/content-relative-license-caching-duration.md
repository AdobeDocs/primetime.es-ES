---
title: Duración del almacenamiento en caché de licencias
description: Duración del almacenamiento en caché de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Duración del almacenamiento en caché de licencias{#license-caching-duration}

Especifica la duración durante la que una licencia se puede almacenar en caché en disco en el almacén de licencias local del cliente sin necesidad de volver a adquirirse desde el servidor de licencias. También puede especificar una fecha y hora absolutas después de la cual una licencia ya no se puede almacenar en caché.

Una vez que ha pasado la fecha de caducidad de la caché, la licencia ya no es válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: Utilice la duración de la caché de licencias para especificar una cantidad fija de tiempo válido para una licencia en particular, como en un caso de uso de alquiler. Se puede especificar un alquiler de 30 días (con caché de licencia) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.
