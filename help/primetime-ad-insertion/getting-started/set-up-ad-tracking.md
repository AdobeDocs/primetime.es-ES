---
title: Configurar el seguimiento de publicidad
description: Configuración del seguimiento de publicidad
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Configurar el seguimiento de publicidad {#ser-up-ad-tracking}

La mayoría de los anunciantes requieren información sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus publicidades. Primetime Ad Insertion admite el seguimiento de anuncios híbridos, del lado del cliente y del lado del servidor para proporcionar flexibilidad en la recopilación de esta información.

## Seguimiento de anuncios del lado del cliente con VMAP/JSON {#client-side-ad-tracking-vmap-json}

En el seguimiento de anuncios del lado del cliente, el servidor envía al cliente una estructura JSON, VMAP o in-manifest que especifica eventos de seguimiento y direcciones URL junto con la lista de reproducción enlazada con la publicidad.

Para habilitar el seguimiento de publicidades en el lado del cliente, especifique los siguientes parámetros en la [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>Si se establece `pttrackingmode=simple`, la solicitud de API de arranque inicial devolverá una respuesta JSON, en lugar de un documento HLS o DASH.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## Seguimiento de anuncios del lado del servidor {#server-side-ad-tracking}

Con este método, los datos del seguimiento de anuncios se calculan por completo en el servidor. Esto resulta útil cuando no es posible actualizar la aplicación cliente. Sin embargo, es posible que el seguimiento de anuncios en el lado del servidor no coincida con la actividad de reproducción en el lado del cliente. Por ejemplo, el servidor considera que una publicidad se debe reproducir después de que se entreguen los segmentos, incluso si el usuario final no vista toda la publicidad.

Para habilitar el seguimiento de anuncios en el lado del servidor, especifique el siguiente parámetro en la [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

Consulte `pttrackingmode` secciones de [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

Todas las señalizaciones de seguimiento de publicidad se envían con los siguientes encabezados de solicitud HTTP:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Estos valores contienen la dirección IP del cliente/reproductor y del usuario-agente y del cliente.

## Seguimiento de publicidad híbrido {#hybrid-ad-tracking}

Este método es como el seguimiento del lado del servidor, pero la aplicación cliente también solicita sidecars desde Primetime Ad Insertion para obtener información detallada sobre el seguimiento. El seguimiento de anuncios híbridos puede enviar anuncios no lineales, como superposiciones y complementos, a la aplicación cliente, mientras que el Ad Insertion Primetime sigue confiando en que se envíen direcciones URL de seguimiento de anuncios individuales.
Para habilitar el seguimiento de anuncios híbridos, consulte el parámetro `pttrackingmode` en la [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).