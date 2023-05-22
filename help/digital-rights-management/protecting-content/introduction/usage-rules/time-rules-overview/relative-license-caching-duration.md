---
title: Duración de almacenamiento en caché de licencias
description: Duración de almacenamiento en caché de licencias
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Duración de almacenamiento en caché de licencias{#license-caching-duration}

La duración del almacenamiento en caché de licencias especifica cuánto tiempo se puede almacenar una licencia en caché en el disco en el almacén de licencias local del cliente sin que sea necesario volver a obtenerla del servidor de licencias. También puede especificar una fecha y hora absolutas después de las cuales una licencia ya no se puede almacenar en caché.

Una vez transcurrida la fecha de caducidad de la caché, la licencia deja de ser válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: utilice la duración del almacenamiento en caché de la licencia para especificar una cantidad fija de tiempo válido para una licencia determinada, como en un caso de uso de alquiler. Puede especificar un alquiler de 30 días (con almacenamiento en caché de licencias) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.
