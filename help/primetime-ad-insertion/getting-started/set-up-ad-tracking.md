---
title: Configuración del seguimiento de anuncios
description: Configuración del seguimiento de anuncios
exl-id: b5ebad0f-4e20-456a-892d-4c981ab26e51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Configuración del seguimiento de anuncios {#ser-up-ad-tracking}

La mayoría de los anunciantes necesitan información sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus anuncios. El Ad Insertion de Primetime admite el seguimiento de anuncios híbridos, del lado del servidor y del lado del cliente para proporcionar flexibilidad a la hora de recopilar esta información.

## Seguimiento de anuncios del lado del cliente con VMAP/JSON {#client-side-ad-tracking-vmap-json}

En el seguimiento de anuncios del lado del cliente, el servidor envía al cliente una estructura JSON, VMAP o en manifiesto que especifica eventos de seguimiento y direcciones URL junto con la lista de reproducción vinculada a anuncios.

Para habilitar el seguimiento de anuncios del lado del cliente, especifique los siguientes parámetros en la variable [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>Configuración de la `pttrackingmode=simple` provocará que la solicitud inicial de la API de arranque devuelva una respuesta JSON, en lugar de un documento HLS o DASH.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## Seguimiento de anuncios del lado del servidor {#server-side-ad-tracking}

Con este método, los datos de seguimiento de anuncios se calculan completamente en el servidor. Esto resulta útil cuando no es posible actualizar la aplicación cliente. Sin embargo, es posible que el seguimiento de anuncios del lado del servidor no coincida con la actividad de reproducción del lado del cliente. Por ejemplo, el servidor considera que un anuncio se reproduce después de que se envíen los segmentos, incluso si el usuario final no ve todo el anuncio.

Para habilitar el seguimiento de anuncios del lado del servidor, especifique el siguiente parámetro en la [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

Consulte `pttrackingmode` secciones de [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

Todas las señalizaciones de seguimiento de anuncios se envían con los siguientes encabezados de solicitud HTTP:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Estos valores contienen el user-agent del cliente/reproductor y la dirección IP del cliente.

## Seguimiento de publicidad híbrida {#hybrid-ad-tracking}

Este método es similar al seguimiento del lado del servidor, pero la aplicación cliente también solicita sidecars del Ad Insertion de Primetime para obtener información detallada del seguimiento. El seguimiento de anuncios híbridos puede enviar anuncios no lineales como superposiciones y complementos a la aplicación cliente, mientras sigue dependiendo del Ad Insertion de Primetime para enviar direcciones URL de seguimiento de anuncios individuales.
Para habilitar el seguimiento de anuncios híbridos, consulte la `pttrackingmode` en el campo [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
