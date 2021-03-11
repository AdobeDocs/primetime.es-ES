---
title: Duración del almacenamiento en caché de licencias
description: Duración del almacenamiento en caché de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Duración del almacenamiento en caché de licencias{#license-caching-duration}

La duración del almacenamiento en caché de licencias especifica cuánto tiempo se puede almacenar una licencia en caché en disco en el almacén de licencias local del cliente sin necesidad de volver a adquirirla desde el servidor de licencias. Como alternativa, puede especificar una fecha y hora absolutas después de las cuales una licencia ya no se puede almacenar en caché.

Una vez que ha pasado la fecha de caducidad de la caché, la licencia ya no es válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: Utilice la duración de la caché de licencias para especificar una cantidad fija de tiempo válido para una licencia en particular, como en un caso de uso de alquiler. Puede especificar un alquiler de 30 días (con caché de licencia) para indicar la duración total de la licencia dentro de la cual consumir el contenido.
