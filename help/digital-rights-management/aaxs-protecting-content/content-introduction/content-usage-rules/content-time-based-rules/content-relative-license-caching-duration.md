---
seo-title: Duración del almacenamiento en caché de licencias
title: Duración del almacenamiento en caché de licencias
uuid: 378940a2-f072-478d-bee1-05ccba888b5c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Duración del almacenamiento en caché de licencias{#license-caching-duration}

Especifica la duración durante la que una licencia se puede almacenar en caché en disco en el almacén de licencias local del cliente sin necesidad de volver a adquirirla en el servidor de licencias. También puede especificar una fecha y hora absolutas después de la cual una licencia ya no se puede almacenar en caché.

Una vez pasada la fecha de caducidad de la caché, la licencia ya no es válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: Utilice la duración de la caché de licencia para especificar una cantidad fija de tiempo válida para una licencia determinada, como en un caso de uso de alquiler. Se puede especificar un alquiler de 30 días (con caché de licencia) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.
