---
title: Transcodificación Just-In-Time
description: Transcodificación Just-In-Time
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Transcodificación Just-In-Time {#just-in-time-transcoding}

El Ad Insertion de Primetime incorpora transcodificación y empaquetado &quot;Just-In-Time&quot; para garantizar que los elementos creativos e incompatibles se puedan reproducir correctamente en las emisiones de contenido. También puede insertar paquetes ID3 en fragmentos de anuncios que se pueden utilizar en el seguimiento de anuncios del lado del cliente.
Un flujo de trabajo típico es el siguiente:

1. El Ad Insertion de Adobe Primetime recupera anuncios/creativos del servidor de publicidad del cliente.

1. Si el formato creativo de un anuncio es compatible de forma nativa con el flujo de contenido, el creativo se inserta en el manifiesto.

1. Si el formato creativo de un anuncio no es compatible de forma nativa (por ejemplo, .mp4, .mov, .webm), el Ad Insertion de Primetime busca una versión pretranscodificada del anuncio desde una CDN especificada. Si se encuentra uno, se inserta ese anuncio; de lo contrario, el anuncio se pone en cola para su transcodificación.

1. Una vez transcodificado el creativo de publicidad, el Ad Insertion de Primetime vinculará todas las solicitudes posteriores para ese recurso de publicidad en los manifiestos.

El Ad Insertion Primetime admite la transcodificación para la mayoría de los formatos lineales y de vídeo. La transcodificación creativa de anuncios suele producirse en menos de tres minutos. Póngase en contacto con su representante de asistencia técnica de Primetime para obtener más información.
