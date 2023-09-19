---
description: Un generador de oportunidades identifica las oportunidades de ubicación mediante etiquetas personalizadas en un flujo, modo de señalización, marcadores personalizados, etc. El generador de oportunidades envía estas oportunidades de colocación al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
title: Personalizar generadores de oportunidades y solucionadores de contenido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Información general {#customize-opportunity-generators-and-content-resolvers-overview}

Un generador de oportunidades identifica las oportunidades de ubicación mediante etiquetas personalizadas en un flujo, modo de señalización, marcadores personalizados, etc. El generador de oportunidades envía estas oportunidades de colocación al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye los siguientes generadores de oportunidades predeterminados:

* `ManifestCuesOpportunityGenerator` genera oportunidades a partir de las señales de publicidad predeterminadas ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera una oportunidad inicial para el modo de señalización de anuncio especificado. Esto ignora cualquier señal o información de metadatos cronometrada.
* `CustomMarkerOpportunityGenerator` genera oportunidades para reemplazar anuncios C3 precocinados.
* `AuditudeResolver`El generador de oportunidades de produce oportunidades cuando la resolución de anuncios diferidos está activada.

TVSDK también incluye solucionadores de contenido predeterminados:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que puede comunicarse con Primetime y Decisioning.

Puede anular los generadores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de publicidad de las siguientes maneras:

* Reconocimiento de etiquetas personalizadas para la inserción de anuncios
* Cree un proveedor de publicidad personalizado.
* Contenido en negro.
