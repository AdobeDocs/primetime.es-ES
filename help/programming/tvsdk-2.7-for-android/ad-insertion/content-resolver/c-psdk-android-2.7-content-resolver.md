---
description: Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados del modo de señalización de publicidad, etc. El generador de oportunidades envía estas oportunidades de colocación a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
seo-description: Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados del modo de señalización de publicidad, etc. El generador de oportunidades envía estas oportunidades de colocación a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
seo-title: Personalización de los generadores de oportunidades y los solucionadores de contenido
title: Personalización de los generadores de oportunidades y los solucionadores de contenido
uuid: 97738b80-5cf8-494f-8811-449bceded220
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Información general {#customize-opportunity-generators-and-content-resolvers-overview}

Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados del modo de señalización de publicidad, etc. El generador de oportunidades envía estas oportunidades de colocación a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye los siguientes generadores de oportunidades predeterminados:

* `ManifestCuesOpportunityGenerator` genera oportunidades a partir de las señales de publicidad predeterminadas ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera una oportunidad inicial para el modo de señalización de publicidad especificado. Esto ignora cualquier señal o información de metadatos temporizados.
* `CustomMarkerOpportunityGenerator` genera oportunidades para reemplazar las publicidades C3 incorporadas.
* `AuditudeResolver`El generador de oportunidades de Omniture genera oportunidades cuando la resolución perezosa de anuncios está activada.

TVSDK también incluye los resueltores de contenido predeterminados:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que pueden comunicarse con Primetime y la toma de decisiones.

Puede anular los generadores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de la publicidad de formas como las siguientes:

* Reconocer etiquetas personalizadas para la inserción de publicidades
* Cree un proveedor de publicidad personalizado.
* Desactivar contenido.