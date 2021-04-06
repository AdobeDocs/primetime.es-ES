---
title: Transcodificación Just-in-Time
description: Transcodificación Just-in-Time
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Transcodificación Just-in-Time {#just-in-time-transcoding}

El Ad Insertion Primetime incluye transcodificación y empaquetado justo a tiempo para garantizar que los elementos creativos de publicidad incompatibles se puedan reproducir correctamente en los flujos de contenido. También puede insertar paquetes ID3 en fragmentos de anuncios que se puedan utilizar en el seguimiento de anuncios del lado del cliente.
Un flujo de trabajo típico es el siguiente:

1. El Ad Insertion de Adobe Primetime obtiene anuncios/creativos del servidor de publicidad del cliente.

1. Si el formato creativo de una publicidad es nativamente compatible con el flujo de contenido, el creativo se inserta en el manifiesto.

1. Si el formato creativo de un anuncio no es compatible de forma nativa (por ejemplo, .mp4, .mov, .webm), el Ad Insertion de Primetime busca una versión pretranscodificada del anuncio de una CDN específica. Si se encuentra uno, se inserta ese anuncio; de lo contrario, el anuncio se pone en cola para su transcodificación.

1. Una vez que se haya transcodificado el elemento creativo de la publicidad, el Ad Insertion de Primetime enlazará en los manifiestos todas las solicitudes posteriores para ese recurso de publicidad.

El Ad Insertion Primetime admite la transcodificación en la mayoría de los formatos de vídeo y lineal. La transcodificación creativa de publicidad suele producirse en menos de tres minutos. Póngase en contacto con su representante de asistencia técnica de Primetime para obtener más información.
