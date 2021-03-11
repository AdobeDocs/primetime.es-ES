---
description: Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados en modo de señalización de anuncios, etc. El generador de oportunidades envía estas oportunidades de colocación al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
title: Personalización de generadores de oportunidades y resolución de contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Información general {#customize-opportunity-generators-and-content-resolvers-overview}

Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados en modo de señalización de anuncios, etc. El generador de oportunidades envía estas oportunidades de colocación al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye los siguientes generadores de oportunidades predeterminados:

* `ManifestCuesOpportunityGenerator` genera oportunidades a partir de las señales de publicidad predeterminadas (  `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera una oportunidad inicial para el modo de señalización de anuncio especificado. Esto ignora cualquier señal o información de metadatos temporizados.
* `CustomMarkerOpportunityGenerator` genera oportunidades para reemplazar anuncios C3 incorporados.
* `AuditudeResolver`El generador de oportunidades de genera oportunidades cuando la resolución de anuncios perezosos está activada.

TVSDK también incluye los solucionadores de contenido predeterminados:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que pueden comunicarse con Primetime y decisioning.

Puede anular los generadores de oportunidades predeterminados y los solucionadores de contenido para personalizar el flujo de trabajo de la publicidad de formas como las siguientes:

* Reconocer etiquetas personalizadas para la inserción de anuncios. Para obtener más información, consulte [Personalización de los generadores de oportunidades y los solucionadores de contenido](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* Cree un proveedor de publicidad personalizado.
* Apaguen el contenido.