---
title: Transcodificación Just-in-Time
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Transcodificación Just-in-Time {#just-in-time-transcoding}

Primetime Ad Insertion ofrece transcodificación y empaquetado justo a tiempo para garantizar que los elementos creativos de publicidad incompatibles se puedan reproducir correctamente en los flujos de contenido. También puede inyectar paquetes de ID3 en fragmentos de publicidad que se pueden utilizar en el seguimiento de anuncios del lado del cliente.
A continuación se muestra un flujo de trabajo típico:

1. Adobe Primetime Ad Insertion obtiene publicidades/elementos creativos del servidor de publicidad del cliente.

1. Si el formato creativo de una publicidad es nativamente compatible con el flujo de contenido, el elemento creativo se inserta en el manifiesto.

1. Si el formato creativo de una publicidad no es nativamente compatible (por ejemplo, .mp4, .mov, .webm), el Ad Insertion de Primetime busca una versión pretranscodificada de la publicidad desde una CDN especificada. Si se encuentra uno, se inserta ese anuncio; de lo contrario, la publicidad se pone en cola para su transcodificación.

1. Una vez que el elemento creativo de la publicidad se haya transcodificado, el Ad Insertion de Primetime vinculará todas las solicitudes posteriores de ese recurso de publicidad en los manifiestos.

Primetime Ad Insertion admite la transcodificación para la mayoría de los formatos de vídeo y lineales. La transcodificación creativa de publicidad suele producirse en menos de tres minutos. Comuníquese con el representante de asistencia técnica de Primetime para obtener más detalles.
